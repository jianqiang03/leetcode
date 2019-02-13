## Binary Tree Postorder Traversal

http://oj.leetcode.com/problems/binary-tree-postorder-traversal/

### Recursion solution
time: O(n), space:O(logn)

```
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        postorderTraversal(root, ans);
        return ans;
    }
private:
    void postorderTraversal(TreeNode* root, vector<int>& ans) {
        if(!root) return;
        postorderTraversal(root->left, ans);
        postorderTraversal(root->right, ans);
        ans.push_back(root->val);
    }
};
```
### Iterative solution
time: O(n), space:O(logn)

```
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        if(!root) return {};
        vector<int> ans;
        stack<TreeNode*> s1;
        stack<TreeNode*> s2;
        s1.push(root);
        while(!s1.empty()) {
            root = s1.top(); s1.pop();
            s2.push(root);
            if(root->left) s1.push(root->left);
            if(root->right) s1.push(root->right);
        }
        while(!s2.empty()) {
            root = s2.top(); s2.pop();
            ans.push_back(root->val);
        }
        return ans;
    }
};
```
