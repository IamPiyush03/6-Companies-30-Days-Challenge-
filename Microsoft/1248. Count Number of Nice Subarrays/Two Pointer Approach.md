# 1248. Count Number of Nice Subarrays

## Problem Statement
Given an array of integers `nums` and an integer `k`, return the number of nice subarrays. A nice subarray is defined as a contiguous subarray that contains exactly `k` odd numbers.

## Solution
The solution uses a two-pointer approach to count the number of subarrays with at most `k` odd numbers. The number of subarrays with exactly `k` odd numbers is then calculated by subtracting the number of subarrays with at most `k-1` odd numbers from the number of subarrays with at most `k` odd numbers.

### Code
```cpp
class Solution {
public:
    int lessEqualtoK(vector<int>& nums, int goal) {
        if (goal < 0) return 0;
        int n = nums.size();
        int i = 0;
        int j = 0;
        int sum = 0;
        int count = 0;
        while (j < n) {
            sum += (nums[j] % 2);
            while (sum > goal) {
                sum -= (nums[i] % 2);
                i++;
            }
            count += (j - i + 1);
            j++;
        }
        return count;
    }

    int numberOfSubarrays(vector<int>& nums, int k) {
        return lessEqualtoK(nums, k) - lessEqualtoK(nums, k - 1);
    }
};
```

### Explanation
1. **lessEqualtoK Function**:
   - This function counts the number of subarrays with at most `goal` odd numbers.
   - It uses a two-pointer approach to maintain a sliding window of subarrays.
   - The `sum` variable keeps track of the number of odd numbers in the current window.
   - The `count` variable accumulates the number of valid subarrays.

2. **numberOfSubarrays Function**:
   - This function calculates the number of subarrays with exactly `k` odd numbers.
   - It calls `lessEqualtoK` with `k` and `k-1` and returns the difference.

### Complexity
- **Time Complexity**: O(n), where `n` is the number of elements in the array. The two-pointer approach ensures that each element is processed at most twice.
- **Space Complexity**: O(1), as no extra space is used apart from the input array.

This approach efficiently counts the number of nice subarrays using the two-pointer technique.
