# Chapter 1: Introduction

## Key Concepts
- **O(log n) v O(n)**: The operation is divided stepwise by 2. A logarithmic op, $\log_2{8}$ = 3, answers the question: "To what power must 2 be raised to get 8?" O(log n) time complexity is more efficient than O(n) because the number of op grows logarithmically, halving the problem size at each step. In contrast, O(n) grows linearly, with 1 op per element.
- **O(log n) only works for sorted elements**: if the elements aren't sorted they can't be halved, and searches would require ops to O(n)
- **Big O worst case**: Worst case scenarios. Even if you win the lotto the complexity is O(n) because you might have to check every number.
- **Big O 'speed'**: Expresses growth rate of operations (as size of input increases), not execution time (the time can be calculated if you first know the rate).


## Big O run times (fastest to slowest)
- **O(1)**, constant time (access array element by index)
- **O(log n)**, log time (binary search)
- **O(n)**, linear time (simple search)
- **O(n * log n)**. (fast sorting algorithm, ie quicksort)
- **O(n²)**. (slow sorting algorithm, ie selection sort)
- **O(n!)**. (very slow, ie the traveling salesperson)

## Exercises
- **1.1** If you have a sorted list of 128 items in a binary search, it will take $\log_2{128}$ = 7 operations
- **1.2** If that list doubles (256), the ops increase stepwise by 2: $\log_2{256}$ = 8
- **1.3** Phone book (sorted list by name): run time for finding the number for a name? O(log n)
- **1.4** Run time for finding the name for a number? O(n) because it's sorted by name not number
- **1.5** Run time to read all numbers in the phone book? O(n)
- **1.6** Run time to read only the A's? O(n) because the algorithm is worst-case Big O. In Big O notation a constant is just a number and so O(n / 26) is not valid.

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
