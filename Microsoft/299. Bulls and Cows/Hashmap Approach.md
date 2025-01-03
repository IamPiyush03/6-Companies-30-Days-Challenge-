# 299. Bulls and Cows

## Problem Statement
You are playing the "Bulls and Cows" game with your friend. You write down a secret number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in the guess match the secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your task is to return the hint in the format "xAyB", where `x` is the number of bulls and `y` is the number of cows.

## Solution
The solution uses two hashmaps to count the occurrences of each digit in the secret and guess strings that are not bulls. It then calculates the number of cows by finding the minimum count of each digit in both hashmaps.

### Code
```cpp
class Solution {
public:
    string getHint(string secret, string guess) {
        int bulls = 0, cows = 0;
        unordered_map<char, int> secretmap, guessmap;
        
        // Step 1: Count bulls and populate hashmaps for non-bull characters
        for (int i = 0; i < secret.size(); i++) {
            if (secret[i] == guess[i]) {
                bulls++;
            } else {
                secretmap[secret[i]]++;
                guessmap[guess[i]]++;
            }
        }

        // Step 2: Count cows
        for (auto pair : guessmap) {
            char digit = pair.first;
            cows += min(secretmap[digit], guessmap[digit]);
        }

        return to_string(bulls) + 'A' + to_string(cows) + 'B';
    }
};
```

### Explanation
1. **Counting Bulls**:
   - Iterate through the `secret` and `guess` strings.
   - If the characters at the same position are equal, increment the `bulls` count.
   - If not, populate the `secretmap` and `guessmap` with the counts of the characters.

2. **Counting Cows**:
   - Iterate through the `guessmap` and for each character, find the minimum count between `secretmap` and `guessmap`.
   - Increment the `cows` count by this minimum value.

3. **Returning the Result**:
   - Construct the result string in the format "xAyB" using the counts of bulls and cows.

### Complexity
- **Time Complexity**: O(n), where `n` is the length of the `secret` and `guess` strings. Each character is processed a constant number of times.
- **Space Complexity**: O(1), as the hashmaps store a fixed number of characters (digits 0-9).

This approach efficiently calculates the number of bulls and cows using hashmaps.
