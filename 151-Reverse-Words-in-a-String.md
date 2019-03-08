Given an input string, reverse the string word by word.

#### Example1:
```
Input: "the sky is blue"
Output: "blue is sky the"
```

#### Example2:
```
Input: "  hello world!  "
Output: "world! hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

#### Example3:
```
Input: "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

#### Note:
```
1. A word is defined as a sequence of non-space characters.
2. Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
3. You need to reduce multiple spaces between two words to a single space in the reversed string.
```

#### Solution
```
class Solution {
public:
    string reverseWords(string s) {
        int storeIndex=0;
        int n=s.size();
        reverse(s.begin(), s.end());
        for(int i=0; i<n; ++i){
            if(s[i]!=' '){
                if(storeIndex!=0){
                    s[storeIndex++]=' ';
                }
                int j=i;
                while (j < n && s[j] != ' '){
                    s[storeIndex++] = s[j++];
                }
                reverse(s.begin()+storeIndex-(j-i), s.begin()+storeIndex);
                i=j;
            }
        }
        s.resize(storeIndex);
        return s;

    }
};
```


