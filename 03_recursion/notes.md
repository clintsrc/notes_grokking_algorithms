# Chapter 3: Recursion

## Key Concepts
- **Recursive Function**: A function that calls itself. It is at risk of entering an infinite loop.
- **Recursive case**: The recusive function calls itself
- **Base case**: The recursive function *does not* call itself again (preventing an infinite loop)
- **Call Stack** (operations): A stack has two operations: push and pop.
- **Call Stack** (state): All functions go onto the call stack. When a function calls another function that calling function is paused in a *partially completed state* with its variables stored in memory. When the called function returns, the calling function picks up where it left off.
- **Convenience**: It's convenient to use a recursive stack instead of iterating over a finite number of items inside a loop.
- **Cost**: The overhead of allocated memory for each call can be expensive. If it's too expensive it may be necessary to implement the loop instead (cf. or else use tail recursion)

## Exercises
- **3.1** Suppose I show you a call stack like this.

<img src="../images/03_recursion/033_the_stack/call_stack_greet.png" alt="Call Stack Greet" width="33%" height="33%">

What information can you give me, just based on this call stack?

A: greet() has a local 'name' variable set to 'Maggie'. It calls greet2() which has it's own local 'name' variable also set to 'Maggie'. greet() is in a suspended state when it calls greet2 (puts it's local 'name' variable on the call stack). When greet2() returns, greet() resumes.
- **3.2** Suppose you accidentally write a recursive function that runs forever. As you saw, your computer allocates memory on the stack for each function call. What happens to the stack when your recursive function runs forever?

A: At some point the program will crash with a stack overflow error when the OS fails to allocate more memory to the calling function.

## LeetCode Problems
| # | Problem | ID | Topic | Notes |
|---|---------|----|-------|-------|
| 1 | [Factorial Trailing Zeroes](https://leetcode.com/problems/factorial-trailing-zeroes/) | 172 | Recursion (Math) | Involves understanding of recursive factorial decomposition and base cases. |
| 2 | [Power of Two](https://leetcode.com/problems/power-of-two/) | 231 | Recursion / Bit Manipulation | Good for recognizing simple base and recursive cases. |
| 3 | [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | 206 | Recursion / Linked List | Uses recursive unwinding of call stack to reverse node pointers. |
| 4 | [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/) | 509 | Recursion / DP | Classic recursion with an obvious base case and exponential stack growth. |
| 5 | [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) | 104 | Recursion / Tree | Demonstrates call stack depth and multiple recursive paths. |
| 6 | [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | 21 | Recursion / Linked List | Recursive merging demonstrates memory state and functional stack behavior. |
| 7 | [Same Tree](https://leetcode.com/problems/same-tree/) | 100 | Recursion / Tree Comparison | Recursive symmetry with multiple base/recursive branches. |
| 8 | [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/) | 226 | Recursion / Tree Manipulation | Recursively swaps left and right children, showing suspended state in memory. |
| 9 | [Pascal’s Triangle II](https://leetcode.com/problems/pascals-triangle-ii/) | 119 | Recursion / Array | Uses recursive insight into row generation and base edge cases. |
|10 | [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) | 17 | Recursion / Backtracking | Deep recursion tree, stack unwinding shows recursive state traversal. |

## Important Code Snippets
### Recursive Function
```javascript
/**
 * Consider the factorial of the number
 * @param {number} x Number
 * @returns {number} Result
 */
function fact(x) {
  if (x === 0) return 1;
  return x * fact(x - 1);
}

console.log(fact(5));
```
- Recursive state: return x * fact(x - 1);
- Base state (prevents infinite loop): x === 0

### Call Stack
```javascript
/**
 * Displays a message to the console
 * @param {string} name Name
 */
function greet2(name) {
  console.log("how are you, " + name + "?");
}

/**
 * Displays a message to the console
 */
function bye() {
  console.log("ok bye!");
}

/**
 * Displays a message to the console
 * @param {string} name Name
 */
function greet(name) {
  console.log("hello, " + name + "!");
  greet2(name);
  console.log("getting ready to say bye...");
  bye();
}

greet("adit");
```
- All function calls go on the call stack (in memory)
- greet() call's last executed line and it's local variables are suspended (in memory on the call stack) when it calls greet2()
- greet2() goes on the top of the stack (its own location and variables stored in memory). When it returns, greet() will resume where it left off.