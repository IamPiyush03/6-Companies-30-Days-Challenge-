# 187. Repeated DNA Sequences

## Problem Statement
Given a string `s` that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in any order.

## Solution
The solution uses a hashmap (unordered_map) to count the occurrences of each 10-letter-long substring in the DNA sequence. Substrings that appear more than once are collected and returned.

### Code
```cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        vector<string> ans;
        if (s.length() <= 10) return ans;

        unordered_map<string, int> mp;

        for (int i = 0; i <= s.length() - 10; i++) {
            string sub = s.substr(i, 10);
            mp[sub]++;
        }

        for (auto x : mp) {
            if (x.second > 1) ans.push_back(x.first);
        }
        return ans;
    }
};
```

### Explanation
1. **Initial Check**:
   - If the length of the string `s` is less than or equal to 10, return an empty vector since no 10-letter-long sequences can be formed.

2. **Counting Substrings**:
   - Use a hashmap `mp` to count the occurrences of each 10-letter-long substring.
   - Iterate through the string `s` and extract each 10-letter-long substring using `s.substr(i, 10)`.
   - Increment the count of each substring in the hashmap.

3. **Collecting Results**:
   - Iterate through the hashmap and collect all substrings that appear more than once into the result vector `ans`.

### Complexity
- **Time Complexity**: O(n), where `n` is the length of the string `s`. Each substring extraction and hashmap operation is O(1) on average.
- **Space Complexity**: O(n), for storing the substrings and their counts in the hashmap.

This approach efficiently finds all 10-letter-long repeated sequences in the DNA string using a hashmap.
