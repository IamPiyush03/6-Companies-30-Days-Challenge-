# 1401. Circle and Rectangle Overlapping

## Problem Statement
Given a circle represented as `(radius, xCenter, yCenter)` and an axis-aligned rectangle represented as `(x1, y1, x2, y2)`, determine if the circle and rectangle overlap.

## Solution

### Approach
1. **Find Nearest Point**: For the circle's center `(xCenter, yCenter)`, find the nearest point on the rectangle. This is done by clamping the circle's center coordinates to the rectangle's boundaries.
2. **Calculate Distance**: Compute the distance between the circle's center and this nearest point.
3. **Check Overlap**: If the distance is less than or equal to the circle's radius, the circle and rectangle overlap.

### Code
```cpp
class Solution {
public:
    bool checkOverlap(int radius, int xCenter, int yCenter, int x1, int y1, int x2, int y2) {
        int nearest_x = max(x1, min(x2, xCenter));
        int nearest_y = max(y1, min(y2, yCenter));

        int dist_x = nearest_x - xCenter;
        int dist_y = nearest_y - yCenter;

        return pow(dist_x, 2) + pow(dist_y, 2) <= pow(radius, 2);
    }
};
```

### Explanation
1. **Finding Nearest Point**: 
   - `nearest_x` is the x-coordinate of the nearest point on the rectangle to the circle's center. It is clamped between `x1` and `x2`.
   - `nearest_y` is the y-coordinate of the nearest point on the rectangle to the circle's center. It is clamped between `y1` and `y2`.
2. **Calculating Distance**: 
   - `dist_x` is the horizontal distance between the circle's center and the nearest point.
   - `dist_y` is the vertical distance between the circle's center and the nearest point.
3. **Checking Overlap**: 
   - The sum of the squares of `dist_x` and `dist_y` is compared to the square of the radius. If it is less than or equal to the square of the radius, the circle and rectangle overlap.

### Complexity Analysis
- **Time Complexity**: O(1), as the solution involves a constant number of operations.
- **Space Complexity**: O(1), as no additional space is used.

### Example
```cpp
int radius = 5;
int xCenter = 0, yCenter = 0;
int x1 = -3, y1 = -3, x2 = 3, y2 = 3;
bool result = Solution().checkOverlap(radius, xCenter, yCenter, x1, y1, x2, y2);
// Output: true
```

In this example, the circle with radius 5 centered at (0, 0) overlaps with the rectangle defined by the corners (-3, -3) and (3, 3).

### Conclusion
This approach efficiently determines if a circle and a rectangle overlap by leveraging geometric properties and simple distance calculations.
