# Day 2 - LeetCode Problem 2559: Count Vowel Strings in Ranges 🌟

## Problem Description 📜
You are given a 0-indexed array of strings `words` and a 2D array of integers `queries`.

Each query `queries[i] = [li, ri]` asks us to find the number of strings present in the range `li` to `ri` (both inclusive) of `words` that start and end with a vowel.

Return an array `ans` of size `queries.length`, where `ans[i]` is the answer to the `i-th` query.

### Notes 📝:
- The vowel letters are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`.

---

## Examples 🔍

### Example 1:
**Input**:  
`words = ["aba", "bcb", "ece", "aa", "e"]`  
`queries = [[0,2], [1,4], [1,1]]`  

**Output**:  
`[2, 3, 0]`  

**Explanation**:  
- The strings starting and ending with a vowel are `"aba"`, `"ece"`, `"aa"`, and `"e"`.  
- For query `[0,2]`, the answer is `2` (`"aba"` and `"ece"`).  
- For query `[1,4]`, the answer is `3` (`"ece"`, `"aa"`, `"e"`).  
- For query `[1,1]`, the answer is `0`.  

### Example 2:
**Input**:  
`words = ["a", "e", "i"]`  
`queries = [[0,2], [0,1], [2,2]]`  

**Output**:  
`[3, 2, 1]`  

**Explanation**:  
- Every string satisfies the conditions.  

---

## Constraints ⚠️:
- `1 <= words.length <= 10^5`
- `1 <= words[i].length <= 40`
- `words[i]` consists only of lowercase English letters.
- `sum(words[i].length) <= 3 * 10^5`
- `1 <= queries.length <= 10^5`
- `0 <= li <= ri < words.length`

---

## Approach 🚀

### Optimized Prefix Sum Solution
- **Logic**:
  1. Identify if each word starts and ends with a vowel (`a, e, i, o, u`).
  2. Use a **prefix sum array** to efficiently calculate the number of valid vowel strings in any subarray.
  3. For each query `[li, ri]`, compute the result using:
     ```cpp
     result = prefixSum[ri] - (li > 0 ? prefixSum[li - 1] : 0)
     ```

- **Implementation Steps**:
  1. Create a set of vowels for quick lookup.
  2. Traverse the `words` array and build a `prefixSum` array to count valid strings up to each index.
  3. For each query, compute the result using the difference of prefix sums.

---

## Code 💻:
```cpp
class Solution {
public:
    vector<int> vowelStrings(vector<string>& words, vector<vector<int>>& queries) {
        vector<int> ans(queries.size());
        unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u'};
        vector<int> prefixSum(words.size());
        int sum = 0;

        // Build prefix sum array
        for (int i = 0; i < words.size(); i++) {
            string currentWord = words[i];
            if (vowels.count(currentWord[0]) && vowels.count(currentWord[currentWord.size() - 1])) {
                sum++;
            }
            prefixSum[i] = sum;
        }

        // Process each query
        for (int i = 0; i < queries.size(); i++) {
            vector<int> currentQuery = queries[i];
            int start = currentQuery[0];
            int end = currentQuery[1];
            ans[i] = prefixSum[end] - (start > 0 ? prefixSum[start - 1] : 0);
        }
        
        return ans;
    }
};
```

---

## Complexity Analysis 🧠

### Time Complexity:
- **Building Prefix Sum**: O(n), where `n` is the size of the `words` array.  
- **Processing Queries**: O(q), where `q` is the number of queries.  
- **Total**: O(n + q).

### Space Complexity:
- O(n) for the `prefixSum` array.  

---

## Results 📊
| Step            | Time Complexity | Space Complexity | Remarks                  |
|------------------|-----------------|------------------|--------------------------|
| Build Prefix Sum | O(n)            | O(n)             | Efficient preprocessing. |
| Process Queries  | O(q)            | O(1)             | Efficient computation.   |

---

## Problem Link 🔗
You can find the problem description on LeetCode: [Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges/)

---

Happy coding! 💻🔥