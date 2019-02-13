## Binary Tree Preorder Traversal

http://oj.leetcode.com/problems/binary-tree-preorder-traversal/

### Recursion solution
time: O(n), space: O(logn)

```
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        preorderTraversal(root, ans);
        return ans;
    }
private:
    void preorderTraversal(TreeNode* root, vector<int>& ans) {
        if(!root) return;
        ans.push_back(root->val);
        preorderTraversal(root->left, ans);
        preorderTraversal(root->right, ans);
    }
};
```
### Iterative solution
time: O(n), space: O(logn)

```
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        if(!root) return {};
        vector<int> ans;
        stack<TreeNode*> s;
        while(root || !s.empty()) {
            if(root) {
                s.push(root);
                ans.push_back(root->val);
                root = root->left;
            }
            else {
                root = s.top(); s.pop();
                root = root->right;
            }
        }
        return ans;
    }
};
```
