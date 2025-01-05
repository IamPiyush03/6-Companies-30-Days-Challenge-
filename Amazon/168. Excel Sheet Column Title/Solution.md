# 168. Excel Sheet Column Title

## Problem Statement
Given a positive integer `columnNumber`, return its corresponding column title as it appears in an Excel sheet. For example:
- 1 -> "A"
- 2 -> "B"
- 3 -> "C"
- ...
- 26 -> "Z"
- 27 -> "AA"
- 28 -> "AB"
- ...

## Solution

### Approach
1. **Initialize Result String**: Start with an empty string `ans` to build the result.
2. **Convert to Title**: Use a loop to convert the `columnNumber` to the corresponding title:
   - Calculate the character for the current position using `(columnNumber - 1) % 26`.
   - Prepend the character to the result string `ans`.
   - Update `columnNumber` by dividing it by 26 after subtracting 1.
3. **Return Result**: Once the loop completes, return the result string `ans`.

### Code
```cpp
class Solution {
public:
    string convertToTitle(int columnNumber) {
        string ans = "";
        while (columnNumber) {
            char c = 'A' + ((columnNumber - 1) % 26);
            ans = c + ans;
            columnNumber = (columnNumber - 1) / 26;
        }
        return ans;
    }
};
```

### Explanation
1. **Initialize Result String**: `ans` is initialized as an empty string.
2. **Convert to Title**:
   - In each iteration, calculate the character corresponding to the current position using `(columnNumber - 1) % 26` and convert it to a character by adding 'A'.
   - Prepend this character to `ans`.
   - Update `columnNumber` by dividing it by 26 after subtracting 1.
3. **Return Result**: The loop continues until `columnNumber` becomes 0. The final result string `ans` is returned.

### Complexity Analysis
- **Time Complexity**: O(log26(n)), where n is the input `columnNumber`. This is because we repeatedly divide the number by 26.
- **Space Complexity**: O(1) for the auxiliary space used.

### Example
```cpp
int columnNumber = 28;
string result = Solution().convertToTitle(columnNumber);
// Output: "AB"
```

In this example, the input `columnNumber` is 28. The corresponding Excel column title is "AB".

### Conclusion
This approach efficiently converts a given column number to its corresponding Excel sheet column title using simple arithmetic operations and string manipulation.
