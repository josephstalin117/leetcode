Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

#### Example1:
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

#### Example2:
```
Input: "cbbd"
Output: "bb"
```

#### Solution1
```
//DP
class Solution {
public:
    string longestPalindrome(string s) {
        
        if(s.size()<=1) return s; 
        int start = 0, maxLen = 1, n = s.size();
        bool isPal[1000][1000] = {false};
        
        for(int i=n-1; i>=0; i--) {
            for(int j=i; j<n; j++) {
                if((i+1>j-1 || isPal[i+1][j-1]) && s[i]==s[j]) {
                    isPal[i][j] = true;
                    if(j-i+1>maxLen) {
                        maxLen = j-i+1;
                        start = i;
                    }
                }
            }
        }
        
        return s.substr(start,maxLen);
    }
};
```