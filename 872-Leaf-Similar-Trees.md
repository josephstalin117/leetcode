Consider all the leaves of a binary tree.  From left to right order, the values of those leaves form a leaf value sequence.

![Alt text](./images/872.png)

For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

#### Note:
```
Both of the given trees will have between 1 and 100 nodes.
```

#### Solution1
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
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int> root1Leaf;
        vector<int> root2Leaf;
        getLeaf(root1, root1Leaf);
        getLeaf(root2, root2Leaf);
        
        if(root1Leaf.size()!=root2Leaf.size()){
            return false;
        }
        for(int i=0;i<root1Leaf.size();i++){
            if(root1Leaf[i]!=root2Leaf[i]){
                return false;
            }
        }
        return true;
        
    }
    
    void getLeaf(TreeNode* root, vector<int> &leaf){
        if(root->left){
            getLeaf(root->left, leaf);    
        }
        if(root->right){
             getLeaf(root->right, leaf);
        }
        if(root->left==NULL && root->right==NULL){
            leaf.push_back(root->val);
        }
    }
};
```