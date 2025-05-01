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
|---|---------|-------------|----------|------------------|-------|
| 1 | [Sort Colors](https://leetcode.com/problems/sort-colors/) | 75 | Sorting (O(n)) | Uses a variation of selection-like partitioning (Dutch National Flag); avoids built-in sort. Reinforces selection-like sort behavior. |
| 2 | [Remove Element](https://leetcode.com/problems/remove-element/) | 27 | Array manipulation | O(n) | Demonstrates how deletions work in arrays and the cost of shifting elements. |
| 3 | [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/) | 380 | Array + HashMap | Avg O(1) | Great example of handling fast insert/delete with array and pointer tricks. |
| 4 | [Design Linked List](https://leetcode.com/problems/design-linked-list/) | 707 | Linked List | O(n) for traversal | Directly explores manual linked list operations like insert, delete, and get. |
| 5 | [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) | 88 | Array insertions | O(n) | Highlights cost of merging arrays (insert/delete + shifting elements). |
| 6 | [Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/) | 350 | Array/List traversal | O(n + m) | Compares approaches using arrays and hash maps—emphasizes linear scans and memory handling. |

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
```
### The findSmallestIndex() function accesses elements in the input array multiple times to find the index of the smallest value. This is no different from an inner loop, and so the selection sort is quadratic O(n²) efficiency.
