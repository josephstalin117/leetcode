Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes. More formally, the property root.val = min(root.left.val, root.right.val) always holds.

Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree.

If no such second minimum value exists, output -1 instead.

#### Example1:
```
Input: 
    2
   / \
  2   5
     / \
    5   7

Output: 5
Explanation: The smallest value is 2, the second smallest value is 5.
```

#### Example2:
```
Input: 
    2
   / \
  2   2

Output: -1
Explanation: The smallest value is 2, but there isn't any second smallest value.
```

This tree is also valid:

```
         5
       /   \
      2     7
     / \   
    1   3
         \
          4
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
    int findSecondMinimumValue(TreeNode* root) {
        if(!root) return -1;
        
        // return BFS(root);        
        return DFS(root, root->val);
    }

    // Return the second smallest number in the (sub-tree)
    // s1 is the smallest value
    int DFS(TreeNode* root, int s1) {
        if(!root) return -1;
        
        // If root's value is already grater than s1, 
        // then all its children's value should be >= s1.
        // Thus root's value is the second smallest one.
        // No need to visit the 
        if(root->val > s1) return root->val;
        
        int sl = DFS(root->left, s1);
        int sr = DFS(root->right, s1);
        
        if(sl == -1) return sr;
        if(sr == -1) return sl;
        
        // Return the smaller one among two subtrees
        return min(sl, sr);
    }
};
```

#### Solution2:
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
    int findSecondMinimumValue(TreeNode* root) {
        if(!root) return -1;

        return BFS(root);
    }

    int BFS(TreeNode* root) {
        if(!root) return -1;
        
        // Smallest value
        int s1 = root->val;
        // Sencond smallest value
        int s2 = INT_MAX;
        bool found = false;
        
        deque<TreeNode*> q;
        q.push_back(root);
        
        while(!q.empty()) {
            TreeNode* node = q.front();
            q.pop_front();
            
            // Keep updating second smallest value
            if(node->val > s1 && node->val < s2) {
                s2 = node->val;
                found = true;
                // No need to add it's children into queue
                continue; 
            }
            
            if(!node->left) continue;
            q.push_back(node->left);
            q.push_back(node->right);
        }
        
        return found?s2:-1;
    }
};
```