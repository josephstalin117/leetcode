Given a binary tree, return all root-to-leaf paths.

#### Note: 
A leaf is a node with no children.

#### Example:
```
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
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
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> res;
        if(!root) return res;
        helper(root, res, to_string(root->val));
        return res;
    }
    
    void helper(TreeNode* root, vector<string>& res, string t){
        if(!root->left && !root->right){
            res.push_back(t);
        }
        if(root->left){
            helper(root->left, res, t+"->"+to_string(root->left->val));
        }
        if(root->right){
            helper(root->right, res, t+"->"+to_string(root->right->val));
        }
    }
};
```