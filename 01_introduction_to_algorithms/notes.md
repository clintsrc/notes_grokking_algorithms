# Chapter 1: Introduction

## Key Concepts
- **O(log n) v O(n)**: For O(log n) the operation is divided stepwise by 2. A logarithmic op, $\log_2{8}$ = 3, answers the question: "To what power must 2 be raised to get 8?"
  - O(log n) time complexity is more efficient than O(n) because the number of op grows logarithmically, halving the problem size at each step. O(n) grows linearly at 1 op per element.
  - O(log n) is faster than O(n), but it gets a lot faster once the list of items you’re searching through grows.
- **O(log n) only works for sorted elements**: if the elements aren't sorted they can't be halved, and searches would require ops to O(n)
- **Big O worst case**: Worst case scenarios. Even if you win the lotto the complexity is O(n) because you might have to check every number.
- **Big O 'speed'**: Expresses growth rate of operations (as size of input increases), not execution time (the time can be calculated if you first know the rate).
- **Traveling salesperson**: O(n!) problems exist with no known improvement. Iconic traveling salesperson problem describes a salesperson seeking the shortest distance to travel to a few cities. All possible distances between each city is calcluated and compared against the total distance. As the number of cities increases, the ops to find the shortest route increases factorially.


## Big O run times (fastest to slowest)
- **O(1)**, constant time (access array element by index)
- **O(log n)**, log time (binary search)
- **O(n)**, linear time (simple search)
- **O(n * log n)**. (fast sorting algorithm, ie quicksort)
- **O(n²)**. (slow sorting algorithm, ie selection sort)
- **O(n!)**. factorial time (very slow, ie the traveling salesperson)

## Exercises
- **1.1** If you have a sorted list of 128 items in a binary search, it will take $\log_2{128}$ = 7 operations
- **1.2** If that list doubles (256), the ops increase stepwise by 2: $\log_2{256}$ = 8
- **1.3** Phone book (sorted list by name): run time for finding the number for a name? O(log n)
- **1.4** Run time for finding the name for a number? O(n) because it's sorted by name not number
- **1.5** Run time to read all numbers in the phone book? O(n)
- **1.6** Run time to read only the A's? O(n) because the algorithm is worst-case Big O. In Big O notation a constant is just a number and so O(n / 26) is not valid.

## LeetCode Problems

| #  | Problem | Category | Time Complexity | Notes |
|----|---------|----------|------------------|-------|
| 1  | [Binary Search (704)](https://leetcode.com/problems/binary-search/) | Binary Search | O(log n) | Textbook example of binary search. Must sort data if not already. |
| 2  | [Guess Number Higher or Lower (374)](https://leetcode.com/problems/guess-number-higher-or-lower/) | Binary Search | O(log n) | Direct application of divide-and-conquer logic. |
| 3  | [First Bad Version (278)](https://leetcode.com/problems/first-bad-version/) | Binary Search | O(log n) | Binary search with constraints. Classic "bounded range" pattern. |
| 4  | [Find Target Indices After Sorting (2089)](https://leetcode.com/problems/find-target-indices-after-sorting-array/) | Sort + Linear Scan | O(n log n) + O(n) | Combines sorting with a simple linear pass. |
| 7  | [Search Insert Position (35)](https://leetcode.com/problems/search-insert-position/) | Binary Search | O(log n) | Binary search variant to find a potential insertion point. |
| 8  | [Squares of a Sorted Array (977)](https://leetcode.com/problems/squares-of-a-sorted-array/) | Two Pointers / Sort | O(n log n) → O(n) | First thought is sorting; better solution uses two pointers. |


## Important Code Snippets
### Binary search O(log n)
```javascript
/**
 * Searches recursively number from the list
 * @param {Array} list Source array
 * @param {number} item Search item
 * @returns {(number|null)} Number if the value is found or NULL otherwise
 */
function binary_search(list, item) {
  let low = 0;
  let high = list.length - 1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    const guess = list[mid];

    if (guess === item) {
      return mid;
    } else if (guess > item) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return null;
}

const my_list = [1, 3, 5, 7, 9];

console.log(binary_search(my_list, 3)); // 1
console.log(binary_search(my_list, -1)); // null
