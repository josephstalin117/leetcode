Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

#### Note:
1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

#### Example1:
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

#### Example2:
```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```


#### Solution
```
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        const int sum=std::accumulate(nums.begin(), nums.end(), 0);
        if(sum % 2!=0) return false;
        vector<int> dp(sum+1, 0);
        dp[0]=1;
        for(const int num:nums){
            for(int i=sum; i>=0; --i)
                if(dp[i]) dp[i+num]=1;
            if(dp[sum/2]) return true;
        }
        return false;
    }
};
```
