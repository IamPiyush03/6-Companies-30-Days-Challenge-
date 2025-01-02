# 1823. Find the Winner of the Circular Game

## Problem Statement
You are given `n` friends, numbered from `1` to `n`. They are playing a game in a circle, starting from friend `1` and moving clockwise. In each step, `k-1` friends are skipped, and the `k-th` friend is eliminated from the circle. The game continues until only one friend remains. The task is to find the winner of the game.

## Solution
The solution uses a recursive approach to determine the winner of the circular game. The idea is to reduce the problem size by eliminating one friend at a time and adjusting the index of the winner accordingly.

### Code
```cpp
class Solution {
public:
    int findTheWinnerIdx(int n, int k) {
        if (n == 1)
            return 0;

        int idx = findTheWinnerIdx(n - 1, k);
        idx = (idx + k) % n;
        return idx;
    }
    int findTheWinner(int n, int k) {
        int result_idx = findTheWinnerIdx(n, k);
        return result_idx + 1;
    }
};
```

### Explanation
1. **findTheWinnerIdx Function**:
   - This function recursively finds the index of the winner in a zero-indexed list.
   - Base case: If there is only one friend (`n == 1`), the winner is at index `0`.
   - Recursive case: The function calls itself with `n-1` friends and adjusts the index of the winner by adding `k` and taking modulo `n`.

2. **findTheWinner Function**:
   - This function calls `findTheWinnerIdx` to get the zero-indexed winner and then adjusts it to one-indexed by adding `1`.

### Complexity
- **Time Complexity**: O(n), where `n` is the number of friends. The function makes `n` recursive calls.
- **Space Complexity**: O(n), due to the recursion stack.

