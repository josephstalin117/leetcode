Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

####Note: 

1. The same word in the dictionary may be reused multiple times in the segmentation.
2. You may assume the dictionary does not contain duplicate words.

#### Example1:
```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

#### Example2:
```
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

#### Example3:
```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```


#### Solution
建一个数组用于存到第i个位置为止能不能用wordDict里的词表示出来，能为true，不能为false。当遍历到第i个位置时，检查在它之前的位置j为true或者false，如果为true，则检查从i到j的字符串是不是在wordDict中。
```
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        if (wordDict.size() == 0) {
            return false;
        }

        vector<bool> endHere(s.size() + 1, false);
        endHere[0] = true;

        for (int i = 1; i <= s.size(); i++) {
            for (int j = i - 1; j >= 0; j--) {
                if (endHere[j]) {
                    string word = s.substr(j, i - j);
                    if (find(wordDict.begin(), wordDict.end(), word) != wordDict.end()) {
                        endHere[i] = true;
                        break;
                    }
                }
            }
        }
        return endHere[s.size()];
    }
};
```
