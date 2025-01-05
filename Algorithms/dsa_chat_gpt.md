## Give all the important DSA techniques to master for FAANG interviews. ##
To excel in FAANG interviews, mastering Data Structures and Algorithms (DSA) is critical. Here's a comprehensive list of key DSA techniques and concepts you should focus on:

---

## **Core Data Structures**
1. **Arrays and Strings**
   - Sliding Window Technique
   - Two Pointer Technique
   - Prefix Sum
   - Subarray problems

2. **Linked Lists**
   - Single and Doubly Linked Lists
   - Fast and Slow Pointers
   - Reversal of Linked List
   - Merge Two Sorted Linked Lists

3. **Stacks and Queues**
   - Stack and Queue Implementation
   - Monotonic Stacks/Queues
   - Circular Queue
   - Problems like Next Greater Element, Stock Span Problem

4. **Hashing**
   - Hash Maps, Hash Sets
   - Collision Handling
   - Anagram Grouping
   - Two-Sum and related problems

5. **Trees**
   - Binary Trees, Binary Search Trees
   - Trie (Prefix Tree)
   - AVL Tree, Red-Black Tree (basic understanding)
   - Tree Traversals: Preorder, Inorder, Postorder (recursive and iterative)
   - Lowest Common Ancestor (LCA)
   - Problems like Diameter of a Tree, Path Sum

6. **Graphs**
   - Graph Representations (Adjacency List, Adjacency Matrix)
   - Breadth-First Search (BFS), Depth-First Search (DFS)
   - Shortest Path Algorithms (Dijkstra, Bellman-Ford, Floyd-Warshall)
   - Minimum Spanning Tree (Kruskal, Prim)
   - Topological Sort
   - Strongly Connected Components (Kosaraju's or Tarjan's algorithm)
   - Union-Find (Disjoint Set Union)

---

## **Key Algorithmic Techniques**
1. **Sorting Algorithms**
   - Merge Sort, Quick Sort
   - Counting Sort, Radix Sort
   - Custom Sorting (Comparator Functions)

2. **Binary Search**
   - Standard Binary Search
   - Applications in Arrays, Search Space Reduction Problems
   - Lower and Upper Bound Searches

3. **Dynamic Programming (DP)**
   - Memoization vs Tabulation
   - Classic DP Problems:
     - Longest Common Subsequence
     - Longest Increasing Subsequence
     - Knapsack Problem
     - Coin Change Problem
     - Matrix Chain Multiplication
   - DP on Trees, Subsets, and Intervals

4. **Recursion and Backtracking**
   - Subset and Permutation Generation
   - N-Queens Problem
   - Sudoku Solver
   - Word Search on Grid

5. **Greedy Algorithms**
   - Interval Scheduling Problems
   - Huffman Encoding
   - Minimum Platforms Problem

