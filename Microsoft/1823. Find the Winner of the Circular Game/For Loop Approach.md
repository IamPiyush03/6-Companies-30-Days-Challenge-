

# 1823. Find the Winner of the Circular Game

## Problem Description

You are given `n` friends who are playing a game. The friends are sitting in a circle and are numbered from 1 to `n` in a clockwise direction. More formally, moving clockwise from the `i-th` friend brings you to the `(i+1)-th` friend for `1 <= i < n`, and moving clockwise from the `n-th` friend brings you to the `1-st` friend.

The rules of the game are as follows:

1. Start at friend 1.
2. Count the next `k` friends in the clockwise direction, including the friend you started at. The counting wraps around the circle and may count some friends more than once.
3. The last friend you counted leaves the circle and loses the game.
4. If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
5. The last friend remaining in the circle wins the game.

You are given two integers, `n` and `k`, and you need to return the winner of the game.

## Solution

The solution uses the Josephus Problem approach to determine the winner. The Josephus Problem is a famous theoretical problem related to a certain elimination game.

### Code

```cpp
class Solution {
public:
    int findTheWinner(int n, int k) {
        int val = 0;
        for (int i = 2; i < n + 1; i++) {
            val = (val + k) % i;
        }
        return val + 1;
    }
};
```

### Explanation

1. Initialize `val` to 0. This variable will hold the index of the winner.
2. Iterate from 2 to `n` (inclusive). In each iteration, update `val` using the formula `(val + k) % i`. This formula adjusts the index of the winner in a 0-based index system.
3. After completing the loop, add 1 to `val` to convert it to a 1-based index system, which represents the actual position of the winner.

## Usage

To use this code, create an instance of the `Solution` class and call the `findTheWinner` method with the appropriate parameters `n` (number of friends) and `k` (step count).

### Example

```cpp
Solution solution;
int winner = solution.findTheWinner(5, 2);
// winner will be 3
```

In this example, with `n = 5` and `k = 2`, the winner is friend number 3.

## Conclusion

This solution efficiently determines the winner of the circular game using the Josephus Problem approach with a time complexity of O(n).
```

You can copy this content into a `README.md` file in your repository.
