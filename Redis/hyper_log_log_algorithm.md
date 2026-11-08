## What data structure does HyperLogLog use?

At a high level, **HyperLogLog (HLL)** is **not a traditional data structure** like a hash table or tree. It is a **probabilistic data structure** for estimating the number of distinct elements (cardinality) in a set while using a fixed amount of memory.

Internally, HyperLogLog primarily consists of the following:

### 1. Register Array (Core Data Structure)

The main data structure is an array of small integer registers.

```
Registers
+----+----+----+----+----+----+----+----+
|  3 |  0 |  5 |  2 |  1 |  4 |  2 |  6 |
+----+----+----+----+----+----+----+----+
```

If there are:

* `m = 2^p` registers
* each register stores a small integer

then the memory usage is approximately:

```
m × register_size
```

Typical implementations use:

* 5 bits/register
* 6 bits/register
* occasionally 8 bits/register

Example:

```
p = 14

m = 2^14 = 16384 registers

16384 × 6 bits
≈ 12 KB
```

This is enough to estimate billions of distinct values.

---

### 2. Hash Function

Every input item is first hashed into a uniformly distributed binary value.

Example:

```
"apple"

↓

MurmurHash3

↓

101001011010101011001...
```

The quality of the hash function is extremely important because HLL assumes a uniform distribution.

Common choices include:

* MurmurHash3
* xxHash
* SipHash
* CityHash

---

### 3. Register Index

The first `p` bits of the hash determine which register to update.

Example:

```
Hash

101001011010101001...

^^^^

Register #41
```

This is essentially an array lookup:

```
register[index]
```

---

### 4. Rank (Leading Zero Count)

The remaining bits are used to compute:

```
ρ(w)
```

which is the number of leading zeros plus one.

Example:

```
Remaining bits

000001010111...

Leading zeros = 5

Rank = 6
```

The register stores the maximum rank ever seen.

```
register[41]

Old = 4

New rank = 6

Store:

max(4,6)=6
```

---

## So what data structures are actually involved?

Internally:

```
HyperLogLog

 ├── Fixed-size array
 │      of registers
 │
 ├── Hash function
 │
 └── Small integer values
```

There are:

* no trees
* no linked lists
* no hash tables storing keys
* no Bloom filter
* no skip list

Just a compact register array.

---

## Sparse Representation (Many Implementations)

When the structure is nearly empty, allocating all registers is wasteful.

Many implementations (Redis, PostgreSQL, Apache DataSketches, etc.) start with a sparse representation.

Instead of

```
16384 registers
```

they store only the non-zero registers.

For example:

```
Register 10 -> 4
Register 25 -> 2
Register 91 -> 6
```

Internally this may be represented using:

```
Map

10 → 4
25 → 2
91 → 6
```

or

```
Sorted list

(10,4)
(25,2)
(91,6)
```

When enough registers become populated, the implementation converts to the dense register array.

---

## Time Complexity

For each insertion:

```
Hash            O(1)

Find register   O(1)

Leading zeros   O(1)

Update register O(1)
```

Overall:

```
Insert  : O(1)

Merge   : O(m)

Estimate: O(m)
```

where `m` is the fixed number of registers (typically 16K–64K).

---

## Memory Layout Example

```
Incoming element
        │
        ▼
   Hash Function
        │
        ▼
64-bit Hash
        │
 ┌──────┴────────┐
 │               │
 ▼               ▼
Index bits    Remaining bits
 │               │
 ▼               ▼
Register     Leading-zero count
 │               │
 └──────┬────────┘
        ▼
register[i] = max(register[i], rank)
```

### Summary

HyperLogLog is fundamentally built on:

* A **fixed-size array of small integer registers** (the primary data structure)
* A **uniform hash function** to map elements
* **Bit manipulation** (register indexing and leading-zero counting)
* Optionally, a **sparse map or sorted list** representation for low-cardinality sets before transitioning to the dense register array

This simplicity is one of the reasons HyperLogLog achieves excellent space efficiency while providing cardinality estimates with a relative error of about **1.04 / √m**.

---

## How is the cardinality estimated?

The key insight behind **HyperLogLog (HLL)** is surprisingly elegant:

> **The probability of observing a long run of leading zeros in a random hash decreases exponentially.** If you observe many leading zeros, it suggests you've likely seen many distinct elements.

Let's build up the intuition step by step.

---

# Step 1: Hash Every Element

Suppose you have the elements:

```
apple
banana
orange
grape
pear
```

Hash each one into a uniformly random 64-bit value.

```
apple   → 010011101001...
banana  → 111001010010...
orange  → 000000100101...
grape   → 001101010111...
pear     → 000010101101...
```

Because a good hash function behaves like a random number generator, each bit is equally likely to be 0 or 1.

---

# Step 2: Split the Hash

Suppose we use:

```
p = 4
```

Then:

* First 4 bits → register index
* Remaining 60 bits → rank computation

Example:

```
Hash

1011 | 000001010110...

^^^^
Register 11
```

