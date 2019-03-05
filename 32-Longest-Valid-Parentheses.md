Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

#### Example 1:
```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

#### Example 2:
```
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
```

#### Solution
```
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> q;
        int start=0;
        int ans=0;
        for(int i=0; i<s.length(); i++){
            if(s[i]=='('){
                q.push(i);
            }else{
                if(q.empty()){
                    start=i+1;
                }else{
                    q.pop();
                    ans=max(ans, q.empty()?i-start+1:i-q.top());
                }
            }
        }
        return ans;
    }
};
```