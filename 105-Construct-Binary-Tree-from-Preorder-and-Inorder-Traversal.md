Given preorder and inorder traversal of a tree, construct the binary tree.

#### Note:
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
```

#### Solution
题目中给了一个很关键的条件就是树中没有相同元素，有了这个条件我们就可以在中序遍历中也定位出根节点的位置，并以根节点的位置将中序遍历拆分为左右两个部分，分别对其递归调用原函数。
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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return buildTree(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1);
    }
    
    TreeNode *buildTree(vector<int> &preorder, int pLeft, int pRight, vector<int> &inorder, int iLeft, int iRight) {
        if(pLeft > pRight || iLeft > iRight) return NULL;
        int i=0;
        for(i = iLeft; i<=iRight;++i){
            if(preorder[pLeft] == inorder[i]) break;
        }
        TreeNode *cur = new TreeNode(preorder[pLeft]);
        cur->left = buildTree(preorder, pLeft+1, pLeft+i-iLeft, inorder, iLeft, i-1);
        cur->right = buildTree(preorder, pLeft+i-iLeft+1, pRight, inorder, i+1, iRight);
        return cur;
    }
};
```