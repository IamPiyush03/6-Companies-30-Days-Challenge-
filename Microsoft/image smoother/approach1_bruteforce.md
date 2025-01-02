# Image Smoother - Approach 1: Brute Force

## Problem Overview
This implementation of the image smoother uses **direction vectors** to iterate over all possible neighbors for a given cell in a concise and organized manner.

## Solution

```cpp
class Solution {
public:
    vector<vector<int>> directions{
        {-1,-1},{-1,0},{-1,1},
        {0,-1},{0,0},{0,1},
        {1,-1},{1,0},{1,1}
    };
    vector<vector<int>> imageSmoother(vector<vector<int>>& img) {
        int m = img.size();
        int n = img[0].size();
        vector<vector<int>> result(m, vector<int>(n, 0));

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int sum_neighbours = 0;
                int count_neighbours = 0;
                for (auto& it : directions) {
                    int i_ = i + it[0];
                    int j_ = j + it[1];

                    if (i_ >= 0 && i_ < m && j_ >= 0 && j_ < n) {
                        sum_neighbours += img[i_][j_];
                        count_neighbours++;
                    }
                }
                result[i][j] = sum_neighbours / count_neighbours;
            }
        }
        return result;
    }
};
```

## Explanation

### Key Concepts

1. **Directions Vector**:
    ```cpp
    vector<vector<int>> directions{
        {-1,-1},{-1,0},{-1,1},
        {0,-1},{0,0},{0,1},
        {1,-1},{1,0},{1,1}
    };
    ```
    This vector stores all relative positions of a 3x3 grid around a cell, including the cell itself. Each pair \((dx, dy)\) represents a relative offset:
    - **(-1, -1)**: Top-left neighbor.
    - **(-1, 0)**: Top neighbor.
    - **(0, 0)**: The current cell.
    - **(1, 1)**: Bottom-right neighbor.
   
    Using this structure, we can iterate through all neighbors in a structured way without writing multiple nested loops.

2. **Matrix Dimensions**:
    ```cpp
    int m = img.size();
    int n = img[0].size();
    ```
    - `m` and `n` represent the number of rows and columns in the matrix.
    - This ensures that the program can dynamically adapt to any valid matrix size.

3. **Result Matrix**:
    ```cpp
    vector<vector<int>> result(m, vector<int>(n, 0));
    ```
    - A new matrix `result` is initialized with the same dimensions as `img`.
    - This matrix will store the smoothed values.

4. **Iterating Through Cells**:
    ```cpp
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
    ```
    - This double loop ensures that every cell in the matrix is visited.

5. **Iterating Through Neighbors**:
    ```cpp
    for (auto& it : directions) {
        int i_ = i + it[0];
        int j_ = j + it[1];
    ```
    - The `for (auto& it : directions)` loop iterates through each direction in the `directions` vector.
    - For each direction, the neighbor’s coordinates are computed as:
      \[
      i\_ = i + dx, \quad j\_ = j + dy
      \]
      where \((dx, dy)\) comes from `directions`.

6. **Validating Neighbor Coordinates**:
    ```cpp
    if (i_ >= 0 && i_ < m && j_ >= 0 && j_ < n) {
    ```
    - This condition ensures that the computed neighbor \((i_, j_)\) lies within the bounds of the matrix.
    - If the neighbor is valid, its value is added to `sum_neighbours`, and the count is incremented.

7. **Computing the Average**:
    ```cpp
    result[i][j] = sum_neighbours / count_neighbours;
    ```
    - After iterating through all valid neighbors, the sum of their values (`sum_neighbours`) is divided by their count (`count_neighbours`).
    - The floored average is stored in the corresponding cell of the `result` matrix.

8. **Returning the Result**:
    ```cpp
    return result;
    ```
    - After all cells are processed, the resulting smoothed matrix is returned.

## Example Walkthrough

### Input:
```cpp
img = [[1, 1, 1],
       [1, 0, 1],
       [1, 1, 1]];
```

### Iteration for (0, 0):
1. **Neighbors**:
    - Using `directions`, compute neighbors \((i_, j_)\): \((-1,-1), (-1,0), (-1,1), (0,-1), (0,0), (0,1), (1,-1), (1,0), (1,1)\).
    - Valid neighbors: \((0,0), (0,1), (1,0), (1,1)\).
2. **Sum and Count**:
    - `sum_neighbours = 1 + 1 + 1 + 0 = 3`.
    - `count_neighbours = 4`.
3. **Average**:
    - `result[0][0] = 3 / 4 = 0`.

## Complexity Analysis

1. **Time Complexity**:
    - Outer loops iterate through all cells (\(m \times n\)).
    - Inner loop iterates through 9 neighbors (constant).
    - Total: \(O(m \times n \times 9) = O(m \times n)\).

2. **Space Complexity**:
    - `result` matrix: \(O(m \times n)\).
    - `directions` vector: \(O(1)\).
    - Total: \(O(m \times n)\).

## Advantages of This Approach
1. **Readability**:
    - Using `directions` makes the logic for neighbor traversal clean and easy to follow.
2. **Reusability**:
    - The `directions` vector can be reused for other 2D grid problems.
3. **Bound Checking**:
    - Simplifies neighbor validation with a single condition.

This approach is elegant and combines clarity with efficiency, making it a robust solution for the problem.
