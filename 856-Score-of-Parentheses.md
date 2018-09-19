Given a balanced parentheses string S, compute the score of the string based on the following rule:  

1. () has score 1  
2. AB has score A + B, where A and B are balanced parentheses strings.  
3. (A) has score 2 * A, where A is a balanced parentheses string.  

#### Example 1:
```
Input: "()"
Output: 1
```

#### Example 2:
```
Input: "(())"
Output: 2
```

#### Example 3:
```
Input: "()()"
Output: 2
```

#### Example 4:
```
Input: "(()(()))"
Output: 6
```

#### Note:
1. S is a balanced parentheses string, containing only ( and ).
2. 2 <= S.length <= 50

#### Solution1
```
class Solution {
public:
    int scoreOfParentheses(string S) {
        return score(S, 0, S.length() - 1);
    }
    
    int score(string& s, int begin, int end){
        if((end-1)==begin){
            return 1;
        }
        int b=0;
        for(int i=begin;i<end;i++){
            if(s[i]=='(') b++;
            if(s[i]==')') b--;
            if(b==0){
                return score(s, begin, i)+score(s, i+1, end);
            }
        }
        return 2 * score(s, begin + 1, end - 1);
    }
};
```