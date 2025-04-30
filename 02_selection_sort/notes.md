# Chapter 2: Selection Sort

## Key Concepts
- **Array v Linked List**: focus on how they're mapped in memory: array is contiguous (expensive, potentially wasteful), linked list noncontiguous (dynamically mapped, allocated as needed, efficient)
- **Arrays**: Direct read access (index is location). All elements in the array should be the same type (all ints, all doubles, etc).
- **List**: Sequential access. Each element has a field that points to the next in the list. The discussion assumes if an available reference to the node for delete/add.
- **Hybrid**: Array of linked lists: example array compartmentalized alphabetically, storing lists of items beginning with that letter

# Array vs List Operations

| Operation   | Array                | Linked List          |
|-------------|----------------------|----------------------|
| **Read**    | O(1)                 | O(n)                 |
| **Delete**  | O(n)                 | O(1)                 |
| **Insert**  | O(n)                 | O(1) (head/tail)     |
| **Update**  | O(1)                 | O(n) (traverse)      |

---

### Key Insights:

- **Read**:
   - **Arrays** provide direct access by index
   - **Linked Lists** require traversal from the head to find the desired node

- **Delete**:
   - **Arrays** involve shifting subsequent elements to fill the gap after deletion.
   - **Linked Lists** allow **O(1)** deletion if the node reference is available; if not, finding the node takes **O(n)** time.

- **Insert**:
   - **Arrays** additional time may be required due to shifting element.
   - **Linked Lists** Head/tail use **O(1)**. Middle takes **O(n)** due to traversal.

- **Update**:
   - **Arrays** elements are directly accessed by index.
   - **Linked Lists** r**O(n)** time to find the node, update is **O(1)**.

## Exercises
- **2.1** You update a daily finance list and total the expenses (many inserts, few reads). Use array or list? A list has faster insertions. Reads only happen monthly, and even then it's probably more efficient since you'll be reading the entire list anyway.
- **2.2** A restaraunt wait staff takes orders and adds them to a queue (first in) for the cooks to fill (first out). Use array (random access) or list (inserts/deletes)? Since no (or very few) searches would be needed a list would be more efficient for the insert/deletes.
- **2.3** Facebook keeps a list of usernames. It searches for the username in a list of usernames for their login. If they use a binary search which requires random access. Use array or list? A sorted list would access the user instantly (rather than the full traversal required using a list)
- **2.4** If Facebook uses an array for the list of users, think about signups (adding). What is the downside of adding a new user to the list of users? Inserts to an array are expensive, and it must be sorted in order to take advantage of a binary search.
- **2.5** If Facebook used a hybrid: 26 elements to index alphabetically, each element is a pointer to a list. Compare this hybrid structure to arrays and lists: is it slower or faster than each for searching and inserting. Is the hybrid structure faster or slower? Search: faster slower than an array but faster than a list. Insert: faster than arrays, same for a list. Result: slower for searching than an array, but faster or equal to a list overall.

## LeetCode Problems

| # | Problem | LeetCode # | Category | Time Complexity | Notes |
|----|---------|------------|----------|------------------|-------|
| 1 | [Find Maximum Number in Array](https://leetcode.com/problems/maximum-subarray/) | 53 | Linear Scan | O(n) | Focus only on identifying the largest element (not Kadane’s logic yet). |
| 2 | [Find Numbers With Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/) | 1295 | Linear Scan | O(n) | Basic loop through array + number-to-string length check. |
| 3 | [Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/) | 1346 | Scan / Set | O(n²) → O(n) | Start with brute force, then use a `Set` for efficiency. |
| 4 | [Find Target Indices After Sorting](https://leetcode.com/problems/find-target-indices-after-sorting-array/) | 2089 | Sort + Linear Scan | O(n log n) + O(n) | Combines sorting with targeted element selection. |
| 5 | [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/) | 977 | Two Pointers | O(n) | Optimized approach beats naive sort of squared values. |
| 6 | [Count Items Matching a Rule](https://leetcode.com/problems/count-items-matching-a-rule/) | 1773 | Filter / Loop | O(n) | Simple filter-style logic, builds comfort with conditions. |
| 7 | [Count Negative Numbers in a Sorted Matrix](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/) | 1351 | Grid Traversal | O(m + n) | Think row/column relationships in sorted data. |

## Important Code Snippets
### Selection Sort O(n²)
```typescript
function findSmallestIndex<T>(array: T[]): number {
  let smallestIndex: number = 0;
  let smallestElement: T = array[smallestIndex];

  for (let i: number = 1; i < array.length; i++) {
    if (array[i] < smallestElement) {
      smallestElement = array[i];
      smallestIndex = i;
    }
  }

  return smallestIndex;
}

function selectionSort<T>(array: T[]): T[] {
  const sortedArray: T[] = [];
  const length = array.length;

  for (let i: number = 0; i < length; i++) {
    const smallestIndex: number = findSmallestIndex(array);
    sortedArray.push(array.splice(smallestIndex, 1)[0]);
  }

  return sortedArray;
}

console.log(selectionSort([5, 3, 6, 2, 10])); // [2, 3, 5, 6, 10]