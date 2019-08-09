Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

#### Note: 
A leaf is a node with no children.

#### Example1:
Given the below binary tree and sum = 22,
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```
Return:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

#### Solution
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> res;
        vector<int> out;
        helper(root, sum, out, res);
        return res;
    }
    
    void helper(TreeNode* node, int sum, vector<int>& curr, vector<vector<int>>& res){
        if(node==nullptr) return;
        if(node->right==nullptr && node->left==nullptr){
            if(sum==node->val){
                res.push_back(curr);
                res.back().push_back(node->val);
            }    
            return;
        }
        
        curr.push_back(node->val);
        int new_sum= sum- node->val;
        helper(node->left, new_sum, curr, res);
        helper(node->right, new_sum, curr, res);
        curr.pop_back();
        
    }
};
```