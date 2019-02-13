## 	Binary Tree Zigzag Level Order Traversal

http://oj.leetcode.com/problems/binary-tree-zigzag-level-order-traversal/ 

time: O(n), space: O(n)

```
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        //use 2 stacks
        if(!root) return {};
        vector<vector<int>> ans;
        stack<TreeNode*> s1;
        stack<TreeNode*> s2;
        vector<int> cur;
        s1.push(root);
        while(!s1.empty() || !s2.empty()) {
            while(!s1.empty()) {
                TreeNode* node = s1.top(); s1.pop();
                cur.push_back(node->val);
                if(node->left) s2.push(node->left);
                if(node->right) s2.push(node->right);
            }
            if(!cur.empty()) ans.push_back(cur);
            cur.clear();
            while(!s2.empty()) {
                TreeNode* node = s2.top(); s2.pop();
                cur.push_back(node->val);
                if(node->right) s1.push(node->right);
                if(node->left) s1.push(node->left);
            }
            if(!cur.empty()) ans.push_back(cur);
            cur.clear();
        }
        return ans;
    }
};
```
