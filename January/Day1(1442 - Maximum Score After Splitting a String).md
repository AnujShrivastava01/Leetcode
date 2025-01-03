# Day 1 - LeetCode Problem 1442 - Maximum Score After Splitting a String

## Problem Description
Given a binary string `s`, you can split it into two non-empty substrings `s1` and `s2` (i.e., `s = s1 + s2`). The score after splitting is the sum of:
- The number of `0`'s in `s1`.
- The number of `1`'s in `s2`.

Return the maximum score you can achieve after splitting the string.

---

## Approaches

### Approach 1: Brute Force
- **Logic**:  
  - Count the total number of `1`s in the string.
  - Iterate through the string, keeping track of the number of `0`s in the left substring (`s1`) and updating the number of `1`s in the right substring (`s2`) by decrementing the count.
  - Calculate the score as the sum of `0`s in `s1` and `1`s in `s2`.
  - Update the maximum score encountered during the iteration.

- **Code**:
```cpp
class Solution {
public:
    int maxScore(string s) {
        int ones = 0;
        int n = s.length();
        for (int i = 0; i < n; i++) {
            if (s[i] == '1') {
                ones++;
            }
        }
        int zeroes = 0;
        int res = 0;
        for (int i = 0; i < n - 1; i++) {
            if (s[i] == '0') {
                zeroes++;
            } else {
                ones--;
            }
            res = max(res, zeroes + ones);
        }
        return res;
    }
};
```

---

### Approach 2: Optimized with Difference Tracking
- **Logic**:  
  - Use the difference between the count of `0`s and `1`s (`zeroes - ones`) as a key metric.
  - Track the running difference (`zeroes - ones`) while iterating through the string.
  - At each split point, calculate the maximum difference and adjust it with the total count of `1`s.

- **Code**:
```cpp
class Solution {
public:
    int maxScore(string s) {
        // Using idea: Zero(Left) + Ones(Right) = Zero(L) + ones(Total) - ones(Left)
        int ones = 0;
        int n = s.length();
        int zeroes = 0;
        int maxDiff = -1;
        for (int i = 0; i < n - 1; i++) {
            if (s[i] == '0') {
                zeroes++;
            } else {
                ones++;
            }
            maxDiff = max(maxDiff, zeroes - ones); 
        }
        if (s[n - 1] == '1') ones++; // Check the last element of the string.
        return maxDiff + ones;
    }
};
```

---

## Complexity Analysis

### Approach 1:
- **Time Complexity**: O(n)  
  (First pass to count `1`s and second pass to compute maximum score).  
- **Space Complexity**: O(1).

### Approach 2:
- **Time Complexity**: O(n)  
  (Single pass with efficient tracking of `zeroes` and `ones` differences).  
- **Space Complexity**: O(1).

---

## Results
| Approach    | Time Complexity | Space Complexity | Remarks                  |
|-------------|-----------------|------------------|--------------------------|
| Approach 1  | O(n)            | O(1)             | Straightforward logic.   |
| Approach 2  | O(n)            | O(1)             | Optimized difference tracking. |

---

## Notes
Both approaches solve the problem effectively. **Approach 2** offers a cleaner and more optimized solution by leveraging the difference metric.

---

## Problem Link
You can find the problem description on LeetCode: [1442. Maximum Score After Splitting a String](https://leetcode.com/problems/maximum-score-after-splitting-a-string/)

---

Happy coding! 💻🔥