6. **Divide and Conquer**
   - Applications in Sorting and Searching
   - Matrix Multiplication
   - Maximum Subarray Problem (Kadane's Algorithm)

7. **Bit Manipulation**
   - Bitwise Operators
   - XOR for Missing/Repeating Numbers
   - Subset Generation using Bits
   - Count Set Bits

8. **Math and Number Theory**
   - GCD, LCM
   - Prime Numbers (Sieve of Eratosthenes)
   - Modular Arithmetic
   - Fibonacci in Log Time (Matrix Exponentiation)

---

## **Advanced Topics**
1. **Segment Trees and Fenwick Trees**
   - Range Queries and Updates
   - Lazy Propagation

2. **Heaps and Priority Queues**
   - Min-Heap, Max-Heap
   - Median in a Stream
   - Top-K Elements

3. **Advanced Graph Algorithms**
   - A* Search Algorithm
   - Graph Coloring
   - Network Flow Algorithms (Ford-Fulkerson)

4. **Trie and String Algorithms**
   - KMP Algorithm
   - Rabin-Karp Algorithm
   - Suffix Arrays and Suffix Trees
   - Longest Palindromic Substring

---

## **Key Practices**
1. **Problem-Solving Skills**
   - Practice coding on platforms like LeetCode, HackerRank, Codeforces, and CodeChef.
   - Participate in mock interviews and coding contests.

2. **Time and Space Complexity**
   - Analyze the complexity of solutions for optimality.

3. **System Design (for senior roles)**
   - Understand Scalability, Load Balancing, and Database Sharding.
   - Practice design problems like URL Shortener, Cache System.

By mastering these techniques, you'll be well-prepared for DSA rounds in FAANG interviews. Let me know if you'd like a detailed guide on any specific topic!

## Give good problems that require using the Sliding Window Technique. ##
Here’s a curated list of problems that effectively use the **Sliding Window Technique**. These problems will help you master the approach across a variety of scenarios, from basic to advanced.

---

### **Easy Level**
1. **Maximum Sum Subarray of Size K**
   - Given an array and an integer K, find the maximum sum of a subarray of size K.
   - **Key Concept**: Fixed window size.

2. **First Negative Number in Every Window of Size K**
   - Given an array and a window size K, find the first negative number in each sliding window of size K.
   - **Key Concept**: Sliding window with additional tracking.

3. **Check for Anagram in a Sliding Window**
   - Given two strings, find if an anagram of the second string exists in a sliding window of the first string.
   - **Key Concept**: Use a frequency map.

---

### **Medium Level**
4. **Longest Substring Without Repeating Characters**
   - Given a string, find the length of the longest substring with unique characters.
   - **Key Concept**: Dynamic sliding window with character tracking.

5. **Minimum Size Subarray Sum**
   - Given an array of positive integers and a target sum, find the minimal length of a subarray whose sum is greater than or equal to the target.
   - **Key Concept**: Shrinking the window.

6. **Fruits into Baskets (LeetCode: Fruit Picker)**
   - You are given a tree with fruits, represented as an array. Each type of fruit is a different integer. Find the maximum number of fruits you can collect in two baskets.
   - **Key Concept**: Sliding window with at most two distinct elements.

7. **Longest Substring with At Most K Distinct Characters**
   - Find the length of the longest substring that contains at most K distinct characters.
   - **Key Concept**: Use a hashmap to track characters.

8. **Permutations in a String**
   - Given two strings s1 and s2, return true if s2 contains any permutation of s1.
   - **Key Concept**: Check for a frequency match within a sliding window.

9. **Binary Subarrays with Sum**
   - Given a binary array and a target sum, count the number of subarrays that sum up to the target.
   - **Key Concept**: Expand and shrink the window with sum tracking.

---

### **Hard Level**
10. **Maximum Sliding Window**
    - Given an array and a window size K, find the maximum element in each sliding window.
    - **Key Concept**: Use a deque to track maximum elements efficiently.

11. **Longest Substring with Exactly K Distinct Characters**
    - Find the length of the longest substring containing exactly K distinct characters.
    - **Key Concept**: Manage a hashmap with frequency tracking.

12. **Subarrays with K Different Integers**
    - Given an array, find the number of subarrays containing exactly K different integers.
    - **Key Concept**: Two sliding windows with frequency maps.

13. **Count of Substrings Containing All Three Characters**
    - Given a string, find the number of substrings containing at least one of each character: 'a', 'b', and 'c'.
    - **Key Concept**: Expand and contract the window while tracking counts.

14. **Longest Subarray with Sum Divisible by K**
    - Given an array and an integer K, find the longest subarray whose sum is divisible by K.
    - **Key Concept**: Use prefix sums and modular arithmetic in combination with sliding window.

15. **Maximum Consecutive Ones III**
    - Given a binary array, find the maximum number of consecutive 1s that can be achieved by flipping at most K 0s.
    - **Key Concept**: Track the count of flipped 0s in the window.

---

### **Practice Tips**
1. **Visualize the Window**: Think of the sliding window as a range of indices in the array or string.
2. **Dynamic Adjustments**: Practice problems where the window size is adjusted dynamically based on conditions.
3. **Optimize Space**: Learn to use maps or arrays to track counts or conditions efficiently.

Let me know if you'd like detailed explanations or solutions for any of these problems!

## Give good problems that require using the Two Pointer Technique. ##
The **Two Pointer Technique** is a powerful strategy for solving problems efficiently, particularly when dealing with sorted arrays, linked lists, or strings. Here's a collection of problems to practice and master this technique:

---

### **Easy Level**
1. **Pair with Target Sum (Sorted Array)**
   - Given a sorted array and a target sum, find the indices of the two numbers that add up to the target.
   - **Key Concept**: Start with one pointer at the beginning and another at the end, adjusting based on the sum.

2. **Remove Duplicates from Sorted Array**
   - Given a sorted array, remove duplicates in-place such that each element appears only once.
   - **Key Concept**: Use one pointer to iterate and another to mark the position for unique elements.

3. **Move Zeroes**
   - Given an array, move all zeroes to the end while maintaining the relative order of the non-zero elements.
   - **Key Concept**: Use two pointers to swap elements.

4. **Reverse a String**
   - Reverse a given string in-place.
   - **Key Concept**: Swap elements at the two pointers moving inward.

---

### **Medium Level**
5. **3Sum**
   - Find all unique triplets in the array that sum to zero.
   - **Key Concept**: Sort the array, fix one element, and use two pointers for the remaining two.

6. **Container with Most Water**
   - Given an array representing heights, find the maximum water area a container can trap.
   - **Key Concept**: Use two pointers to explore the widest container first and adjust based on the height.

7. **Sort Colors (Dutch National Flag Problem)**
   - Sort an array with values 0, 1, and 2 without using additional space.
   - **Key Concept**: Use two pointers to segregate values by swapping.

8. **Subarray Product Less Than K**
   - Count the number of subarrays where the product of all elements is less than K.
   - **Key Concept**: Expand and shrink the window using two pointers.

9. **Remove Nth Node from End of List**
   - Given a linked list, remove the Nth node from the end.
   - **Key Concept**: Use two pointers with a fixed gap.

10. **Longest Subarray with Ones After K Flips**
    - Find the length of the longest subarray of 1s if you can flip at most K 0s.
    - **Key Concept**: Move two pointers while tracking flipped 0s.

---

### **Hard Level**
11. **4Sum**
    - Find all unique quadruplets in the array that sum to a target value.
    - **Key Concept**: Extend 3Sum by fixing two elements and using two pointers for the other two.

12. **Minimum Window Substring**
    - Find the smallest substring of `s` that contains all characters of `t`.
    - **Key Concept**: Use two pointers to expand and contract the window.

13. **Trapping Rain Water**
    - Given an array of heights, calculate how much water can be trapped after raining.
    - **Key Concept**: Use two pointers to calculate trapped water from both ends.

14. **Find the Closest Pair from Two Sorted Arrays**
    - Given two sorted arrays, find a pair (one from each array) with the smallest absolute difference.
    - **Key Concept**: Use two pointers to traverse both arrays efficiently.

15. **Smallest Range Covering Elements from K Lists**
    - Given K sorted lists, find the smallest range that includes at least one element from each list.
    - **Key Concept**: Use a heap combined with two-pointer logic.

16. **Maximum of Minimum Values in Subarrays**
    - Find the maximum of the minimum values for every window size in the array.
    - **Key Concept**: Two pointers combined with a deque for optimization.

---

### **Tips for Two Pointer Problems**
1. **Sorted Input**: Many two-pointer problems work best on sorted arrays or lists.
2. **Opposite Directions**: For problems like sums or area maximization, use pointers starting from both ends.
3. **Same Direction**: For problems involving subarrays or substrings, use two pointers moving in the same direction.
4. **Optimization**: Identify when to move the left pointer (shrink the window) and when to move the right pointer (expand the window).

---

These problems will help you build intuition and efficiency with the two-pointer technique. Let me know if you’d like detailed solutions or explanations for any of them!

## Give good problems that require using the Prefix Sum technique. ##
The **Prefix Sum Technique** is widely used for efficiently solving problems involving cumulative sums or range queries. Here's a list of excellent problems to practice the technique:

---

### **Easy Level**
1. **Running Sum of 1D Array**
   - Compute the running sum of an array.
   - **Key Concept**: Iteratively add elements to the prefix sum.

2. **Find Pivot Index**
   - Find an index such that the sum of elements to its left is equal to the sum of elements to its right.
   - **Key Concept**: Use prefix sums to calculate the left and right sums.

3. **Subarray Sum Equals K**
   - Given an array of integers and a target `k`, find the total number of subarrays whose sum equals `k`.
   - **Key Concept**: Use a prefix sum hashmap for efficient range sum lookups.

4. **Range Sum Query - Immutable**
   - Given an array, calculate the sum of elements between indices `i` and `j` (inclusive) for multiple queries.
   - **Key Concept**: Precompute prefix sums to answer range queries in constant time.

---

### **Medium Level**
5. **Longest Subarray with Sum Divisible by K**
   - Find the length of the longest subarray with a sum divisible by `k`.
   - **Key Concept**: Use prefix sum modulo and hashmap to detect repeated remainders.

6. **Maximum Subarray Sum with Size Exactly K**
   - Find the maximum sum of any subarray of size exactly `k`.
   - **Key Concept**: Use prefix sums to avoid recomputing sums for overlapping subarrays.

7. **Sum of All Odd Length Subarrays**
   - Find the sum of all possible odd-length subarrays in an array.
   - **Key Concept**: Calculate contributions of each element using prefix sums.

8. **Count Number of Nice Subarrays**
   - Find the number of subarrays containing exactly `k` odd numbers.
   - **Key Concept**: Use prefix sum to count occurrences of odd-numbered subarrays.

9. **Split Array into Two with Equal Sum**
   - Determine if an array can be split into two parts with equal sum.
   - **Key Concept**: Use the total sum and prefix sums to find the split point.

---

### **Hard Level**
10. **Maximum Subarray Sum with At Most K Elements**
    - Find the maximum sum of a subarray that has at most `k` elements.
    - **Key Concept**: Use prefix sums to track sums dynamically.

11. **Subarrays with Bounded Maximum**
    - Count subarrays where the maximum value is within a given range.
    - **Key Concept**: Use prefix sums to count valid subarrays efficiently.

12. **Ways to Split Array into Three Parts**
    - Count the number of ways to split an array into three contiguous parts such that the sum of each part is at least `k`.
    - **Key Concept**: Use prefix sums to identify valid split points.

13. **Minimum Value to Get Positive Step-by-Step Sum**
    - Find the minimum value you can add to all elements such that the cumulative sum never goes below zero.
    - **Key Concept**: Track prefix sums and ensure positivity.

14. **Maximum Sum of Two Non-Overlapping Subarrays**
    - Find the maximum sum of two non-overlapping subarrays of specified lengths.
    - **Key Concept**: Use prefix sums to compute sums for overlapping and non-overlapping regions.

15. **Sum of All Subarrays**
    - Calculate the sum of all possible subarrays of a given array.
    - **Key Concept**: Use prefix sums to determine contributions of each subarray efficiently.

---

### **Advanced/Variants**
16. **2D Range Sum Queries**
    - Compute the sum of elements within a submatrix defined by its top-left and bottom-right corners.
    - **Key Concept**: Use a 2D prefix sum array.

17. **Maximum Sum Rectangle in a 2D Matrix**
    - Find the rectangle in a 2D matrix with the maximum sum.
    - **Key Concept**: Use prefix sums to convert the problem into a 1D maximum subarray problem.

18. **Count Subarrays with Given XOR**
    - Count the number of subarrays with a given XOR value.
    - **Key Concept**: Use prefix sums with XOR properties.

19. **Find All Continuous Subarrays with Sum Zero**
    - Count and return all subarrays whose sum is zero.
    - **Key Concept**: Use prefix sum hashmap to track cumulative sums.

20. **Maximize Sum After K Negations**
    - Maximize the sum of an array after negating exactly `k` elements.
    - **Key Concept**: Use prefix sums to manage contributions efficiently.

---

### **Tips for Prefix Sum Problems**
1. **Precompute and Store**: Store prefix sums in an array or hashmap for efficient range query computations.
2. **Modulo Arithmetic**: Use modulo operations with prefix sums for divisibility problems.
3. **Edge Cases**: Handle negative numbers, empty subarrays, and boundary conditions carefully.
4. **Optimize with Hashmaps**: For problems requiring counts or conditions, hashmaps often make solutions more efficient.

---

These problems cover a wide range of applications of the prefix sum technique. Let me know if you'd like explanations, hints, or solutions for any of these!

## Give good Subarray problems. ##
Here’s a curated list of excellent subarray problems to help you master the concept. These problems are categorized by difficulty and cover a variety of techniques like sliding window, prefix sum, and two-pointer approaches.

---

### **Easy Level**
1. **Maximum Sum Subarray of Size K**
   - Find the maximum sum of all subarrays of size K.
   - **Key Concept**: Sliding window with fixed size.

2. **Find All Subarrays with Sum Zero**
   - Count and return all subarrays whose sum is zero.
   - **Key Concept**: Prefix sum with hashmap to track sums.

3. **Subarray Sum Equals K**
   - Find the total number of continuous subarrays that sum up to `k`.
   - **Key Concept**: Prefix sum hashmap.

4. **Remove Duplicates from Sorted Array**
   - Modify the array in-place to remove duplicates such that each element appears only once.
   - **Key Concept**: Subarray manipulation using pointers.

5. **Count Odd Numbers in Intervals**
   - Given an array, find subarrays containing a specific number of odd numbers.
   - **Key Concept**: Two-pointer method.

---

### **Medium Level**
6. **Maximum Product Subarray**
   - Find the contiguous subarray within an array (containing at least one number) that has the largest product.
   - **Key Concept**: Dynamic programming with min and max product tracking.

7. **Longest Subarray with Sum Divisible by K**
   - Find the length of the longest subarray with a sum divisible by `k`.
   - **Key Concept**: Prefix sum modulo tracking.

8. **Longest Subarray with At Most K Distinct Characters**
   - Find the length of the longest subarray containing at most `k` distinct characters.
   - **Key Concept**: Sliding window with frequency hashmap.

9. **Subarray Product Less Than K**
   - Count the number of subarrays where the product of all elements is less than `k`.
   - **Key Concept**: Two-pointer or sliding window.

10. **Longest Subarray with Equal Number of 0s and 1s**
    - Replace 0s with -1 and find the longest subarray with a sum of zero.
    - **Key Concept**: Prefix sum with hashmap.

11. **Kadane’s Algorithm (Maximum Subarray)**
    - Find the maximum sum of a contiguous subarray.
    - **Key Concept**: Dynamic programming.

12. **Count Subarrays with XOR Equal to K**
    - Count the number of subarrays that have a given XOR value.
    - **Key Concept**: Prefix XOR with hashmap.

13. **Split Array into Consecutive Subsequences**
    - Determine if the array can be split into subsequences of consecutive integers.
    - **Key Concept**: Hashmaps for subarray tracking.

---

### **Hard Level**
14. **Maximum Sliding Window**
    - Find the maximum value in every subarray of size K as the window slides.
    - **Key Concept**: Deque to maintain maximum efficiently.

15. **Shortest Subarray with Sum at Least K**
    - Find the shortest subarray with a sum greater than or equal to `k`.
    - **Key Concept**: Prefix sum and two-pointer method.

16. **Subarrays with K Different Integers**
    - Count subarrays with exactly `k` distinct integers.
    - **Key Concept**: Sliding window with two hashmaps.

17. **Maximum Sum of Two Non-Overlapping Subarrays**
    - Find the maximum sum of two non-overlapping subarrays of specified lengths.
    - **Key Concept**: Prefix sum to track non-overlapping regions.

18. **Largest Subarray with Contiguous Elements**
    - Find the length of the largest subarray where the elements are contiguous, though not sorted.
    - **Key Concept**: Hashset to check for contiguous ranges.

19. **Sum of All Odd Length Subarrays**
    - Calculate the sum of all possible odd-length subarrays in an array.
    - **Key Concept**: Math with prefix sum to calculate contributions.

20. **Maximum Subarray Sum After K Negations**
    - Maximize the sum of a subarray after negating exactly `k` elements.
    - **Key Concept**: Greedy or heap-based approach.

21. **Maximum Subarray with a Constraint**
    - Find the maximum sum of a subarray such that the subarray’s sum is less than or equal to `S`.
    - **Key Concept**: Sliding window or prefix sum with binary search.

22. **K-Concatenated Maximum Sum**
    - Given an array and an integer `k`, find the maximum sum of a subarray in a new array formed by repeating the array `k` times.
    - **Key Concept**: Kadane's algorithm with modular arithmetic.

---

### **2D Subarray Problems**
23. **Maximum Sum Rectangle in a 2D Matrix**
    - Find the sub-matrix with the maximum sum.
    - **Key Concept**: Reduce the problem to 1D Kadane's using prefix sums for rows.

24. **Range Sum Query 2D - Immutable**
    - Given a 2D matrix, compute the sum of the elements in a rectangular sub-matrix.
    - **Key Concept**: Precompute prefix sum for efficient range queries.

---

### **Practice Tips**
1. **Use Visualizations**: Draw or visualize the subarray ranges while solving problems.
2. **Break Down Conditions**: For complex constraints, simplify the problem into smaller parts.
3. **Precompute**: Use prefix sums or hashmaps to speed up subarray queries.
4. **Iterate in Multiple Ways**: Explore sliding window, prefix sum, and dynamic programming for different approaches.

Let me know if you’d like detailed explanations or solutions for any of these problems!

## Give good Single and Doubly Linked Lists problems. ##
Here’s a curated list of excellent **Single** and **Doubly Linked List** problems categorized by difficulty. These problems cover a variety of operations, techniques, and real-world applications, which are essential for mastering linked lists.

---

### **Single Linked List Problems**

#### **Easy Level**
1. **Reverse a Linked List**
   - Reverse a singly linked list.
   - **Key Concept**: Use pointers to reverse links iteratively or recursively.

2. **Merge Two Sorted Linked Lists**
   - Merge two sorted linked lists into a single sorted list.
   - **Key Concept**: Two-pointer traversal.

3. **Middle of the Linked List**
   - Find the middle node of a linked list.
   - **Key Concept**: Use two pointers (slow and fast).

4. **Detect a Cycle in a Linked List**
   - Determine if a linked list contains a cycle.
   - **Key Concept**: Floyd’s Cycle Detection Algorithm (slow and fast pointers).

5. **Remove Nth Node from the End**
   - Remove the nth node from the end of a linked list.
   - **Key Concept**: Two-pass traversal or two-pointer technique.

6. **Delete Node in a Linked List**
   - Delete a given (non-tail) node in a singly linked list, given only access to that node.
   - **Key Concept**: Modify the node directly.

---

#### **Medium Level**
7. **Add Two Numbers**
   - Given two linked lists representing numbers in reverse order, add them and return the sum as a linked list.
   - **Key Concept**: Traverse both lists while handling carry.

8. **Intersection of Two Linked Lists**
   - Find the node where two singly linked lists intersect.
   - **Key Concept**: Calculate lengths or use two-pointer approach.

9. **Remove Duplicates from Sorted List**
   - Remove duplicate nodes from a sorted linked list.
   - **Key Concept**: Traverse and skip duplicates.

10. **Reorder List**
    - Rearrange the list such that the order becomes: first node, last node, second node, second last node, etc.
    - **Key Concept**: Split the list, reverse the second half, and merge.

11. **Flatten a Multilevel Doubly Linked List**
    - Flatten a multilevel doubly linked list where each node may have a child list.
    - **Key Concept**: Recursively traverse and merge child nodes.

12. **Split Linked List in Parts**
    - Split a linked list into k equal parts as evenly as possible.
    - **Key Concept**: Calculate the size of each part and traverse accordingly.

---

#### **Hard Level**
13. **Reverse Nodes in K-Group**
    - Reverse the nodes of a linked list in groups of k.
    - **Key Concept**: Iteratively reverse groups while keeping track of connections.

14. **Copy List with Random Pointer**
    - Clone a linked list where each node has a random pointer in addition to the next pointer.
    - **Key Concept**: Use a hashmap or modify the original list to create the copy.

15. **LRU Cache Implementation**
    - Implement an LRU (Least Recently Used) cache using a linked list and a hashmap.
    - **Key Concept**: Doubly linked list combined with a hashmap.

16. **Sort a Linked List**
    - Sort a linked list in O(n log n) time.
    - **Key Concept**: Merge sort with linked lists.

17. **Rotate List**
    - Rotate a linked list to the right by k places.
    - **Key Concept**: Make the list circular and break at the appropriate position.

18. **Linked List in Binary Tree**
    - Check if a linked list is a subpath of a binary tree.
    - **Key Concept**: DFS in the binary tree while matching the list.

---

### **Doubly Linked List Problems**

#### **Easy Level**
1. **Insert at Head and Tail**
   - Insert nodes at the head and tail of a doubly linked list.
   - **Key Concept**: Update previous and next pointers.

2. **Delete a Node**
   - Delete a given node from a doubly linked list.
   - **Key Concept**: Adjust pointers of the previous and next nodes.

3. **Reverse a Doubly Linked List**
   - Reverse the given doubly linked list.
   - **Key Concept**: Swap the next and prev pointers iteratively.

---

#### **Medium Level**
4. **Flatten a Doubly Linked List**
   - Given a doubly linked list where each node may have a child, flatten it.
   - **Key Concept**: Use recursion or an iterative stack-based approach.

5. **Find the K-th Node from the End**
   - Find the k-th node from the end of a doubly linked list.
   - **Key Concept**: Traverse both forward and backward.

6. **Add Nodes in a Circular Doubly Linked List**
   - Insert nodes into a circular doubly linked list and handle edge cases.
   - **Key Concept**: Maintain circular connections.

---

#### **Hard Level**
7. **Design Browser History**
   - Implement a browser history feature using a doubly linked list.
   - **Key Concept**: Navigate forward and backward efficiently.

8. **LRU Cache (Doubly Linked List Version)**
   - Use a doubly linked list to implement an LRU cache.
   - **Key Concept**: Efficiently remove and add nodes at the head and tail.

---

### **Tips for Linked List Problems**
1. **Draw It Out**: Visualizing node connections and changes can help understand tricky problems.
2. **Edge Cases**: Handle edge cases such as empty lists, single-node lists, and cycles.
3. **Recursive vs. Iterative**: Many linked list problems can be solved both ways; choose based on simplicity.
4. **Pointer Management**: Be cautious with pointer updates to avoid breaking links.

Let me know if you'd like explanations or solutions for any of these problems!

## Give good problems that require using the Fast and Slow Pointers techniques. ##
The **Fast and Slow Pointers** (also known as the Floyd's Tortoise and Hare technique) is a powerful approach to solve problems that involve cyclic or overlapping structures in linked lists, arrays, and other sequences. Below is a list of excellent problems to practice and master this technique.

---

### **Classic Problems in Linked Lists**

#### **Easy Level**
1. **Middle of the Linked List**
   - Find the middle node of a linked list.
   - **Key Concept**: Move one pointer twice as fast as the other; the slow pointer will stop at the middle.

2. **Detect a Cycle in a Linked List**
   - Check if a linked list contains a cycle.
   - **Key Concept**: Use fast and slow pointers to detect if they meet.

3. **Length of the Cycle in a Linked List**
   - After detecting a cycle, find its length.
   - **Key Concept**: Count the number of steps for the fast pointer to loop back to the slow pointer.

#### **Medium Level**
4. **Start of the Cycle in a Linked List**
   - Find the starting node of the cycle in a linked list.
   - **Key Concept**: After detection, reset one pointer to the head and move both at the same speed.

5. **Palindrome Linked List**
   - Check if a linked list is a palindrome.
   - **Key Concept**: Use the slow pointer to find the middle, reverse the second half, and compare both halves.

6. **Intersection of Two Linked Lists**
   - Find the node where two linked lists intersect.
   - **Key Concept**: Use two pointers, but fast and slow can be used to check relative distances if a cycle exists.

---

### **Cyclic Problems in Arrays**

#### **Medium Level**
7. **Circular Array Loop**
   - Determine if there’s a cycle in a circular array.
   - **Key Concept**: Treat array indices as nodes in a circular linked list and use fast and slow pointers.

8. **Find the Duplicate Number**
   - Given an array of integers where each number appears once except for one duplicate, find the duplicate.
   - **Key Concept**: Treat the array as a linked list where indices point to the next element, and use the cycle detection technique.

---

### **Hard Level**
9. **First Missing Positive**
   - Find the smallest missing positive integer in an unsorted array.
   - **Key Concept**: Use fast and slow pointers for optimization in the cycle-sort approach.

10. **Split Linked List into Two Halves**
    - Split a linked list into two halves, one larger than the other if the length is odd.
    - **Key Concept**: Use the slow pointer to find the middle and split accordingly.

---

### **Time-Based Problems**

#### **Medium Level**
11. **Happy Number**
    - Determine if a number eventually reaches 1 when repeatedly replacing it with the sum of the squares of its digits.
    - **Key Concept**: Use fast and slow pointers to detect cycles in the process.

12. **Linked List Cycle II**
    - Similar to detecting a cycle in a linked list but requires returning the entry point of the cycle.
    - **Key Concept**: Combine cycle detection with pointer reset.

---

### **Pattern Recognition Problems**

#### **Hard Level**
13. **Maximum Twin Sum of a Linked List**
    - Find the maximum sum of pairs of nodes from the first and last halves of a linked list.
    - **Key Concept**: Use the slow pointer to find the middle, reverse the second half, and calculate sums.

14. **K-th Node from the End**
    - Find the k-th node from the end of a linked list.
    - **Key Concept**: Use two pointers where the fast pointer is k steps ahead.

15. **Smallest Window with All Distinct Characters**
    - Given a string, find the smallest substring that contains all distinct characters.
    - **Key Concept**: Fast pointer moves to expand the window, and the slow pointer adjusts it.

---

### **Advanced Linked List Problems**

#### **Hard Level**
16. **Rearrange Linked List**
    - Rearrange a linked list such that it becomes a specific order like `L0 → Ln → L1 → Ln-1 → ...`.
    - **Key Concept**: Use the slow pointer to split the list, reverse the second half, and merge.

17. **Sort Linked List**
    - Sort a linked list in O(n log n) time.
    - **Key Concept**: Use slow and fast pointers to divide the list into halves for merge sort.

---

### **Key Tips for Fast and Slow Pointers**
1. **Cycle Detection**: The fast pointer moves twice as fast as the slow pointer; if there's a cycle, they'll eventually meet.
2. **Middle Element**: In any sequence, fast and slow pointers help locate the middle element efficiently.
3. **Pointer Reset**: After detecting a cycle, resetting one pointer to the head often helps find the start of the cycle.
4. **Visualization**: For array-based problems, treat indices as nodes and simulate movement.

Let me know if you'd like detailed explanations or solutions for any of these problems!

## Give good problems requiring the Reversal of the Linked List technique. ##
Reversing a linked list is a fundamental operation that serves as the foundation for solving numerous linked list problems. Here’s a list of excellent problems that directly or indirectly require reversing a linked list, categorized by difficulty:

---

### **Easy Level**
1. **Reverse a Linked List**
   - Reverse an entire singly linked list.
   - **Key Concept**: Iteratively adjust pointers or use recursion.

2. **Reverse a Doubly Linked List**
   - Reverse a doubly linked list.
   - **Key Concept**: Swap `next` and `prev` pointers for each node.

3. **Palindrome Linked List**
   - Check if a linked list is a palindrome.
   - **Key Concept**: Reverse the second half of the list and compare with the first half.

4. **Reverse First K Nodes**
   - Reverse the first `k` nodes of a singly linked list.
   - **Key Concept**: Reverse up to `k` nodes while keeping track of connections.

---

### **Medium Level**
5. **Reverse Nodes in K-Group**
   - Reverse the nodes of a linked list in groups of `k`.
   - **Key Concept**: Iteratively reverse `k` nodes and connect sublists.

6. **Reorder List**
   - Given a linked list, reorder it to: `L0 → Ln → L1 → Ln-1 → ...`.
   - **Key Concept**: Split the list into two halves, reverse the second half, and merge alternately.

7. **Reverse Linked List Between Positions**
   - Reverse a segment of a linked list between two positions `left` and `right`.
   - **Key Concept**: Reverse the sublist while maintaining external connections.

8. **Add Two Numbers (Linked Lists)**
   - Given two linked lists representing numbers, add them.
   - **Key Concept**: Reverse both lists to make addition easier (or add directly without reversing).

9. **Flatten a Multilevel Doubly Linked List**
   - Flatten a multilevel doubly linked list into a single-level doubly linked list.
   - **Key Concept**: Use recursion and adjust `next` and `prev` pointers while reversing child lists.

10. **Split Linked List in Half**
    - Split a linked list into two halves, and reverse one half for comparison or further operations.
    - **Key Concept**: Use slow and fast pointers to find the middle, then reverse the second half.

---

### **Hard Level**
11. **Rotate a Linked List**
    - Rotate the list to the right by `k` positions.
    - **Key Concept**: Reverse the entire list, then reverse segments to achieve the desired rotation.

12. **Sort a Linked List**
    - Sort a linked list in O(n log n) time.
    - **Key Concept**: Use merge sort with reversal during the merging phase for simplicity.

13. **Maximum Twin Sum of a Linked List**
    - Find the maximum sum of pairs of nodes from the first and last halves of a linked list.
    - **Key Concept**: Reverse the second half and calculate sums.

14. **Reverse Alternating K-Group Nodes**
    - Reverse alternating groups of `k` nodes in a linked list.
    - **Key Concept**: Reverse `k` nodes, skip `k` nodes, and repeat the process.

15. **Reverse Pairs in a Linked List**
    - Swap every two adjacent nodes in the linked list.
    - **Key Concept**: Reverse two nodes at a time iteratively or recursively.

---

### **Bonus Problems with Variations**
16. **Reverse a Circular Linked List**
    - Reverse a circular singly or doubly linked list.
    - **Key Concept**: Similar to reversing a normal list but handle circular connections.

17. **Zig-Zag Reorder**
    - Rearrange the list into a zig-zag pattern such that `L0 < L1 > L2 < L3...`.
    - **Key Concept**: Use partial reversal and reordering.

18. **Reverse Linked List Using Stack**
    - Reverse the linked list using a stack (non-pointer-based method).
    - **Key Concept**: Push all nodes onto a stack and pop them to rebuild the list.

19. **Reverse a Sublist in Circular Linked List**
    - Reverse a segment of a circular linked list.
    - **Key Concept**: Handle pointers carefully to maintain circular structure.

20. **Design Linked List**
    - Implement a linked list with custom operations like reverse, insert, and delete.
    - **Key Concept**: Modularize reversal logic to integrate efficiently.

---

### **Tips for Reversal Problems**
1. **Visualization**: Draw diagrams to clearly understand pointer adjustments during reversal.
2. **Iterative vs. Recursive**: Choose based on problem constraints (iterative is more memory efficient; recursion can be elegant).
3. **Edge Cases**: Handle cases like empty lists, single-node lists, and sublist reversals at boundaries.
4. **Practice Pointer Management**: Correctly maintaining `prev`, `current`, and `next` is crucial to avoid breaking links.

Let me know if you’d like detailed explanations or solutions for any of these problems!

## Give good problems requiring the Merge Two Sorted Linked Lists technique. ##
The "Merge Two Sorted Linked Lists" technique is a foundational problem that introduces the concept of merging sorted sequences efficiently. It forms the basis for many advanced linked list problems and is often used in divide-and-conquer algorithms like merge sort. Below is a list of problems requiring this technique, categorized by difficulty:

---

### **Easy Level**
1. **Merge Two Sorted Lists**  
   - Merge two sorted linked lists into one sorted linked list.  
   - **Key Concept**: Compare nodes one by one and build a new list iteratively or recursively.

2. **Merge K Sorted Lists (Two-by-Two)**  
   - Simplify the problem of merging \(k\) sorted lists by repeatedly merging pairs of lists.  
   - **Key Concept**: Apply the "merge two lists" technique iteratively.

3. **Merge Two Sorted Arrays (as a List)**  
   - Given two sorted arrays, merge them as if they were linked lists.  
   - **Key Concept**: Simulate the merge process using array indices.

---

### **Medium Level**
4. **Merge K Sorted Lists**  
   - Merge \(k\) sorted linked lists into one sorted list.  
   - **Key Concept**: Use a priority queue (min-heap) or divide-and-conquer strategy with "merge two lists."

5. **Merge Intervals**  
   - Given a list of sorted intervals, merge all overlapping intervals.  
   - **Key Concept**: Similar to merging sorted lists, compare and combine overlapping ranges.

6. **Sort List**  
   - Sort a linked list in \(O(n \log n)\) time.  
   - **Key Concept**: Use merge sort by splitting the list into halves and merging sorted sublists.

7. **Merge Two Sorted Circular Linked Lists**  
   - Merge two sorted circular linked lists into one sorted circular list.  
   - **Key Concept**: Adjust pointers carefully to maintain circular connections.

---

### **Hard Level**
8. **Flatten a Multilevel Doubly Linked List**  
   - Flatten a multilevel doubly linked list where each node may have a child list.  
   - **Key Concept**: Treat each level as a sorted list and merge recursively.

9. **Merge Two BSTs (as Linked Lists)**  
   - Convert two binary search trees into sorted linked lists and merge them.  
   - **Key Concept**: In-order traversal for BST to list conversion and apply the merge technique.

10. **Merge Two Sorted Linked Lists with Random Pointers**  
    - Merge two sorted linked lists where nodes also have random pointers.  
    - **Key Concept**: Carefully handle the random pointers while merging.

11. **Merge Sorted Segments of a List**  
    - Given a single linked list divided into multiple sorted segments, merge them into one sorted list.  
    - **Key Concept**: Identify boundaries of segments and apply the merge operation iteratively.

12. **Merge Lists Alternately**  
    - Merge two sorted linked lists such that nodes are alternately picked from both lists.  
    - **Key Concept**: Modify the standard merge technique to alternate node selection.

13. **Merge Two Sorted Doubly Linked Lists**  
    - Merge two sorted doubly linked lists.  
    - **Key Concept**: Adjust both `prev` and `next` pointers during the merge process.

---

### **Bonus Variations**
14. **Merge Two Arrays into a Linked List**  
    - Convert two sorted arrays into linked lists and merge them.  
    - **Key Concept**: Simulate the merge process and construct the resulting linked list.

15. **Merge Sorted Segments in-place**  
    - Merge sorted portions of a single linked list in-place without using extra space.  
    - **Key Concept**: Reorder nodes directly instead of creating a new list.

---

### **Key Tips for Merge Problems**
1. **Recursive vs. Iterative**: Recursive solutions are elegant but may cause stack overflow for very large lists. Iterative approaches are generally safer.
2. **Edge Cases**: Handle empty lists and cases where all elements come from one list.
3. **Efficient Pointer Management**: Maintain clear control over `next` pointers to avoid breaking the list structure.
4. **Optimization for K-Way Merges**: Use divide-and-conquer or a heap-based approach to optimize multi-list merging.

Let me know if you'd like detailed explanations, code samples, or solutions for any of these problems!

## Give good problems requiring Stack and Queue Implementation. ##
Stacks and queues are foundational data structures, and mastering their implementation is essential for solving a wide range of problems. Here’s a list of problems that require implementing stacks and queues or rely heavily on their operations, categorized by difficulty:

---

### **Stack-Based Problems**

#### **Easy Level**
1. **Implement Stack Using Arrays**  
   - Implement a stack using an array with operations like `push`, `pop`, and `peek`.  
   - **Key Concept**: Maintain a top pointer for stack operations.

2. **Implement Stack Using Linked List**  
   - Use a linked list to create a stack with dynamic resizing.  
   - **Key Concept**: Push and pop from the head for \(O(1)\) operations.

3. **Valid Parentheses**  
   - Check if a string of parentheses is valid.  
   - **Key Concept**: Use a stack to match opening and closing brackets.

4. **Min Stack**  
   - Design a stack that supports retrieving the minimum element in \(O(1)\).  
   - **Key Concept**: Maintain an auxiliary stack to store minimum values.

---

#### **Medium Level**
5. **Evaluate Reverse Polish Notation**  
   - Evaluate an arithmetic expression given in postfix notation.  
   - **Key Concept**: Use a stack to store intermediate results.

6. **Sort a Stack**  
   - Sort a stack using recursion or another stack.  
   - **Key Concept**: Use a temporary stack for sorting.

7. **Next Greater Element**  
   - Find the next greater element for each element in an array.  
   - **Key Concept**: Use a monotonic decreasing stack.

8. **Daily Temperatures**  
   - Find the number of days until a warmer temperature for each day.  
   - **Key Concept**: Use a stack to store indices and temperatures.

---

#### **Hard Level**
9. **Largest Rectangle in Histogram**  
   - Find the largest rectangle that can be formed in a histogram.  
   - **Key Concept**: Use a stack to calculate the width of each rectangle.

10. **Trapping Rain Water**  
    - Calculate the amount of water trapped between buildings.  
    - **Key Concept**: Use a stack to track elevation boundaries.

11. **Remove K Digits**  
    - Remove \(k\) digits from a number to get the smallest possible result.  
    - **Key Concept**: Use a stack to build the result digit by digit.

12. **Asteroid Collision**  
    - Simulate the collision of asteroids represented as integers.  
    - **Key Concept**: Use a stack to process collisions iteratively.

---

### **Queue-Based Problems**

#### **Easy Level**
1. **Implement Queue Using Arrays**  
   - Implement a queue using an array with operations like `enqueue`, `dequeue`, and `peek`.  
   - **Key Concept**: Use circular indexing for efficient memory usage.

2. **Implement Queue Using Linked List**  
   - Use a linked list to create a dynamically resizable queue.  
   - **Key Concept**: Maintain head and tail pointers.

3. **Implement Queue Using Stacks**  
   - Design a queue using two stacks.  
   - **Key Concept**: Use one stack for enqueue and the other for dequeue operations.

4. **Design Circular Queue**  
   - Implement a circular queue with fixed capacity.  
   - **Key Concept**: Handle circular indexing and full/empty conditions.

---

#### **Medium Level**
5. **Sliding Window Maximum**  
   - Find the maximum in each sliding window of size \(k\) in an array.  
   - **Key Concept**: Use a deque (double-ended queue) to maintain candidate indices.

6. **Rotten Oranges**  
   - Find the minimum time required to rot all oranges in a grid.  
   - **Key Concept**: Use a queue for BFS traversal.

7. **Binary Tree Level Order Traversal**  
   - Traverse a binary tree level by level.  
   - **Key Concept**: Use a queue to process nodes level by level.

8. **Number of Islands**  
   - Count the number of islands in a 2D grid.  
   - **Key Concept**: Use a queue for BFS to mark visited cells.

---

#### **Hard Level**
9. **Shortest Path in a Binary Matrix**  
   - Find the shortest path from the top-left to the bottom-right of a binary matrix.  
   - **Key Concept**: Use BFS with a queue to explore all possible paths.

10. **Design Hit Counter**  
    - Implement a hit counter that tracks hits received in the past 5 minutes.  
    - **Key Concept**: Use a queue to store timestamps of hits.

11. **First Non-Repeating Character in a Stream**  
    - Find the first non-repeating character in a stream of characters.  
    - **Key Concept**: Use a queue to track character order and a hash map for frequency.

12. **Snake and Ladder Problem**  
    - Find the minimum number of dice throws required to reach the last square in a board game.  
    - **Key Concept**: Use a queue for BFS on the game board.

---

### **Bonus Problems Combining Stacks and Queues**
1. **Implement Deque (Double-Ended Queue)**  
   - Implement a deque that supports operations at both ends.  
   - **Key Concept**: Combine stack and queue functionality.

2. **Design Browser History**  
   - Simulate browser forward and backward navigation.  
   - **Key Concept**: Use two stacks to track history.

3. **Serialize and Deserialize Binary Tree**  
   - Serialize and deserialize a binary tree into a string representation.  
   - **Key Concept**: Use a queue for BFS serialization.

---

### **Tips for Stack and Queue Problems**
1. **Understand Basic Operations**: Know how `push`, `pop`, `enqueue`, and `dequeue` work for both arrays and linked lists.
2. **Know Variants**: Familiarize yourself with deque, priority queues, and circular queues.
3. **Edge Cases**: Handle empty stacks/queues and full circular queues carefully.
4. **Use for BFS/DFS**: Apply queues for BFS and stacks for DFS in graph/tree problems.

Let me know if you'd like detailed explanations or solutions for any of these problems!

## Give good problems that require using Monotonic Stacks/Queues. ##
Monotonic stacks and queues are powerful data structures used to solve problems where you need to track elements in a specific order (either non-increasing or non-decreasing) efficiently. These structures are often used to solve problems that involve finding the "next greater" or "previous smaller" elements in sequences. Below is a list of excellent problems that specifically require the use of monotonic stacks and queues:

---

### **Monotonic Stack Problems**

#### **Easy Level**
1. **Valid Parentheses**  
   - Given a string containing just the characters `'('`, `')'`, `{`, `}`, `[`, `]`, determine if the input string is valid.
   - **Key Concept**: Use a stack to ensure that every opening parenthesis has a corresponding closing parenthesis in the correct order.
   
2. **Next Greater Element I**  
   - Given an array of numbers, find the next greater element for each element. If no such element exists, output `-1`.
   - **Key Concept**: Use a monotonic decreasing stack to track the next greater element for each number.

3. **Next Greater Element II**  
   - Similar to the previous problem, but for a circular array.
   - **Key Concept**: Use a stack to track the elements in decreasing order, but take into account the circular nature of the array.

4. **Daily Temperatures**  
   - Given an array of temperatures, for each day, return how many days you would have to wait until a warmer temperature. If no future days are warmer, return `0`.
   - **Key Concept**: Use a monotonic decreasing stack to keep track of the indices of temperatures and calculate the "next greater" temperature for each day.

5. **Trapping Rain Water**  
   - Given an array representing the height of bars in a histogram, calculate how much water can be trapped between them.
   - **Key Concept**: Use two monotonic stacks (one for left boundaries and one for right boundaries) to calculate the trapped water at each point.

---

#### **Medium Level**
6. **Largest Rectangle in Histogram**  
   - Find the largest rectangle that can be formed in a histogram.
   - **Key Concept**: Use a monotonic stack to store indices in increasing order of heights. When a smaller height is encountered, calculate the largest rectangle that can be formed with the heights in the stack.

7. **Remove Duplicate Letters**  
   - Given a string, remove duplicate letters so that every letter appears once and only once, and the remaining letters are in the same order as the original string.
   - **Key Concept**: Use a monotonic stack to maintain the lexicographical order while removing duplicates.

8. **Maximal Rectangle**  
   - Given a 2D matrix containing only `0` and `1`, find the area of the largest rectangle containing only `1`'s.
   - **Key Concept**: Treat each row as a histogram and apply the "largest rectangle in histogram" problem using a monotonic stack.

9. **Sum of Subarray Minimums**  
   - Given an array of integers, find the sum of the minimum element in every subarray of the array.
   - **Key Concept**: Use a monotonic stack to efficiently track and calculate the minimum of all subarrays.

10. **Find the Right Interval**  
    - Given a list of intervals, find for each interval the interval that starts after it ends. If no such interval exists, return `-1`.
    - **Key Concept**: Use a monotonic stack to maintain intervals in increasing order.

---

#### **Hard Level**
11. **Sliding Window Maximum**  
    - Given an array and an integer `k`, find the maximum value in each sliding window of size `k`.
    - **Key Concept**: Use a monotonic deque (queue) to track the maximum value in the current window.

12. **Longest Valid Parentheses**  
    - Given a string containing just `'('` and `')'`, find the length of the longest valid parentheses substring.
    - **Key Concept**: Use a stack to track the indices of unmatched parentheses and calculate the length of the valid substring.

13. **Largest Rectangle in Binary Matrix**  
    - Given a binary matrix filled with `0` and `1`, find the largest rectangle containing only `1`'s.
    - **Key Concept**: Use dynamic programming and a monotonic stack to calculate the largest rectangle in each row, treating it as a histogram.

14. **Maximal Rectangle**  
    - Given a 2D matrix filled with `1` and `0`, find the maximal rectangle formed by `1`'s.
    - **Key Concept**: Similar to the "largest rectangle in histogram" problem, but applied to 2D grids.

---

### **Monotonic Queue Problems**

#### **Easy Level**
1. **Sliding Window Minimum**  
   - Given an array of integers and an integer `k`, find the minimum value in each sliding window of size `k`.
   - **Key Concept**: Use a monotonic deque (queue) to efficiently find the minimum in each sliding window.

2. **First Non-Repeating Character in a Stream**  
   - Given a stream of characters, find the first non-repeating character in the stream at each point.
   - **Key Concept**: Use a monotonic queue to track characters that appear more than once and return the first non-repeating character at each step.

---

#### **Medium Level**
3. **Maximum of All Subarrays of Size K**  
   - Given an array and a number `k`, find the maximum element in each subarray of size `k`.
   - **Key Concept**: Use a monotonic deque to track the maximum values in the current window.

4. **Smallest Subarray with a Given Sum**  
   - Given an array and a target sum, find the length of the smallest subarray whose sum is greater than or equal to the target.
   - **Key Concept**: Use a sliding window approach with a monotonic queue to track the subarrays.

5. **Sliding Window Average**  
   - Given an array and an integer `k`, find the average of each sliding window of size `k`.
   - **Key Concept**: Use a monotonic queue to maintain the sum of the current window and compute the average efficiently.

---

### **Tips for Using Monotonic Stacks/Queues**
1. **Monotonic Property**: Ensure that the stack or queue is ordered (either increasing or decreasing) at all times.
2. **Efficient Updates**: Monotonic stacks and queues allow you to maintain order and update efficiently, making them ideal for problems that require processing sequences in order.
3. **Edge Cases**: Always check for edge cases, such as empty arrays, no valid answers, or arrays with only one element.

Let me know if you'd like detailed explanations, code samples, or solutions for any of these problems!

## Give good Circular Queue problems. ##
Circular queues are a type of queue in which the last position is connected to the first position to make the structure circular. They are especially useful for buffering, managing limited resources, or handling tasks in a continuous loop, like in round-robin scheduling. Below are several problems that require or can benefit from the use of a circular queue:

---

### **Circular Queue Problems**

#### **Easy Level**

1. **Implement Circular Queue**  
   - Implement a circular queue using arrays or a linked list with basic operations: `enqueue`, `dequeue`, `peek`, `isEmpty`, and `isFull`.
   - **Key Concept**: Maintain two pointers (`front` and `rear`) and use modulo arithmetic to make the queue circular.

2. **Circular Queue – Moving Average**  
   - Given a stream of integers and a window size `k`, design a data structure that supports the computation of the moving average of the last `k` numbers in constant time.
   - **Key Concept**: Use a circular queue to keep track of the last `k` numbers and compute their average.

3. **Queue Using Two Stacks (with Circular Behavior)**  
   - Implement a queue using two stacks where one stack handles `enqueue` and the other handles `dequeue` operations, with behavior resembling a circular queue for efficient space usage.
   - **Key Concept**: Design the stacks such that the "circular" part is ensured by shifting the data when required.

---

#### **Medium Level**

4. **Circular Queue – Printer Simulation**  
   - Simulate a printer queue using a circular queue. Print jobs are added to the queue, and jobs are processed one by one. If a new job is added before the previous one finishes, it goes to the back of the queue.
   - **Key Concept**: Use a circular queue to model the printer buffer where jobs are processed in a round-robin fashion.

5. **Design a Circular Buffer**  
   - Design a circular buffer to hold `n` data elements. Implement functions to read from the buffer, write to the buffer, and handle overflow (wrap-around behavior).
   - **Key Concept**: Use a circular queue to efficiently manage the buffer and handle overflow and underflow situations.

6. **Multithreaded Circular Queue for Producer-Consumer Problem**  
   - Implement a circular queue to solve the producer-consumer problem. A producer adds items to the queue, and a consumer removes them. The queue must handle concurrent access safely (multithreading).
   - **Key Concept**: Use a circular queue to manage shared resources between multiple threads, and use synchronization mechanisms (locks/semaphores).

7. **Design Circular Queue with Dynamic Size Adjustment**  
   - Design a circular queue that can dynamically resize itself as it approaches full capacity. When the queue is full, it doubles in size. When it’s less than a quarter full, it shrinks.
   - **Key Concept**: Use circular queue logic with dynamic array resizing when needed for more efficient space utilization.

---

#### **Hard Level**

8. **Circular Queue – Task Scheduler**  
   - Simulate a task scheduler using a circular queue, where each task has a fixed time slice for execution. After executing for the time slice, tasks are re-enqueued if they are not finished.
   - **Key Concept**: Use a circular queue to manage tasks, keeping track of the remaining time for each task. Tasks are executed in a round-robin fashion.

9. **Circular Queue with Priority**  
   - Implement a priority circular queue where elements are enqueued with a priority value. Elements with higher priority are dequeued first, but the queue should be circular.
   - **Key Concept**: Implement priority queue logic inside a circular queue structure.

10. **Circular Queue for Rate Limiting (Token Bucket Algorithm)**  
    - Implement the token bucket algorithm using a circular queue. In this problem, tokens are added to the queue at a fixed rate, and when a request comes in, a token is consumed if available. If no tokens are available, the request is denied.
    - **Key Concept**: Use a circular queue to model the token bucket, ensuring that tokens are added and removed in a circular fashion.

11. **Circular Queue for Data Stream Processing**  
    - Design a circular queue to handle large data streams where elements come in continuously. The queue should store the most recent `n` elements from the stream while discarding older elements.
    - **Key Concept**: Use the circular queue to maintain only the most recent `n` elements in memory, implementing a sliding window of the stream.

---

#### **Bonus Problems:**

12. **Circular Queue with Linked List Implementation**  
    - Implement a circular queue using a doubly linked list where each node has both a `next` and `prev` pointer, and the first and last nodes are connected in a circular manner.
    - **Key Concept**: Design the circular queue structure with a doubly linked list where the `next` pointer of the last node points to the first, and the `prev` pointer of the first node points to the last.

13. **Circular Queue for Traffic Simulation**  
    - Simulate a traffic system with a circular queue, where cars are waiting at a traffic light. After a fixed time, cars move forward to the intersection, and new cars enter the queue. The queue should model the behavior of cars approaching the light.
    - **Key Concept**: Model cars waiting at the light in a circular queue, ensuring cars move in a round-robin fashion based on time constraints.

---

### **Key Concepts and Tips for Circular Queue Problems:**
1. **Wrap Around**: In a circular queue, when the `rear` reaches the end of the array, it should wrap around to the beginning of the array (modulo arithmetic).
2. **Overflow and Underflow**: Always handle cases where the queue is full (overflow) or empty (underflow).
3. **Efficient Space Management**: Circular queues are efficient in terms of space utilization since they allow for constant-time insertions and deletions.
4. **Dynamic Resizing**: For advanced problems, you may need to implement dynamic resizing to handle larger queues efficiently as data grows.

Let me know if you'd like detailed solutions or code for any of these problems!

## Give more good problems like Next Greater Element, and Stock Span Problem. ##
Here are some excellent problems that are similar to the **Next Greater Element (NGE)** and **Stock Span Problem**, typically involving **monotonic stacks**, **range queries**, or **sequential processing** of arrays. These problems require you to efficiently find the "next" or "previous" larger/smaller element in an array, often using stacks for optimal time complexity:

---

### **Problems Similar to "Next Greater Element" (NGE) and "Stock Span Problem"**

#### **Easy Level**
1. **Next Smaller Element**  
   - Given an array of integers, for each element, find the next smaller element (to the right of the current element). If no smaller element exists, return `-1`.
   - **Key Concept**: Use a monotonic stack to track elements and find the next smaller element efficiently.
   
2. **Previous Greater Element**  
   - Given an array, for each element, find the previous greater element (to the left of the current element). If no greater element exists, return `-1`.
   - **Key Concept**: Use a stack to keep track of the previous greater elements while iterating from left to right.

3. **Previous Smaller Element**  
   - Given an array, for each element, find the previous smaller element (to the left of the current element). If no smaller element exists, return `-1`.
   - **Key Concept**: Use a stack to keep track of previous smaller elements as you iterate through the array.

4. **Temperature Problem**  
   - Given a list of temperatures, for each day, find how many days until a warmer temperature. If no warmer temperature exists, return `0`.
   - **Key Concept**: Use a monotonic stack to maintain indices of temperatures and calculate the number of days until a warmer temperature for each day.

5. **Daily Stock Price Change**  
   - Given a list of daily stock prices, for each day, determine how many days it takes for the price to go higher than today's price. If it never goes higher, return `-1`.
   - **Key Concept**: Use a stack to track the price indices and compute the number of days for price increases.

---

#### **Medium Level**
6. **Next Greater Element II**  
   - This problem is an extension of the "Next Greater Element" problem where the input is a **circular array**. For each element, find the next greater element in the array.
   - **Key Concept**: Use a monotonic stack with a circular array and wrap around to the beginning of the array.

7. **Stock Buy and Sell to Maximize Profit**  
   - Given a list of stock prices, find the maximum profit you can achieve by buying and selling a stock. You can make as many transactions as needed (but must buy before you sell).
   - **Key Concept**: Use a stack or dynamic programming to track the maximum possible profit with multiple buy/sell operations.

8. **Largest Rectangle in Histogram**  
   - Given an array representing the heights of a histogram's bars, find the area of the largest rectangle that can be formed in the histogram.
   - **Key Concept**: Use a stack to efficiently find the largest possible rectangle by processing bars in a monotonic order.

9. **Next Greater Element with Duplicate Values**  
   - Given an array with duplicate elements, find the next greater element for each element in the array. If no such element exists, return `-1`.
   - **Key Concept**: Use a stack to process elements in a non-decreasing manner, considering duplicates.

10. **Find All Elements Greater Than Current in Array**  
    - Given an array, return an array where each element is replaced by the count of elements that are greater than it.
    - **Key Concept**: Use a sorted stack to count the number of elements greater than each element in a single pass.

---

#### **Hard Level**
11. **Largest Rectangle in Binary Matrix**  
    - Given a binary matrix (consisting of `1`s and `0`s), find the largest rectangle containing only `1`s.
    - **Key Concept**: Treat each row as a histogram of consecutive `1`s, and use a monotonic stack to find the largest rectangle in the histogram for each row.

12. **Trapping Rain Water**  
    - Given an array representing the elevation of bars in a histogram, compute how much water can be trapped between them.
    - **Key Concept**: Use two stacks (or two pointers) to calculate the trapped water for each element in the array.

13. **Sliding Window Maximum**  
    - Given an array and an integer `k`, find the maximum value in each sliding window of size `k`.
    - **Key Concept**: Use a monotonic deque (double-ended queue) to track the maximum value in the current window as the window slides.

14. **Sum of Subarray Minimums**  
    - Given an array of integers, compute the sum of the minimum element of all subarrays of the array.
    - **Key Concept**: Use a monotonic stack to track the minimum elements of subarrays and compute the sum efficiently.

15. **Maximal Rectangle**  
    - Given a binary matrix of `1`s and `0`s, find the area of the largest rectangle that can be formed in the matrix.
    - **Key Concept**: Convert each row into a histogram, and use a monotonic stack to find the largest rectangle in the histogram for each row.

---

#### **Bonus Problems**
16. **Maximal Square**  
    - Given a 2D matrix containing only `0`s and `1`s, find the size of the largest square that can be formed by only `1`s.
    - **Key Concept**: Use dynamic programming combined with a monotonic stack to find the maximum size of a square that can be formed at each cell.

17. **Next Greater Element to Right of Each Element in Array**  
    - Given an array of integers, for each element, find the next greater element that is strictly greater and is located to the right of the current element.
    - **Key Concept**: Use a monotonic stack to store indices and find the next greater element for each index in the array.

18. **Remove Duplicate Letters**  
    - Given a string, remove duplicate letters while maintaining the lexicographical order and ensuring that the remaining letters are in the same order as the original string.
    - **Key Concept**: Use a stack to maintain the lexicographical order of letters while removing duplicates.

19. **Evaluate Reverse Polish Notation**  
    - Evaluate a given arithmetic expression in **Reverse Polish Notation**.
    - **Key Concept**: Use a stack to evaluate the postfix expression by pushing operands and performing operations when operators are encountered.

20. **Asteroid Collision**  
    - Given an array of asteroids, where positive integers represent asteroids moving to the right and negative integers represent asteroids moving to the left, determine the resulting state of the asteroids after all collisions.
    - **Key Concept**: Use a stack to simulate asteroid movement and handle collisions between asteroids moving in opposite directions.

---

### **Key Concepts for Solving These Problems**
- **Monotonic Stacks**: Use stacks that maintain a specific order (increasing or decreasing) to process elements efficiently.
- **Efficient Queries**: Many of these problems involve finding the next or previous greater or smaller element in a sequence, which can be done efficiently using stacks.
- **Sliding Window**: Sliding window problems often require maintaining a state (e.g., maximum, minimum) over a fixed-size window, which can be handled efficiently using monotonic queues or stacks.

Let me know if you'd like solutions or explanations for any of these problems!

## Give good problems requiring Hash Maps, and Hash Sets. ##
Hash maps (also known as hash tables) and hash sets are extremely efficient data structures for solving problems that involve looking up, inserting, and deleting elements quickly. Hash maps allow for fast key-value pair lookups, while hash sets are useful for fast membership checks and eliminating duplicates.

Here are some great problems that require or can benefit from using **Hash Maps** and **Hash Sets**:

---

### **Problems Requiring Hash Maps**

#### **Easy Level**

1. **Two Sum**  
   - Given an array of integers and a target sum, find two numbers that add up to the target. Return their indices.
   - **Key Concept**: Use a hash map to store the difference between the target and each number, and check if the current number exists in the hash map.

2. **First Unique Character in a String**  
   - Given a string, find the first non-repeating character in it and return its index. If it doesn’t exist, return `-1`.
   - **Key Concept**: Use a hash map to count the frequency of each character and then iterate through the string to find the first unique character.

3. **Group Anagrams**  
   - Given a list of strings, group the anagrams together. You can return the groups in any order.
   - **Key Concept**: Use a hash map to store the sorted version of each string as the key and the list of anagrams as the value.

4. **Check if a Subarray Sum Equals K**  
   - Given an array of integers and a target sum `k`, determine if there is a subarray of length at least 2 that sums up to `k`.
   - **Key Concept**: Use a hash map to store the cumulative sum up to each index and check if the difference between the current cumulative sum and `k` is in the map.

5. **Find the Difference of Two Arrays**  
   - Given two arrays, find the elements present in the first array but not in the second, and vice versa.
   - **Key Concept**: Use hash sets to find the difference between the two arrays efficiently.

---

#### **Medium Level**

6. **Longest Substring Without Repeating Characters**  
   - Given a string, find the length of the longest substring without repeating characters.
   - **Key Concept**: Use a hash map to store the last occurrence of each character and use a sliding window approach to track the longest substring.

7. **Subarray Sum Equals K**  
   - Given an array of integers and a sum `k`, find the total number of continuous subarrays whose sum equals `k`.
   - **Key Concept**: Use a hash map to store the cumulative sum at each index and check how many times `sum - k` has been encountered.

8. **Top K Frequent Elements**  
   - Given a non-empty array of integers, return the `k` most frequent elements.
   - **Key Concept**: Use a hash map to count the frequency of elements and then use a priority queue or sorting to find the top `k` frequent elements.

9. **Isomorphic Strings**  
   - Given two strings, check if they are isomorphic. Two strings are isomorphic if each character in the first string can be replaced with a corresponding character in the second string to get the second string.
   - **Key Concept**: Use two hash maps to store the mapping of characters between the two strings.

10. **Find All Pairs with a Given Difference**  
    - Given an array of integers and a target difference `k`, find all pairs of numbers such that their difference is `k`.
    - **Key Concept**: Use a hash map to track the elements and check if the current element plus `k` or minus `k` exists in the map.

---

#### **Hard Level**

11. **Longest Substring with At Most K Distinct Characters**  
    - Given a string and an integer `k`, find the length of the longest substring that contains at most `k` distinct characters.
    - **Key Concept**: Use a sliding window and a hash map to count the occurrences of characters in the current window.

12. **Word Pattern**  
    - Given a string `pattern` and a string `str`, check if `str` follows the same pattern as `pattern`.
    - **Key Concept**: Use two hash maps to track the mapping of characters from the pattern to the string and vice versa.

13. **Find All Anagram Substrings in a String**  
    - Given a string `s` and a string `p`, find all the start indices of `p`'s anagrams in `s`.
    - **Key Concept**: Use a hash map to store the character frequencies of `p` and a sliding window to check if the substring of `s` is an anagram of `p`.

14. **Happy Number**  
    - A happy number is defined by the following process: starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals `1` (where it will stay), or it loops endlessly in a cycle that does not include `1`. Determine if a number is happy.
    - **Key Concept**: Use a hash set to track the numbers encountered during the process to detect a cycle.

15. **Subarray Product Less Than K**  
    - Given an array of positive integers `nums` and a positive integer `k`, find the number of contiguous subarrays whose product is strictly less than `k`.
    - **Key Concept**: Use a sliding window approach and a hash map to maintain the product of elements in the window.

---

### **Problems Requiring Hash Sets**

#### **Easy Level**

1. **Intersection of Two Arrays**  
   - Given two arrays, find the intersection of these arrays. Return an array with the common elements.
   - **Key Concept**: Use hash sets to store the elements of one array and check if elements of the second array are in the set.

2. **Contains Duplicate**  
   - Given an array of integers, return `true` if any value appears at least twice in the array, and `false` if every element is distinct.
   - **Key Concept**: Use a hash set to track the elements as you iterate through the array, and check for duplicates.

3. **Single Number**  
   - Given an array of integers, every element appears twice except for one. Find that single one.
   - **Key Concept**: Use a hash set to track the elements that have appeared. If an element appears again, remove it from the set; the remaining element is the single number.

4. **Find the Duplicates in an Array**  
   - Given an array of integers, find all the elements that appear more than once in the array.
   - **Key Concept**: Use a hash set to track the elements as you iterate through the array and store duplicates.

5. **Happy Number**  
   - A number is happy if it eventually reaches `1` when replaced by the sum of the squares of its digits. Use a hash set to detect cycles during the process.
   - **Key Concept**: Track the numbers encountered during the calculation to detect cycles using a hash set.

---

#### **Medium Level**

6. **Find the Missing Number**  
   - Given an array of `n` integers in the range from `1` to `n + 1`, find the missing number in the array.
   - **Key Concept**: Use a hash set to track the elements and check which number is missing.

7. **Unique Paths**  
   - Given a 2D grid, find the number of unique paths from the top-left corner to the bottom-right corner, moving only down or right.
   - **Key Concept**: Use a hash set to track the visited paths.

8. **Longest Consecutive Sequence**  
   - Given an unsorted array of integers, find the length of the longest consecutive elements sequence.
   - **Key Concept**: Use a hash set to efficiently check for consecutive sequences.

---

#### **Hard Level**

9. **Find the Kth Largest Element in an Array**  
   - Given an array, find the `k`th largest element.
   - **Key Concept**: Use a hash set or priority queue to find the largest `k` elements and return the `k`th largest.

10. **Longest Repeating Character Replacement**  
    - Given a string and an integer `k`, you can replace at most `k` characters in the string to make all the characters in the string the same. Find the length of the longest substring that can be obtained.
    - **Key Concept**: Use a sliding window approach and a hash map to track the character counts.

---

### **Key Concepts**
- **Hash Maps**: Used to store key-value pairs and allow for efficient lookups, insertions, and deletions. They are essential for counting occurrences, tracking unique elements, and solving problems involving frequency or mapping.
- **Hash Sets**: Provide efficient membership checks and are used to store unique elements, making them ideal for problems involving duplicates, uniqueness, or set operations like intersection, union, and difference.

Let me know if you'd like solutions or further explanations for any of these problems!

## Give good Collision Handling problems. ##
Collision handling in the context of **hashing** and **hash maps** is crucial when multiple keys hash to the same index in the hash table. There are several techniques for handling collisions, such as **chaining** (using linked lists or other data structures at each index) and **open addressing** (where the next available slot is searched for). Below are some excellent problems related to collision handling:

---

### **Good Problems Related to Collision Handling**

#### **Easy Level**

1. **Implement a Hash Map**  
   - **Problem**: Implement a simple hash map with basic operations such as `put(key, value)`, `get(key)`, and `remove(key)`. Handle collisions using **chaining** (using linked lists or arrays for each index).
   - **Key Concept**: You will need to handle hash collisions by maintaining linked lists (or arrays) at each bucket in the hash table.

2. **Design a Hash Set**  
   - **Problem**: Design a hash set, which supports `add(value)`, `contains(value)`, and `remove(value)` methods. Implement collision handling via **separate chaining** (or open addressing).
   - **Key Concept**: Similar to the hash map problem but only storing values (not key-value pairs). Focus on handling collisions when values are added, removed, or searched.

3. **Check for Duplicates Using a Hash Map**  
   - **Problem**: Given an array of integers, find out if there are any duplicates in the array using a hash map. Handle collisions while storing values in the hash map.
   - **Key Concept**: This problem involves handling potential collisions while checking if the element has already been inserted into the hash map.

4. **Find First Repeating Element**  
   - **Problem**: Given an array of integers, find the first repeating element. If no element repeats, return `-1`. Use a hash map to store the elements and handle collisions appropriately.
   - **Key Concept**: As you traverse the array, store each element in a hash map. Handle collisions and ensure that the first repeat is found.

---

#### **Medium Level**

5. **Design a HashMap with Open Addressing**  
   - **Problem**: Design a hash map that uses **open addressing** for collision resolution. Implement methods like `put(key, value)`, `get(key)`, and `remove(key)`.
   - **Key Concept**: Handle collisions by probing for the next available slot (linear probing, quadratic probing, or double hashing).

6. **Design a Hash Table with Chaining**  
   - **Problem**: Implement a hash table where each bucket stores a linked list (for handling collisions via chaining). You need to implement the basic operations like `insert()`, `delete()`, and `search()`.
   - **Key Concept**: Focus on chaining to handle multiple elements that hash to the same index.

7. **Count Distinct Elements Using a Hash Set**  
   - **Problem**: Given an array of integers, count the number of distinct elements. Handle collisions when storing the elements in a hash set.
   - **Key Concept**: Use a hash set to keep track of the unique elements, and ensure that collisions are handled during insertion.

8. **Longest Substring Without Repeating Characters**  
   - **Problem**: Given a string, find the length of the longest substring without repeating characters. Use a sliding window and a hash map for efficient collision handling while maintaining the character counts.
   - **Key Concept**: Use a hash map to store the indices of characters and handle collisions when the character appears again.

9. **Design a LRU Cache**  
   - **Problem**: Design a **Least Recently Used (LRU)** cache that supports `get(key)` and `put(key, value)` operations. Implement collision handling in the underlying hash map.
   - **Key Concept**: You need to handle collisions while ensuring that the cache evicts the least recently used item efficiently.

---

#### **Hard Level**

10. **Implement a HashMap with Collision Resolution via Double Hashing**  
    - **Problem**: Implement a hash map that resolves collisions using **double hashing** (i.e., using two hash functions to calculate the index for a key). Implement `put()`, `get()`, and `remove()` methods.
    - **Key Concept**: Double hashing is an open addressing collision resolution technique where two hash functions are used. Focus on handling collisions efficiently in a constrained space.

11. **Design a Hash Set with Open Addressing**  
    - **Problem**: Design a hash set that uses **open addressing** (e.g., quadratic probing or double hashing) for collision resolution.
    - **Key Concept**: Handle collisions efficiently by probing for the next open slot, and make sure the hash set functions well under load.

12. **Count Unique Words in a Document**  
    - **Problem**: Given a large document (string), count how many times each word appears. You need to handle collisions while mapping each word to its frequency.
    - **Key Concept**: Use a hash map to store word frequencies, and handle collisions efficiently when two words hash to the same bucket.

13. **Longest Substring with K Distinct Characters**  
    - **Problem**: Given a string and an integer `k`, find the length of the longest substring that contains at most `k` distinct characters. Handle collisions when storing the character counts.
    - **Key Concept**: Use a sliding window technique and a hash map to count the frequency of characters. Collisions occur when the frequency of a character needs to be updated.

14. **Find Anagram Mappings**  
    - **Problem**: Given two arrays, find a mapping of elements from one array to the other (e.g., find indices in the second array that match elements in the first). Ensure collision handling while mapping elements.
    - **Key Concept**: Handle collisions when elements from the two arrays have the same value but are at different indices.

15. **Hash Function Collision Analysis**  
    - **Problem**: Given an array of integers, evaluate the efficiency of a hash function by analyzing the number of collisions it generates. Determine how many collisions occur for a given set of inputs.
    - **Key Concept**: This problem involves understanding how hash functions work, and how different strategies for collision handling (e.g., chaining vs open addressing) affect the overall performance.

---

### **Key Concepts for Collision Handling**
- **Chaining**: Using a secondary data structure (like a linked list) at each index to store multiple elements that hash to the same index.
- **Open Addressing**: Finding the next available index within the hash table (using methods like linear probing, quadratic probing, or double hashing) to resolve collisions.
- **Load Factor**: A measure of how full a hash table is. A high load factor can lead to more collisions, so managing the load factor is essential to prevent excessive collisions.
- **Rehashing**: When the load factor exceeds a certain threshold, rehashing involves resizing the hash table and re-inserting the elements to reduce collisions.

---

Let me know if you'd like solutions, explanations, or additional resources on any of these problems!

## Give good Anagram Grouping problems for FAANG interviews. ##
Here are **anagram grouping problems tailored for FAANG interviews**. These problems are designed to test your ability to efficiently manipulate strings, use data structures, and optimize for time and space complexity.

---

### 1. **Classic Group Anagrams**  
**Problem:**  
Given an array of strings, group the strings that are anagrams of each other.  

**Constraints:**  
1. Optimize for both time and space complexity.
2. Handle edge cases like empty strings or single-character strings.

**Example:**  
Input: `["eat", "tea", "tan", "ate", "nat", "bat"]`  
Output: `[["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]`

**Key Concepts:**  
Hashing, sorting, dictionary usage.

---

### 2. **Find Anagram Pairs in a List**  
**Problem:**  
Given an array of strings, count the number of pairs of strings that are anagrams of each other.  

**Constraints:**  
1. Return only the count of pairs, not the pairs themselves.
2. Aim for linear or near-linear time complexity.  

**Example:**  
Input: `["listen", "silent", "enlist", "abc", "bca", "cab"]`  
Output: `6`  
Explanation: Pairs are `(listen, silent), (listen, enlist), (silent, enlist), (abc, bca), (abc, cab), (bca, cab)`.

**Key Concepts:**  
Hashing, counting character frequencies.

---

### 3. **Anagram Subarray Groups**  
**Problem:**  
Given an array of strings, find the largest subarray where all strings are anagrams of each other.  

**Constraints:**  
1. Subarray must be contiguous.  
2. Return the start and end indices of the subarray.  

**Example:**  
Input: `["abc", "bca", "cab", "xyz", "yxz", "zxy"]`  
Output: `(0, 2)`  
Explanation: The largest contiguous subarray of anagrams is `["abc", "bca", "cab"]`.

**Key Concepts:**  
Sliding window, hash maps.

---

### 4. **Find All Anagrams of a Target String in a List**  
**Problem:**  
Given a target string and a list of words, return all words in the list that are anagrams of the target.  

**Constraints:**  
1. Target string is fixed, while the list size can be large.
2. Case-insensitive comparison.  

**Example:**  
Input: `words = ["enlist", "google", "inlets", "banana", "silent"]`, `target = "listen"`  
Output: `["enlist", "inlets", "silent"]`

**Key Concepts:**  
Efficient comparison using sorted strings or character frequency counts.

---

### 5. **Count Anagrammatic Pairs in a String**  
**Problem:**  
Given a single string, count the number of pairs of substrings that are anagrams of each other.  

**Constraints:**  
1. Optimize to avoid generating all substrings explicitly.
2. Handle strings with repeated characters.  

**Example:**  
Input: `"abba"`  
Output: `4`  
Explanation: The pairs are `("a", "a"), ("b", "b"), ("ab", "ba"), ("abb", "bba")`.

**Key Concepts:**  
Frequency hash map, combinatorics.

---

### 6. **K-Anagram Grouping**  
**Problem:**  
Two strings are called **K-anagrams** if you can replace at most `K` characters in one string to make it an anagram of the other. Group all `K-anagrams` in a list.  

**Constraints:**  
1. Handle cases with large `K` and long strings.
2. Group strings that are identical under the K-anagram rule.  

**Example:**  
Input: `words = ["anagram", "mangaar", "grammar", "rangama"]`, `K = 2`  
Output: `[["anagram", "mangaar", "rangama"], ["grammar"]]`

**Key Concepts:**  
Dynamic programming, hash map optimization.

---

### 7. **Anagram Palindrome Groups**  
**Problem:**  
Group strings that can form palindromes when rearranged.  

**Constraints:**  
1. A string can form a palindrome if at most one character has an odd frequency.  
2. Return grouped strings.  

**Example:**  
Input: `["civic", "ivicc", "hello", "oellh", "banana"]`  
Output: `[["civic", "ivicc"], ["hello", "oellh"], ["banana"]]`

**Key Concepts:**  
Character frequency analysis.

---

### 8. **Largest Anagram Group Size**  
**Problem:**  
Find the size of the largest group of anagrams in a list of strings.  

**Constraints:**  
1. Return only the size, not the group itself.
2. Handle large input arrays efficiently.  

**Example:**  
Input: `["rat", "tar", "art", "cat", "act", "bat"]`  
Output: `3`  
Explanation: The largest anagram group is `["rat", "tar", "art"]`.

**Key Concepts:**  
Hashing, sorting.

---

### 9. **Transform to Anagrams with Minimum Swaps**  
**Problem:**  
Given two strings of equal length, find the minimum number of adjacent swaps required to transform one string into an anagram of the other.  

**Constraints:**  
1. Both strings contain the same characters in different orders.  
2. Optimize for both time and space complexity.  

**Example:**  
Input: `str1 = "abcd"`, `str2 = "dcba"`  
Output: `4`

**Key Concepts:**  
Greedy algorithms, two-pointer techniques.

---

### 10. **Real-Time Anagram Groups**  
**Problem:**  
Design a system to group anagrams in real-time as new words are streamed in.  

**Constraints:**  
1. Maintain a dynamic data structure to update groups on the fly.
2. Optimize for insertion and query efficiency.  

**Example:**  
Input: Stream of words: `"tea"`, `"eat"`, `"bat"`, `"ate"`, `"tab"`, `"cat"`.  
Output after processing:  
`[["tea", "eat", "ate"], ["bat", "tab"], ["cat"]]`

**Key Concepts:**  
Dynamic hash maps, streaming algorithms.

---

These problems will challenge candidates to think critically about efficient data structures, algorithm design, and edge case handling—skills essential for FAANG-level interviews.

## Give good Two-Sum and related problems for FAANG interviews. ##

Here’s a list of **Two-Sum and related problems** tailored for FAANG interviews. These problems emphasize mastery of hash maps, sorting, and two-pointer techniques.

---

### 1. **Classic Two-Sum**  
**Problem:**  
Given an array of integers `nums` and a target integer `target`, return the indices of the two numbers that add up to the target.  

**Constraints:**  
1. Assume exactly one solution exists.  
2. Optimize for time complexity.  

**Example:**  
Input: `nums = [2, 7, 11, 15], target = 9`  
Output: `[0, 1]`

**Key Concepts:**  
Hash map for O(n) time complexity.

---

### 2. **Two-Sum with Duplicates**  
**Problem:**  
Given an array of integers, find all unique pairs of numbers that sum to the target.  

**Constraints:**  
1. Return pairs, not indices.  
2. Avoid duplicate pairs in the output.  

**Example:**  
Input: `nums = [2, 7, 11, 15, 2, -2], target = 9`  
Output: `[[2, 7]]`

**Key Concepts:**  
Set or sorting with two-pointer technique.

---

### 3. **Two-Sum for Sorted Array**  
**Problem:**  
Given a sorted array of integers, return the indices of the two numbers that add up to the target.  

**Constraints:**  
1. Solve in O(n) time using the two-pointer technique.  

**Example:**  
Input: `nums = [2, 3, 4, 6], target = 6`  
Output: `[0, 2]`

**Key Concepts:**  
Two-pointer approach.

---

### 4. **Two-Sum Closest to Target**  
**Problem:**  
Find two numbers in the array whose sum is closest to a given target.  

**Constraints:**  
1. Return the numbers, not indices.  
2. Handle edge cases with ties.  

**Example:**  
Input: `nums = [1, 2, 3, 4, 5], target = 8`  
Output: `[3, 5]`

**Key Concepts:**  
Sorting, two-pointer technique.

---

### 5. **Three-Sum**  
**Problem:**  
Given an array of integers, find all unique triplets that sum to zero.  

**Constraints:**  
1. Avoid duplicate triplets.  
2. Optimize for O(n²) time complexity.  

**Example:**  
Input: `nums = [-1, 0, 1, 2, -1, -4]`  
Output: `[[-1, -1, 2], [-1, 0, 1]]`

**Key Concepts:**  
Sorting and two-pointer technique.

---

### 6. **Four-Sum**  
**Problem:**  
Given an array of integers, find all unique quadruplets that sum to a target.  

**Constraints:**  
1. Avoid duplicate quadruplets.  
2. Optimize for O(n³) time complexity.  

**Example:**  
Input: `nums = [1, 0, -1, 0, -2, 2], target = 0`  
Output: `[[-2, -1, 1, 2], [-2, 0, 0, 2], [-1, 0, 0, 1]]`

**Key Concepts:**  
Sorting and k-sum generalization.

---

### 7. **K-Sum**  
**Problem:**  
Extend the Two-Sum problem to find `k` numbers in an array that add up to a target.  

**Constraints:**  
1. Optimize for higher dimensions using recursion.  

**Example:**  
Input: `nums = [1, 0, -1, 0, -2, 2], target = 0, k = 3`  
Output: `[[-2, 0, 2], [-1, 0, 1]]`

**Key Concepts:**  
Recursive backtracking with two-pointer optimization.

---

### 8. **Two-Sum with Multiples**  
**Problem:**  
Find all pairs of indices such that the two numbers add up to the target and allow using the same number multiple times.  

**Example:**  
Input: `nums = [2, 4, 6], target = 8`  
Output: `[[0, 1], [1, 1]]`

**Key Concepts:**  
Dynamic programming or nested iteration.

---

### 9. **Two-Sum in a Stream**  
**Problem:**  
Design a class that supports adding numbers and finding if any two numbers sum to a target.  

**Example:**  
```python
add(1)  
add(3)  
add(5)  
find(4) # True  
find(7) # False
```

**Key Concepts:**  
Hash map for efficient insertion and lookup.

---

### 10. **Subarray Two-Sum**  
**Problem:**  
Find the number of subarrays whose elements sum to a given target.  

**Constraints:**  
1. Subarrays must be contiguous.  

**Example:**  
Input: `nums = [1, 1, 1], target = 2`  
Output: `2`  
Explanation: Subarrays are `[1, 1]` and `[1, 1]`.

**Key Concepts:**  
Prefix sum with hash map.

---

### 11. **Two-Sum with Absolute Difference**  
**Problem:**  
Find all pairs of numbers with an absolute difference equal to a given value.  

**Example:**  
Input: `nums = [1, 5, 3, 4, 2], diff = 2`  
Output: `[[1, 3], [3, 5], [2, 4]]`

**Key Concepts:**  
Sorting and binary search or hash map.

---

### 12. **Weighted Two-Sum**  
**Problem:**  
Each number in the array has a weight. Find two numbers such that their weighted sum equals the target.  

**Example:**  
Input: `nums = [2, 3, 5], weights = [1, 2, 3], target = 11`  
Output: `[2, 5]` (2×1 + 5×3 = 11)

**Key Concepts:**  
Sorting, hash map.

---

### 13. **Two-Sum in BST**  
**Problem:**  
Given the root of a Binary Search Tree and a target, find if there are two numbers in the tree that sum to the target.  

**Constraints:**  
1. Solve without flattening the tree into an array.  

**Example:**  
Input: BST with nodes `[5, 3, 6, 2, 4, null, 7]`, target = 9  
Output: `True`

**Key Concepts:**  
In-order traversal with hash set.

---

### 14. **Two-Sum Modulo Problem**  
**Problem:**  
Find all pairs of numbers in the array whose sum modulo a given value equals a target remainder.  

**Example:**  
Input: `nums = [2, 3, 7, 11, 6], mod = 5, target = 2`  
Output: `[[2, 11], [3, 6]]`

**Key Concepts:**  
Hash map for modular arithmetic.

---

### 15. **Two-Sum for a Rotated Array**  
**Problem:**  
Given a rotated sorted array, find two numbers that sum to a target.  

**Constraints:**  
1. Solve in O(n) time.  

**Example:**  
Input: `nums = [6, 7, 8, 1, 2, 3], target = 9`  
Output: `[6, 3]`

**Key Concepts:**  
Modified two-pointer approach with rotation detection.

---

These problems cover a range of difficulties and techniques and are commonly asked at FAANG interviews to test problem-solving, optimization, and understanding of data structures.