Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

#### Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

#### Solution
```
bool cmp(pair<int,int> &p1, pair<int,int> &p2) {
    return p1.first < p2.first;
}

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<pair<int,int>> v;
        for(int i=0; i<nums.size(); i++){
            v.push_back(make_pair(nums[i], i));
        }
        sort(v.begin(), v.end(), cmp);

        int i = 0;
        int j = v.size()-1;
        vector<int> res;
        while(i < j) {
            int sum = v[i].first + v[j].first;
            if(sum == target) {
                res.push_back(v[i].second);
                res.push_back(v[j].second);
                break;
            }
            else if(sum < target)
                ++i;
            else
                --j;
        }

        sort(res.begin(), res.end());

        return res;
    }
};
```