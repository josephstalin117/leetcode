Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

Given binary search tree:  root = [6,2,8,0,4,7,9,null,null,3,5]
![Alt text](./images/236.png)

#### Example1:
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

#### Example2:
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

#### Note:
1. All of the nodes' values will be unique.
2. p and q are different and both values will exist in the BST.

#### Solution
通过先序遍历二叉树，先判断当前遍历的节点是否为p/q,如果是则直接返回当前节点，否则继续遍历左子树、右子树，如果左子树返回结果和右子树返回结果同时存在，说明当前节点为最近公共祖先；否则判断左子树返回结果是否为空，如果不为空则返回左子树遍历结果，为空就返回右子树遍历结果
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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root || root==p || root==q) return root;
        TreeNode* l=lowestCommonAncestor(root->left, p, q);
        TreeNode* r=lowestCommonAncestor(root->right, p, q);
        if(l && r) return root;
        return l?l:r;
    }
};
```