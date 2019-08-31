Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

#### Example1:
```
Input:nums = [1,1,1], k = 2
Output: 2
```

#### Note:
1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

#### Solution1
Brute Force
```
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int res = 0, n = nums.size();
        for (int i = 0; i < n; ++i) {
            int sum = nums[i];
            if (sum == k) ++res;
            for (int j = i + 1; j < n; ++j) {
                sum += nums[j];
                if (sum == k) ++res;
            }
        }
        return res;
    }
};
```

#### Solution2
用一个哈希表来建立连续子数组之和跟其出现次数之间的映射，初始化要加入 {0,1} 这对映射，这是为啥呢，因为我们的解题思路是遍历数组中的数字，用 sum 来记录到当前位置的累加和，我们建立哈希表的目的是为了让我们可以快速的查找 sum-k 是否存在，即是否有连续子数组的和为 sum-k，如果存在的话，那么和为k的子数组一定也存在，这样当 sum 刚好为k的时候，那么数组从起始到当前位置的这段子数组的和就是k，满足题意，如果哈希表中事先没有 m[0] 项的话，这个符合题意的结果就无法累加到结果 res 中，这就是初始化的用途。
```
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int res = 0, sum = 0, n = nums.size();
        unordered_map<int, int> m{{0, 1}};
        for (int i = 0; i < n; ++i) {
            sum += nums[i];
            res += m[sum - k];
            ++m[sum]; 
        }
        return res;
    }
};
```