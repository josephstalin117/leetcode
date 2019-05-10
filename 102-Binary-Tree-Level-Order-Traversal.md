Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```

#### Solution
定义一个队列记录当前一层的节点，一开始为根节点。每一次历遍某一层的时候，先计算队列里的元素数量，然后用这个数量（size）控制处理多少节点，因为队列每次处理一个节点的时候，同时要将该节点的左右子节点压入队列，也就是说队列中还存在下一层的节点，所以要通过size来控制，只处理当前层的节点。当所有节点都处理完之后，队列为空，推出循环。
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            vector<int> temp;
            auto size=q.size();
            while(size--){
                TreeNode* node=q.front();
                q.pop();
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
                temp.push_back(node->val);
            }
            res.push_back(temp);
        }
        return res;
    }
};
```