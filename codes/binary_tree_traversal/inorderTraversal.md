### Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

Recursion solution:
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
Iterative solution:
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
