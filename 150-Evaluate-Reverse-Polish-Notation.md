Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are `+, -, *, /`. Each operand may be an integer or another expression.

#### Example1:
```
Input: ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

#### Example2:
```
Input: ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

#### Example3:
```
Input: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

#### Note:
1. Division between two integers should truncate toward zero.
2. The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.

#### Solution
```
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> s;
        string operators="+-*/";
        int num1=0;
        int num2=0;
        
        for(int i=0; i<tokens.size(); ++i){
            int pos=operators.find(tokens[i]);
            if(pos==string::npos){
                s.push(atoi(tokens[i].c_str()));
            }else{
                num2=s.top();
                s.pop();
                num1=s.top();
                s.pop();
                
                if(tokens[i]=="+"){
                    s.push(num1+num2);
                }else if(tokens[i]=="-"){
                    s.push(num1-num2);
                }else if(tokens[i]=="*"){
                    s.push(num1*num2);
                }else{
                    if(num2!=0){
                        s.push(num1/num2);
                    }
                }
            }
        }
        return s.top();
    }
};
```


