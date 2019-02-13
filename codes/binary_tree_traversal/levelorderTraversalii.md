## Binary Tree Level Order Traversal II

http://oj.leetcode.com/problems/binary-tree-level-order-traversal-ii/ 

time: O(n), space: O(n)

```
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        if(!root) return {};
        vector<vector<int>> ans;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            int n = q.size();
            vector<int> curr;
            for(int i=0; i<n; ++i) {
                TreeNode* node = q.front(); q.pop();
                curr.push_back(node->val);
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
            ans.insert(ans.begin(), curr);
        }
        return ans;
    }
};
```
