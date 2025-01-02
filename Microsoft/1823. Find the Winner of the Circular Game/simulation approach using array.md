# 1823. Find the Winner of the Circular Game

## Problem Statement
You are given `n` friends, numbered from `1` to `n`. They are playing a game in a circle, starting from friend `1` and moving clockwise. In each round, the friend at the current position counts `k` friends clockwise and eliminates the `k-th` friend. The process continues until only one friend remains. The task is to determine the winner of the game.

---

## Approach
The solution uses a **simulation-based approach** to replicate the game. A dynamic array keeps track of the friends still in the game. Here's how it works step-by-step:

1. **Initialization**:
   - Create an array `arr` with numbers from `1` to `n` representing the friends.
   - Use a variable `i` initialized to `0` to track the current position in the circle.

2. **Game Simulation**:
   - Continue the process until only one friend remains in the array.
   - Calculate the index of the friend to eliminate using the formula:
     ```cpp
     (i + k - 1) % arr.size()
     ```
   - Remove the friend at the calculated index using `erase`.
   - Update `i` to the position of the friend immediately after the eliminated one.

3. **Return the Winner**:
   - When the array has only one element left, that element is the winner.

---

## Code Implementation

```cpp
class Solution {
public:
    int findTheWinner(int n, int k) {
        vector<int> arr;
        // Initialize the array with friends numbered 1 to n
        for (int i = 1; i <= n; i++) {
            arr.push_back(i);
        }
        int i = 0; // Start the game from the first friend
        // Continue until only one friend remains
        while (arr.size() > 1) {
            // Calculate the index of the friend to eliminate
            int idx = (i + k - 1) % arr.size();
            arr.erase(arr.begin() + idx); // Remove the friend
            i = idx; // Update position to the next friend
        }
        return arr[0]; // The last remaining friend is the winner
    }
};
```

---

## Example Walkthrough

### Example 1
#### Input:
```plaintext
n = 5, k = 2
```

#### Simulation Steps:
1. Initial array: `[1, 2, 3, 4, 5]`
2. Eliminate friend at index `(0 + 2 - 1) % 5 = 1`: `[1, 3, 4, 5]`
3. Eliminate friend at index `(1 + 2 - 1) % 4 = 2`: `[1, 3, 5]`
4. Eliminate friend at index `(2 + 2 - 1) % 3 = 0`: `[3, 5]`
5. Eliminate friend at index `(0 + 2 - 1) % 2 = 1`: `[3]`

#### Output:
```plaintext
3
```

### Example 2
#### Input:
```plaintext
n = 6, k = 5
```

#### Simulation Steps:
1. Initial array: `[1, 2, 3, 4, 5, 6]`
2. Eliminate friend at index `(0 + 5 - 1) % 6 = 4`: `[1, 2, 3, 4, 6]`
3. Eliminate friend at index `(4 + 5 - 1) % 5 = 3`: `[1, 2, 3, 6]`
4. Eliminate friend at index `(3 + 5 - 1) % 4 = 3`: `[1, 2, 3]`
5. Eliminate friend at index `(3 + 5 - 1) % 3 = 1`: `[1, 3]`
6. Eliminate friend at index `(1 + 5 - 1) % 2 = 0`: `[3]`

#### Output:
```plaintext
3
```

---

## Complexity Analysis

### Time Complexity
- The outer loop runs `n-1` times (removing `n-1` friends).
- Each removal uses `erase`, which has a worst-case time complexity of `O(n)` for vectors.
- Overall time complexity: **`O(n^2)`**.

### Space Complexity
- A vector `arr` of size `n` is used to store the friends.
- Space complexity: **`O(n)`**.

---

## Key Points
- **Simulation-Based Approach**: This solution directly models the game, making the logic easy to follow.
- **Dynamic Index Management**: The modulo operation ensures circular traversal, mimicking the clockwise movement in the game.
- **Limitations**: For very large `n`, the `O(n^2)` time complexity may be suboptimal.

---

## Advantages
- **Intuitive**: The solution is simple and mirrors the actual gameplay.
- **Direct**: No additional data structures are required beyond the vector.

---
