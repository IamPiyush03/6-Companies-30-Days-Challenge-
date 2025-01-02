# 462. Minimum Moves to Equal Array Elements II

## Problem Statement
Given an integer array `nums` of size `n`, return the minimum number of moves required to make all array elements equal. In one move, you can increment or decrement an element of the array by `1`.

## Solution
The solution uses the median approach to minimize the number of moves. The median minimizes the sum of absolute deviations from all other points in the array.

### Code
```cpp
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        int median = nums[n / 2];
        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans += abs(median - nums[i]);
        }
        return ans;
    }
};
```

### Explanation
1. **Sorting**:
   - The array `nums` is sorted to find the median easily.

2. **Finding the Median**:
   - The median is chosen as the middle element of the sorted array (`nums[n / 2]`).

3. **Calculating Moves**:
   - The total number of moves is calculated by summing up the absolute differences between each element and the median.

### Complexity
- **Time Complexity**: O(n log n), where `n` is the number of elements in the array. This is due to the sorting step.
- **Space Complexity**: O(1), as no extra space is used apart from the input array.

This approach efficiently finds the minimum number of moves to equalize the array elements using the median.
