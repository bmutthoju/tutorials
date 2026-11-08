## Functional Programming

lambda argument(s) : expression

```
greet = lambda : print('Hello World')

greet()
```

`map(function, iterable, ...)`

	1. `function` - a function
	2. `iterable` - iterable like sets, lists, tuples, etc.
	
`filter(function, iterable)`
	
	1. `function` - returns a boolean
	2. `iterable` - sets, lists, tuples, etc.
	
`reduce(function, iterable, initializer)`

	1. initializer: reduces iterable to a single value (optional)
	
```
add = lambda a, b : a + b

print(add(5, 10))
```

```
numbers = [2, 4, 8, 6, 8, 10]

square = lambda number : number ** 2

numbersSquare_list = list(map(square, numbers))
print(numbersSquare_list)

numbersSquare_list = list(map(lambda number : number ** 2, numbers))
print(numbersSquare_list)

numbersSquare_list = tuple(map(square, numbers))
print(numbersSquare_list)

numbersSquare_list = set(map(square, numbers))
print(numbersSquare_list)
```

```
scores = [66, 90, 68, 59, 76, 60, 88, 74, 81, 65]

filtered_scores = list(filter(lambda number : number > 75, scores))
print(filtered_scores)
```

```
from functools import reduce

result = reduce(lambda x, y : x + y, scores, 0)
print(result)
```

```
func = lambda a, b : a - b if a >= b else a * b
print(func(10, 2), func(34, 23)
```

```
numbers = [2, 4, 8, 6, 8, 10]

square = lambda number : number ** 2

numbersSquare_list = list(map(square, numbers))
print(numbersSquare_list)

numbersSquare_list = list(map(lambda number : number ** 2, numbers))
print(numbersSquare_list)

numbersSquare_list = tuple(map(square, numbers))
print(numbersSquare_list)

numbersSquare_list = set(map(square, numbers))
print(numbersSquare_list)
```

```
scores = [66, 90, 68, 59, 76, 60, 88, 74, 81, 65]

filtered_scores = list(filter(lambda number : number > 75, scores))
print(filtered_scores)
```

```
from functools import reduce

result = reduce(lambda x, y : x + y, scores, 0)
print(result)
```

```
numbers = range(10)

print(list(filter(lambda x : x % 2 == 0, numbers)))
```