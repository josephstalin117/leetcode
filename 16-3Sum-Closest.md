Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

#### Example:
```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

#### Solution
```
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());

        int distance = INT_MAX;
        int sum = nums[0]+nums[1]+nums[2];

        for(int i=0; i<nums.size()-2; ++i) {
            int l = i+1;
            int r = nums.size()-1;
            while(l < r) {
                if(abs(nums[l]+nums[r]+nums[i]-target) < distance) {
                    sum = nums[l]+nums[r]+nums[i];
                    distance = abs(nums[l]+nums[r]+nums[i]-target);
                }

                if(nums[l]+nums[r]+nums[i] == target)
                    return sum;
                else if(nums[l]+nums[r]+nums[i] < target)
                    ++l;
                else
                    --r;
            }
        }

        return sum;
    }
};
```