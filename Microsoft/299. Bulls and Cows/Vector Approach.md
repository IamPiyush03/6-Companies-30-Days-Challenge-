# 299. Bulls and Cows

## Problem Statement
You are playing the "Bulls and Cows" game with your friend. You write down a secret number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in the guess match the secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your task is to return the hint in the format "xAyB", where `x` is the number of bulls and `y` is the number of cows.

## Solution
The solution uses two vectors to count the occurrences of each digit (0-9) in the secret and guess strings that are not bulls. It then calculates the number of cows by finding the minimum count of each digit in both vectors.

### Code
```cpp
class Solution {
public:
    string getHint(string secret, string guess) {
        int bulls = 0, cows = 0;
        vector<int> secretcount(10, 0), guesscount(10, 0);
        
        // Step 1: Count bulls and populate vectors for non-bull digits
        for (int i = 0; i < secret.size(); i++) {
            if (secret[i] == guess[i]) {
                bulls++;
            } else {
                secretcount[secret[i] - '0']++;
                guesscount[guess[i] - '0']++;
            }
        }

        // Step 2: Count cows
        for (int i = 0; i < 10; i++) {
            cows += min(secretcount[i], guesscount[i]);
        }

        return to_string(bulls) + 'A' + to_string(cows) + 'B';
    }
};
```

### Explanation
1. **Vector Initialization**:
   - Initialize two vectors `secretcount` and `guesscount` of size 10 to store counts of digits 0-9.

2. **Counting Bulls**:
   - Iterate through the `secret` and `guess` strings.
   - If characters at the same position are equal, increment the `bulls` count.
   - If not, increment the count of corresponding digits in respective vectors.

3. **Counting Cows**:
   - Iterate through digits 0-9 and find the minimum count between `secretcount` and `guesscount`.
   - Add this minimum value to the `cows` count.

### Complexity
- **Time Complexity**: O(n), where `n` is the length of the `secret` and `guess` strings.
- **Space Complexity**: O(1), as the vectors are of fixed size 10.

This approach efficiently calculates bulls and cows using vectors instead of hashmaps, which can be more memory-efficient for this specific case where we only need to track 10 possible digits.
