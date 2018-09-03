Given an array of size n, find the majority element. The majority element is the element that appears more than n/2 times.

You may assume that the array is non-empty and the majority element always exist in the array.
#### Example1:
```
Input: [3,2,3]
Output: 3
```

#### Example2:
```
Input: [2,2,1,1,1,2,2]
Output: 2
```

#### Solution1
```
//投票算法，因为符合的众数总是存在。所以没出现一对不一样的就可以忽视这一对。我们可以用计数表示，来一个数字，如果和candidate相同那么count++，否则count--，如果count为零了，那么candidate就是下一个数。最后candidate就是众数了。
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int nTimes = 0;
        int candidate = 0;
        for(int i = 0; i < num.size(); i ++){
            if(nTimes == 0){
                candidate = num[i];
                nTimes = 1;
            }else{
                if(candidate == num[i]){
                    nTimes ++;
                }else{
                    nTimes --;
                }
            }
        }
        return candidate;
    }
};
```

#### Solution2
```
//因为给定的是32位数，并且众数一定存在，那么每一位去考虑的话，对于每一位1或者0多的肯定是属于众数的。这样就知道众数了。
class Solution {
public:
    int majorityElement(vector<int> &num) {
        int bitCnt[32];
        memset(bitCnt, 0, sizeof(bitCnt));
        
        for (int i = 0; i < num.size(); i++)
        {
            for (int j = 0; j < 32; j++)
            {
                if (num[i] & (1 << j))
                    bitCnt[j]++;
            }
        }
        
        int ans = 0;
        for (int i = 0; i < 32; i++)
        {
            if (bitCnt[i] > num.size()/2)
                ans += (int)pow(2, i);
        }
        return ans;
    }
}
```