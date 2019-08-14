Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

#### Example1:
```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

#### Example2:
```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
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
    int maxPathSum(TreeNode* root) {
        if(!root) return 0;
        int ans=INT_MIN;
        helper(root, ans);
        return ans;
    }
    
    int helper(TreeNode* root, int& ans){
        if(!root) return 0;
        int l=max(0, helper(root->left, ans));
        int r=max(0, helper(root->right, ans));
        int sum=l+r+root->val;
        ans=max(ans, sum);
        return max(l, r)+root->val;
    }
};
```