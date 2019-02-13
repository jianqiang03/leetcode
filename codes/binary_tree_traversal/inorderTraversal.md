## Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

### Recursion solution
time: O(n), space: O(logn)

```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        inorderTraversal(root, ans);
        return ans;
    }
private:
    void inorderTraversal(TreeNode* root, vector<int>& ans) {
        if(!root) return;
        inorderTraversal(root->left, ans);
        ans.push_back(root->val);
        inorderTraversal(root->right, ans);
    }
};
```
### Iterative solution
time: O(n), space: O(logn)
```
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        //iterative
        //time: O(n) space: O(logn)
        if(!root) return {};
        vector<int> ans;
        stack<TreeNode*> s;
        while(root || !s.empty()) {
            if(root) {
                s.push(root);
                root = root->left;
            }
            else {
                root = s.top(); s.pop();
                ans.push_back(root->val);
                root = root->right;
            }
        }
        return ans;
    }
};
```
