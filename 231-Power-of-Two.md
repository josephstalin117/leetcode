Given an integer, write a function to determine if it is a power of two.

#### Example1:
```
Input: 1
Output: true 
Explanation: 2^0 = 1
```

#### Example2:
```
Input: 16
Output: true
Explanation: 2^4 = 16
```

#### Example3:
```
Input: 218
Output: false
```

#### Solution1
直接判断n与n-1相与后的结果是否为0，为0就表示n的二进制表示中只有一个1，否则有多个1。
```
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return n > 0 && !(n & (n - 1));
    }
};
```
