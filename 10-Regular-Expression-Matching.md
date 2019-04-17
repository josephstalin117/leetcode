Given an input string (s) and a pattern (p), implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```

The matching should cover the entire input string (not partial).

#### Note

1. s could be empty and contains only lowercase letters a-z.
2. p could be empty and contains only lowercase letters a-z, and characters like `.` or `*`.

#### Example1:
```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

#### Example2:
```
Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

#### Example3:
```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

#### Example4:
```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
```

#### Example5:
```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```

#### Solution
```
class Solution {
public:
    bool isMatch(string s, string p) {
        return isMatch(s.c_str(), p.c_str());
    }
    
private:
    bool isMatch(const char* s, const char* p){
        if (*p == '\0') return *s=='\0';
        
        // normal case, e.g. 'a.b','aaa','a'
        if (p[1] != '*' || p[1] == '\0'){
            //no char to match
            if(*s == '\0') return false;
            
            if(*s == *p || *p == '.'){
                return isMatch(s+1, p+1);
            }else{
                return false;
            }
            
        }else{
            int i = -1;
            while(i == -1 || s[i] == p[0] || p[0] == '.'){
                if(isMatch(s+i+1, p+2)){
                    return true;
                }
                if(s[++i]=='\0'){
                    break;
                }
            }
            return false;
        }
        return false;
    }
};
```