Given a collection of numbers that might contain duplicates, return all possible unique permutations.

#### Example
```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

#### Solution
backtracking法（回溯法）
通过排序 + 每层递归跳过重复数字。注意这里的重复数字指的是一直到当前递归层，还未被使用的数字中的重复。
```
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> allPer;
        if(nums.empty()) return allPer;
        sort(nums.begin(), nums.end());
        vector<int> per;
        vector<bool> used(nums.size(), false);
        findPerUniq(nums, used, per, allPer);
        return allPer;
    }
    
    void findPerUniq(vector<int> &nums, vector<bool> &used, vector<int> &per, vector<vector<int>> &allPer){
        if(per.size()==nums.size()){
            allPer.push_back(per);
            return;
        }
        
        for(int i=0; i<nums.size(); i++){
            if(used[i]) continue;
            if(i>0 && nums[i]==nums[i-1] && !used[i-1]) continue;
            used[i]=true;
            per.push_back(nums[i]);
            findPerUniq(nums, used, per, allPer);
            per.pop_back();
            used[i]=false;
        }
    }
};
```

#### Solution2
当只有1时候：[1]
当加入2以后：[2, 1], [1, 2]
当加入3以后：[3, 2, 1], [2, 3, 1], [2, 1, 3], [3, 1, 2], [1, 3, 2], [1, 2, 3]
前3个permutation分别对应将3插入[2, 1]的0, 1, 2的位置。同理后3个为插入[1, 2]的。因此可以用逐个插入数字来构造所有permutations。
```
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
       vector<vector<int>> allPer;
        if(nums.empty()) return allPer;
        allPer.push_back(vector<int>(1,nums[0]));
        
        for(int i=1; i<nums.size(); i++) {
            int n = allPer.size();
            for(int j=0; j<n; j++) {
                for(int k=0; k<allPer[j].size(); k++) {
                    vector<int> per = allPer[j];
                    per.insert(per.begin()+k, nums[i]);
                    allPer.push_back(per);
                }
                allPer[j].push_back(nums[i]);
            }
        }
        return allPer;
    }
};
```
