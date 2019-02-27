Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

#### Example1:
```
Input: "()"
Output: true
```

#### Example2:
```
Input: "()[]{}"
Output: true
```

#### Example3:
```
Input: "(]"
Output: false
```

#### Example4:
```
Input: "([)]"
Output: false
```

#### Example5:
```
Input: "{[]}"
Output: true
```

#### Solution
```
class Solution {
public:
    bool isValid(string s) {
        if(s.length()==1||s.length()%2==1||s[0]==')'||s[0]==']'||s[0]=='}'){
            return false;
        }
        if(s.length()==0){
            return true;
        }
        stack<char> v;
        for(int i=0;i<s.length();i++){
            if(s[i]=='('||s[i]=='['||s[i]=='{'){
                v.push(s[i]);
            }
            if(s[i]==')'||s[i]==']'||s[i]=='}'){
                char temp=v.top();
                v.pop();
                if((s[i]==')' && temp=='(')||(s[i]==']' && temp=='[')||(s[i]=='}' && temp=='{')){
                    continue;
                }else{
                    return false;
                }
                
            }
        }
        return v.empty();
    }
};
```
