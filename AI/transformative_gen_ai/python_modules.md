## Modules

Built-in: math, random, datetime, os, ...

Custom module:

`import module_name`

`module_name.function_name()`

```
import math

num = 16

print(math.sqrt(num))

```

scientific-computing tools:
numpy
scipi

```
import math

num = 4
print(math.factorial(4))

# General function
print(round(math.pi, 2))

print(round(math.sin(math.pi), 2))
print(math.ceil(num))
print(math.floor(num))
```

```
import random

num = random.randint(1, 5) # 5 is inclusive
print([random.randint(1, 5) for _ in range(5)]) # _ : We don't need it

print([random.choice([3, 4, 6, 10]) for _ in range(5)])
```

```
from math import sqrt, floor, ceil

# square root of a number
num = 16
print(sqrt(num))
print(floor(2.9))
```

```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import math_calculator as mc
```