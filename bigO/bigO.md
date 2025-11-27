# Big O and Time Complexity

## What is Big O Notation?

// ...existing code...

# Big O and Time Complexity

## What is Big O Notation?

Big O notation describes how an algorithm's performance scales as the input size grows. It helps us understand the **worst-case scenario** for how long an algorithm takes to run or how much memory it uses.

Think of it like this: if you're organizing a library, Big O tells you how much longer the task takes when you have 1,000 books instead of 10.

## Common Time Complexities (from fastest to slowest)

| Notation      | Name         | Example                                    |
| ------------- | ------------ | ------------------------------------------ |
| $O(1)$        | Constant     | Accessing an array element by index        |
| $O(\log n)$   | Logarithmic  | Binary search                              |
| $O(n)$        | Linear       | Simple loop through array                  |
| $O(n \log n)$ | Linearithmic | Efficient sorting (merge sort, quick sort) |
| $O(n^2)$      | Quadratic    | Nested loops                               |
| $O(n^3)$      | Cubic        | Triple nested loops                        |
| $O(2^n)$      | Exponential  | Recursive algorithms without optimization  |
| $O(n!)$       | Factorial    | Generating all permutations                |

## Analyzing Time Complexity

### Rule 1: Drop Constants

$O(2n) = O(n)$ — We ignore constant multipliers because they don't affect how the algorithm scales.

### Rule 2: Drop Non-Dominant Terms

$O(n^2 + n) = O(n^2)$ — Focus on the term that grows fastest.

### Rule 3: Different Inputs Get Different Variables

If a function has two separate loops over different inputs, use different variables: $O(n + m)$.

## Examples

### Example 1: Linear Time - $O(n)$

```cpp
#include <vector>

int findMax(const std::vector<int>& arr) {
  int max = arr[0];
  for (size_t i = 1; i < arr.size(); ++i) {
    if (arr[i] > max) max = arr[i];
  }
  return max;
}
```

- We loop through the array once
- Time grows proportionally with input size

### Example 2: Quadratic Time - $O(n^2)$

```cpp
#include <vector>
#include <algorithm>

std::vector<int> bubbleSort(std::vector<int> arr) {
  for (size_t i = 0; i < arr.size(); ++i) {
    for (size_t j = 0; j + 1 < arr.size(); ++j) {
      if (arr[j] > arr[j + 1]) {
        std::swap(arr[j], arr[j + 1]);
      }
    }
  }
  return arr;
}
```

- Nested loops mean we do $n \times n$ operations
- For 100 items: ~10,000 operations

### Example 3: Logarithmic Time - $O(\log n)$

```cpp
#include <vector>

int binarySearch(const std::vector<int>& arr, int target) {
  int left = 0;
  int right = static_cast<int>(arr.size()) - 1;
  while (left <= right) {
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}
```

- We eliminate half the remaining elements each iteration
- For 1,000 items: ~10 operations vs. 1,000 with linear search

## Space Complexity

Space complexity follows the same Big O rules but measures **memory** instead of time.

```cpp
#include <vector>

std::vector<int> createArray(int n) {
  std::vector<int> arr;
  arr.reserve(n); // reserve to avoid repeated reallocations
  for (int i = 0; i < n; ++i) {
    arr.push_back(i);
  }
  return arr;
}
```

## Key Takeaways

- **Focus on the worst case** — Big O describes when an algorithm performs poorest
- **Ignore constants and lower-order terms** — They matter less as input grows
- **Know the common complexities** — Helps you spot inefficiencies quickly
- **Trade-offs exist** — Sometimes faster time complexity means more memory usage
