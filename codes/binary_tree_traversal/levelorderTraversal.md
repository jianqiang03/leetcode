## 	Binary Tree Level Order Traversal

http://oj.leetcode.com/problems/binary-tree-level-order-traversal/ 

### DFS
time: O(n), space: O(n)

```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        //dfs
        if(!root) return {};
        vector<vector<int>> ans;
        dfs(root, 0, ans);
        return ans;
    }
private:
    void dfs(TreeNode* root, int depth, vector<vector<int>>& ans) {
        if(!root) return;
        if(ans.size() <= depth) ans.push_back({});
        ans[depth].push_back(root->val);
        dfs(root->left, depth+1, ans);
        dfs(root->right, depth+1, ans);
    }
};
```
### BFS
time: O(n), space: O(n)

```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        //bfs
        if(!root) return {};
        vector<vector<int>> ans;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            int n = q.size();
            ans.push_back({});
            for(int i=0; i<n; ++i) {
                TreeNode* node = q.front(); q.pop();
                ans.back().push_back(node->val);
                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);
            }
        }
        return ans;
    }
};
```
