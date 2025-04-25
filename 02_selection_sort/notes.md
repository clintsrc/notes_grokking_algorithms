# Chapter 2: Selection Sort

## Key Concepts
- **Array v Linked List**: focus on how they're mapped in memory: array is contiguous (expensive, potentially wasteful), linked list noncontiguous (dynamically mapped, allocated as needed, efficient)
- **Arrays**: Direct read access (index is location)
- **List**: Sequential access. Each element has a field that points to the next in the list. The discussion assumes if an available reference to the node for delete/add.
- **Hybrid**: Array of linked lists: example array compartmentalized alphabetically, storing lists of items beginning with that letter
- **Concept 3**: Brief explanation of concept.

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

| #  | Problem | Category | Time Complexity | Notes |
|----|---------|----------|------------------|-------|
| 1  | [Binary Search (704)](https://leetcode.com/problems/binary-search/) | Binary Search | O(log n) | Textbook example of binary search. Must sort data if not already. |
| 2  | [Guess Number Higher or Lower (374)](https://leetcode.com/problems/guess-number-higher-or-lower/) | Binary Search | O(log n) | Direct application of divide-and-conquer logic. |
| 3  | [First Bad Version (278)](https://leetcode.com/problems/first-bad-version/) | Binary Search | O(log n) | Binary search with constraints. Classic "bounded range" pattern. |
| 4  | [Find First and Last Position of Element in Sorted Array (34)](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | Binary Search | O(log n) | Find the range of a target element in a sorted array. |
| 5  | [Search a 2D Matrix (74)](https://leetcode.com/problems/search-a-2d-matrix/) | Binary Search | O(log m + log n) | Binary search in a 2D matrix. |
| 6  | [Search a 2D Matrix II (240)](https://leetcode.com/problems/search-a-2d-matrix-ii/) | Binary Search | O(m + n) | Binary search variant in a matrix with sorted rows and columns. |
| 7  | [Sort an Array (912)](https://leetcode.com/problems/sort-an-array/) | Sorting | O(n log n) | Implement sorting algorithms like quicksort, mergesort. |
| 8  | [Sort Colors (75)](https://leetcode.com/problems/sort-colors/) | Sorting | O(n) | Sort using the Dutch National Flag algorithm. |
| 9  | [Kth Largest Element in an Array (215)](https://leetcode.com/problems/kth-largest-element-in-an-array/) | Sorting / Heap | O(n log n) | Find the kth largest element using sorting or a heap. |
| 10 | [Median of Two Sorted Arrays (4)](https://leetcode.com/problems/median-of-two-sorted-arrays/) | Binary Search | O(log(min(n, m))) | Use binary search to find the median of two sorted arrays. |
| 11 | [Binary Tree Level Order Traversal (102)](https://leetcode.com/problems/binary-tree-level-order-traversal/) | BFS | O(n) | Level-order traversal using breadth-first search (BFS). |
| 12 | [Number of Islands (200)](https://leetcode.com/problems/number-of-islands/) | DFS | O(n * m) | Count the number of connected components using depth-first search (DFS). |

## Important Code Snippets
```javascript
// Include key code examples you find important or tricky
const example = "This is an important piece of code";