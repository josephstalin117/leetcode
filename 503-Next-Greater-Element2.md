Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

#### Example1:
```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.
```

#### Note:
The length of given array won't exceed 10000.

#### Solution
我们可以使用栈来进行优化上面的算法，我们遍历两倍的数组，然后还是坐标i对n取余，取出数字，如果此时栈不为空，且栈顶元素小于当前数字，说明当前数字就是栈顶元素的右边第一个较大数，那么建立二者的映射，并且去除当前栈顶元素，最后如果i小于n，则把i压入栈。因为res的长度必须是n，超过n的部分我们只是为了给之前栈中的数字找较大值，所以不能压入栈，参见代码如下：
```
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        stack<int> s;
        unordered_map<int, int> next;
        for(int num : nums2){
            while(!s.empty() && num > s.top()){
                next[s.top()]=num;
                s.pop();
            }
            s.push(num);
        }
        
        vector<int> ans;
        for(int num : nums1){
            ans.push_back(next.count(num)?next[num]:-1);
        }
        return ans;
    }
};

```
