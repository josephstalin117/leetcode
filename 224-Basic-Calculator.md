Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open (and closing parentheses), the plus + or minus sign -, non-negative integers and empty spaces .

#### Example1:
```
Input: "1 + 1"
Output: 2
```

#### Example2:
```
Input: " 2-1 + 2 "
Output: 3
```

#### Example3:
```
Input: "(1+(4+5+2)-3)+(6+8)"
Output: 23
```

#### Note:
1. You may assume that the given expression is always valid.
2. Do not use the eval built-in library function.

#### Solution
我们需要一个栈来辅助计算，用个变量sign来表示当前的符号，我们遍历给定的字符串s，如果遇到了数字，由于可能是个多位数，所以我们要用while循环把之后的数字都读进来，然后用sign*num来更新结果res；如果遇到了加号，则sign赋为1，如果遇到了符号，则赋为-1；如果遇到了左括号，则把当前结果res和符号sign压入栈，res重置为0，sign重置为1；如果遇到了右括号，结果res乘以栈顶的符号，栈顶元素出栈，结果res加上栈顶的数字，栈顶元素出栈。
```
class Solution {
public:
    int calculate(string s) {
        int res=0;
        int sign=1;
        int n=s.size();
        stack<int> st;
        for(int i=0; i<n; ++i){
            char c=s[i];
            if(c>='0'){
                int num=0;
                while(i<n && s[i]>='0'){
                    num=num*10+(s[i++]-'0');
                }
                res += sign * num;
                --i;
            }else if(c=='+'){
                sign = 1;
            }else if(c=='-'){
                sign = -1;
            }else if(c=='('){
                st.push(res);
                st.push(sign);
                res = 0;
                sign = 1;
            }else if(c==')'){
                res *=st.top();
                st.pop();
                res +=st.top();
                st.pop();
            }
        }
        return res;
    }
};
```