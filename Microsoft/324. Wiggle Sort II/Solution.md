# 324. Wiggle Sort II

## Problem Statement
Given an unsorted array `nums`, reorder it such that `nums[0] < nums[1] > nums[2] < nums[3]...`.

## Solution

### Approach
1. **Sort the Array**: First, sort the array to make it easier to rearrange elements.
2. **Create a Result Array**: Create a new array `ans` of the same size as `nums` to store the result.
3. **Fill Odd Indices**: Fill the odd indices of `ans` with the largest elements from the sorted `nums`.
4. **Fill Even Indices**: Fill the even indices of `ans` with the remaining elements from the sorted `nums`.
5. **Copy Back to Original Array**: Copy the elements from `ans` back to `nums`.

### Code
```cpp
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<int> ans(nums.size());
        int n = nums.size();
        int i = 1;
        int j = n - 1;
        while (i < n) {
            ans[i] = nums[j];
            i += 2;
            j--;
        }
        i = 0;
        while (i < n) {
            ans[i] = nums[j];
            i += 2;
            j--;
        }
        for (int k = 0; k < n; k++) {
            nums[k] = ans[k];
        }
    }
};
```

### Explanation
1. **Sorting**: The array is sorted in ascending order.
2. **Filling Odd Indices**: Starting from the largest element, fill the odd indices (1, 3, 5, ...) of `ans`.
3. **Filling Even Indices**: Continue with the remaining elements to fill the even indices (0, 2, 4, ...) of `ans`.
4. **Copying Back**: Finally, copy the rearranged elements from `ans` back to the original `nums` array.

### Complexity Analysis
- **Time Complexity**: O(n log n) due to the sorting step.
- **Space Complexity**: O(n) for the auxiliary array `ans`.

### Example
```cpp
vector<int> nums = {1, 5, 1, 1, 6, 4};
Solution().wiggleSort(nums);
// Output: [1, 6, 1, 5, 1, 4]
```

In this example, the sorted array is [1, 1, 1, 4, 5, 6]. The odd indices are filled with [6, 5, 4] and the even indices with [1, 1, 1], resulting in the wiggle sorted array [1, 6, 1, 5, 1, 4].

### Conclusion
This approach ensures that the array is rearranged to satisfy the wiggle sort condition. The use of sorting simplifies the process of finding the correct elements for each position in the result array.
