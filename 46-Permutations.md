Given a collection of distinct integers, return all possible permutations.

#### Example
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### Solution1
backtracking法（回溯法）
我们需要用一个辅助数组来记录当前递归层时，哪些数字已经在上层的递归使用过了。
```
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> allPer;
        if(nums.empty()) return allPer;
        vector<bool> used(nums.size(), false);
        vector<int> per;
        findPermutations(nums, used, per, allPer);
        return allPer;
    }
    
    void findPermutations(vector<int> &nums, vector<bool> &used, vector<int> &per, vector<vector<int>> &allPer){
        if(per.size()==nums.size()){
            allPer.push_back(per);
            return;
        }
        
        for(int i=0; i<nums.size(); i++){
            if(used[i]) continue;
            used[i]=true;
            per.push_back(nums[i]);
            findPermutations(nums, used, per, allPer);
            used[i]=false;
            per.pop_back();
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