The remaining bits are:

```
000001010110...
```

---

# Step 3: Count Leading Zeros

HyperLogLog computes:

```
ρ(w)
```

which is:

```
Leading zeros + 1
```

Example:

```
000001010...

Leading zeros = 5

Rank = 6
```

Why add one?

Simply because rank values begin at 1 instead of 0.

---

# Step 4: Update the Register

Suppose register 11 currently contains:

```
4
```

New rank:

```
6
```

Update:

```
register[11]

max(4,6)

↓

6
```

Each register remembers only the **largest** rank ever observed.

---

# Why Does This Work?

This is the brilliant statistical observation.

For random bits:

Probability the first bit is 1:

```
1/2
```

Probability of one leading zero:

```
01...

Probability = 1/4
```

Probability of two leading zeros:

```
001...

Probability = 1/8
```

Probability of three leading zeros:

```
0001...

Probability = 1/16
```

Generally:

```
P(rank = r)

≈ 2^(-r)
```

So seeing a rank of 20 is extremely rare.

```
Probability

≈ 1 / 2^20

≈ 1 / 1,048,576
```

This suggests you've probably processed around a million distinct values.

---

# One Register Gives a Rough Estimate

Suppose one register contains:

```
Rank = 10
```

This suggests

```
2^10

≈ 1024
```

distinct elements were needed before observing such a rare event.

But relying on a single register would produce a noisy estimate.

---

# Multiple Registers Reduce Variance

Suppose we have:

```
16 registers
```

```
[5,6,5,7,8,6,4,5,
 7,6,5,5,7,6,8,5]
```

Each register is an independent sample of the underlying distribution.

Combining them significantly improves accuracy.

---

# Why Not Use the Average?

Imagine:

```
[4,4,4,20]
```

Arithmetic mean:

```
(4+4+4+20)/4

= 8
```

This is dominated by the outlier (20).

Instead, HyperLogLog uses the **harmonic mean**, which is much less sensitive to large values.

Specifically, it computes:

[
Z=\left(\sum_{j=1}^{m}2^{-M_j}\right)^{-1}
]

where:

* (M_j) is the value stored in register (j)
* (m) is the number of registers

Registers with smaller values contribute much more to the sum, preventing a few unusually large ranks from dominating the estimate.

---

# Raw Cardinality Estimate

The raw estimate is:

[
E=\alpha_m,m^2,Z
]

where:

* (m) = number of registers
* (Z) = harmonic-mean term above
* (\alpha_m) = empirically derived bias-correction constant

Typical values are:

* (m=16): (\alpha_m \approx 0.673)
* (m=32): (\alpha_m \approx 0.697)
* (m=64): (\alpha_m \approx 0.709)
* Larger (m): (\alpha_m \approx \frac{0.7213}{1 + 1.079/m})

---

# Small-Cardinality Correction

If many registers are still zero, the raw estimate tends to overestimate.

Suppose:

```
16384 registers

15000 are still zero.
```

Clearly, not many distinct elements have been seen.

In this case, HyperLogLog switches to **Linear Counting**:

[
E = m \ln\left(\frac{m}{V}\right)
]

where:

* (V) = number of zero-valued registers

This produces much more accurate estimates for small cardinalities.

---

# Large-Cardinality Correction

When the estimate approaches the range of the hash space (e.g., a 32-bit hash nearing (2^{32})), collisions become significant, and an additional correction is applied.

With modern 64-bit hash functions, this correction is rarely needed in practice because the available hash space is enormous.

---

# Complete Estimation Pipeline

```
Incoming element
        │
        ▼
Hash (64-bit)
        │
        ▼
Split hash
        │
 ┌──────┴────────┐
 ▼               ▼
Register      Remaining bits
 index
                   │
                   ▼
          Leading-zero count
                   │
                   ▼
Update register = max(old, rank)
                   │
                   ▼
After all elements:
                   │
                   ▼
Compute harmonic mean
                   │
                   ▼
Apply bias correction
                   │
                   ▼
Small-range correction (if needed)
                   │
                   ▼
Large-range correction (if needed)
                   │
                   ▼
Estimated cardinality
```

### Why it is so accurate

HyperLogLog never stores the actual elements. It stores only the maximum observed leading-zero count for each register, yet these maxima collectively encode enough statistical information to estimate the number of distinct elements. The estimator is designed so that the **relative standard error** is approximately:

[
\frac{1.04}{\sqrt{m}}
]

For example:

| Registers ((m)) | Approx. Memory (6-bit registers) | Relative Error |
| --------------: | -------------------------------: | -------------: |
|           1,024 |                       ~768 bytes |         ~3.25% |
|           4,096 |                            ~3 KB |         ~1.63% |
|          16,384 |                           ~12 KB |         ~0.81% |
|          65,536 |                           ~48 KB |         ~0.41% |

This excellent trade-off between memory usage and accuracy is why HyperLogLog is widely used in systems like Redis, PostgreSQL, Apache Spark, BigQuery, and many large-scale analytics platforms.
