## Give an exhaustive list of sorting algorithms. ##
Here is an exhaustive list of commonly used sorting algorithms:

1. **Bubble Sort**: Repeatedly swaps adjacent elements if they are in the wrong order until the entire list is sorted. It has a time complexity of O(n^2).
2. **Selection Sort**: Finds the minimum element from the unsorted part of the list and swaps it with the first unsorted element. It has a time complexity of O(n^2).
3. **Insertion Sort**: Builds the final sorted array one item at a time by repeatedly inserting the current element into the correct position within the sorted part of the array. It has a time complexity of O(n^2).
4. **Merge Sort**: Divides the unsorted list into smaller sublists, recursively sorts them, and then merges the sorted sublists to produce a final sorted list. It has a time complexity of O(n log n).
5. **Quick Sort**: Selects a pivot element and partitions the array such that all elements less than the pivot are placed before it, and all elements greater than the pivot are placed after it. It then recursively sorts the subarrays. It has an average time complexity of O(n log n) but can degrade to O(n^2) in the worst case.
6. **Heap Sort**: Builds a max heap from the input array and repeatedly extracts the maximum element (root of the heap) and places it at the end of the array. It has a time complexity of O(n log n).
7. **Counting Sort**: Suitable for sorting integers with a known range. It counts the number of occurrences of each element and uses this information to reconstruct a sorted array. It has a time complexity of O(n+k), where n is the number of elements and k is the range of input values.
8. **Radix Sort**: Sorts numbers by processing individual digits from least significant to most significant. It can be used for integers or strings. It has a time complexity of O(d * (n + k)), where d is the number of digits, n is the number of elements, and k is the range of input values.
9. **Bucket Sort**: Divides the input into equally spaced buckets, distributes elements into the buckets, sorts each bucket individually, and then concatenates the sorted buckets to obtain the final sorted array. It has an average time complexity of O(n+k), where n is the number of elements and k is the number of buckets.
10. **Shell Sort**: Variation of insertion sort that sorts elements far apart and progressively reduces the gap between elements to be compared. It has a time complexity that depends on the chosen gap sequence, typically ranging from O(n log n) to O(n^2).
11. **Tim Sort**: Hybrid sorting algorithm derived from merge sort and insertion sort. It divides the array into small blocks, sorts them using insertion sort, and then merges the sorted blocks using merge sort. It has a time complexity of O(n log n) and is known for its efficiency in handling real-world data.
12. **Comb Sort**: Variation of bubble sort that compares elements separated by a varying gap and swaps them if they are in the wrong order. It has a time complexity of O(n^2) but performs better than bubble sort in practice.
13. **Cocktail Shaker Sort**: Variation of bubble sort that sorts the list in both directions, repeatedly moving the largest and smallest elements to their correct positions. It has a time complexity of O(n^2) but can perform better than bubble sort in some cases.
14. **Cycle Sort**: Sorts the array by cycling through the elements and placing each element in its correct position, swapping it with the element already in that position. It has a time complexity of O(n^2) but is efficient for minimizing

## Give an exhaustive list of search algorithms. ##

Here is an exhaustive list of commonly used search algorithms:

1. **Linear Search**: A simple search algorithm that **sequentially checks each element in a list until a match is found or the end of the list is reached**.
2. **Binary Search**: A divide-and-conquer algorithm used to search for a target value in a sorted list by repeatedly dividing the search space in half.
3. **Depth-First Search (DFS)**: A graph traversal algorithm that explores as far as possible along each branch before backtracking. It is often used to traverse or search in tree or graph structures.
4. **Breadth-First Search (BFS)**: A graph traversal algorithm that explores all the vertices of a graph in breadth-first order, i.e., exploring all the vertices at the same level before moving to the next level.
5. **Uniform-Cost Search (UCS)**: A variant of Dijkstra's algorithm that explores the graph by considering the cost of reaching each node. It finds the shortest path from a starting node to a goal node in terms of cumulative edge costs.
6. **A\* Search**: An informed search algorithm that uses heuristics to guide the search towards the goal. It combines the advantages of both uniform-cost search and a heuristic function.
7. **Iterative Deepening Depth-First Search (IDDFS)**: A combination of depth-first search and breadth-first search where the depth-first search is performed iteratively with increasing depth limits.
8. **Greedy Search**: A search algorithm that makes locally optimal choices at each step, without considering the long-term consequences. It selects the option that appears to be the best at the current state.
9. **Hill Climbing**: A local search algorithm that repeatedly makes small changes to a current solution to reach an optimal solution. It is used in optimization problems but can get stuck in local optima.
10. **Best-First Search**: A search algorithm that uses a heuristic function to evaluate each node and selects the most promising node based on the heuristic value.
11. **Depth-Limited Search**: A variant of depth-first search that limits the depth of exploration to a specified level to avoid infinite loops or excessive search.
12. **Bidirectional Search**: A search algorithm that simultaneously explores from both the start and goal states, searching for a path where the searches meet.
13. **Jump Search**: A search algorithm used on sorted arrays. It performs linear search steps with a fixed step size and then performs linear search to find the exact location.
14. **Interpolation Search**: A search algorithm that extrapolates the position of the desired element based on the value of the target and the distribution of elements. It works on uniformly distributed sorted arrays.
15. **Exponential Search**: A search algorithm that performs a binary search after finding an appropriate range using exponential increments.
16. **Fibonacci Search**: A search algorithm that divides the array into Fibonacci numbers and narrows down the search range using these numbers.
17. **Red-Black Tree Search**: A search algorithm performed on a self-balancing binary search tree called a red-black tree, which ensures logarithmic search time.
18. **Trie Search**: A search algorithm performed on a tree-like data structure called a trie or prefix tree, often used for efficient search in string-related problems.

These are just some of the many search algorithms available. The choice of algorithm depends on the characteristics of the problem, the data structure used, and the specific requirements of the search task at hand.

## Techniques in Use ##
1) Sliding Window
2) Islands (Matrix Traversal)
3) Two Pointers
4) Fast & Slow Pointers
5) Merge Intervals
6) Cyclic Sort
7) In-place Reversal of a LinkedList
8) Tree Breadth-First Search
9) Tree Depth First Search
10) Two Heaps
11) Subsets
12) Modified Binary Search
13) Bitwise XOR
14) Top ‘K’ Elements
15) K-way Merge
16) Topological Sort
17) 0/1 Knapsack
18) Fibonacci Numbers
19) Palindromic Subsequence
20) Longest Common subsequence.