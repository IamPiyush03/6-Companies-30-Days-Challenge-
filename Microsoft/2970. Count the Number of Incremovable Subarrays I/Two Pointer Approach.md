# Count the Number of Incremovable Subarrays I - Two Pointer Approach

## Problem Overview
The problem requires counting how many subarrays can be removed from the given array `nums` such that, after removal, the remaining array remains incrementally ordered (i.e., it should be strictly increasing).

## Solution

```cpp
class Solution {
public:
    int incremovableSubarrayCount(vector<int>& nums) {
        int i = 0, n = nums.size();
        while (i + 1 < n && nums[i] < nums[i + 1]) {
            ++i;
        }
        if (i == n - 1) {
            return n * (n + 1) / 2;
        }
        int ans = i + 2;
        for (int j = n - 1; j > 0; --j) {
            while (i >= 0 && nums[i] >= nums[j]) {
                --i;
            }
            ans += i + 2;
            if (nums[j - 1] >= nums[j]) {
                break;
            }
        }
        return ans;
    }
};
```

### Explanation

1. **Variable Initialization**:
    ```cpp
    int i = 0, n = nums.size();
    ```
    - `i` is used to track the index of the longest strictly increasing prefix of the array.
    - `n` holds the size of the input array `nums`.

2. **Step 1: Identify the longest increasing prefix**:
    ```cpp
    while (i + 1 < n && nums[i] < nums[i + 1]) {
        ++i;
    }
    ```
    - This loop iterates through the array from the beginning to find the longest prefix that is strictly increasing.
    - It stops when `nums[i]` is no longer smaller than `nums[i + 1]`, which marks the end of the increasing sequence.
    - After this loop, `i` will represent the last index of the longest increasing subsequence at the beginning of the array.

3. **Step 2: Special case when the entire array is strictly increasing**:
    ```cpp
    if (i == n - 1) {
        return n * (n + 1) / 2;
    }
    ```
    - If `i` is equal to `n - 1`, it means the entire array is strictly increasing.
    - In this case, all subarrays are removable because any subarray will leave behind a strictly increasing array.
    - The total number of subarrays in an array of size `n` is given by the formula for the sum of the first `n` natural numbers: `n * (n + 1) / 2`.

4. **Step 3: Count removable subarrays**:
    ```cpp
    int ans = i + 2;
    ```
    - Initialize the result with `i + 2`. This accounts for all the subarrays in the strictly increasing prefix. The `+2` is to adjust for the fact that the number of subarrays that can be removed start from the second element onwards.

5. **Step 4: Process the remaining elements in reverse order**:
    ```cpp
    for (int j = n - 1; j > 0; --j) {
        while (i >= 0 && nums[i] >= nums[j]) {
            --i;
        }
        ans += i + 2;
        if (nums[j - 1] >= nums[j]) {
            break;
        }
    }
    ```
    - Start from the end of the array (index `n - 1`) and iterate backwards.
    - For each element, the code checks if it can form a valid subarray with any part of the previously identified increasing prefix (`nums[i]`).
    - The `while (i >= 0 && nums[i] >= nums[j])` loop moves `i` backwards until a smaller value is found, ensuring that the subarray we are counting still maintains the strictly increasing property.
    - For each valid subarray found, the count (`ans`) is incremented by `i + 2`, accounting for the subarrays ending at `j`.
    - The `if (nums[j - 1] >= nums[j])` condition ensures that if a non-increasing pair is found while processing backwards, the loop breaks, as no further valid subarrays can be found in this direction.

6. **Return the result**:
    ```cpp
    return ans;
    ```
    - Finally, the function returns the total count of incrementally removable subarrays.
