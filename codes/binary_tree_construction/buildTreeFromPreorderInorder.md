## Construct Binary Tree from Preorder and Inorder Traversal

http://oj.leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/ 

### solution
time: O(nlogn), space: O(logn)

```
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        //key: find breaking point k
        //i,j : starting index of left-tree in preorder and inorder
        if(preorder.empty() || inorder.empty()) return nullptr;
        return build(preorder, inorder, 0, 0, preorder.size());
    }
private:
    TreeNode* build(vector<int>& preorder, vector<int>& inorder, int i, int j, int n) {
        if(n <= 0) return nullptr;
        TreeNode* root = new TreeNode(preorder[i]);
        int k = 0;
        while(inorder[k] != preorder[i]) k++;
        int l = k-j;
        root->left = build(preorder, inorder, i+1, j, l);
        root->right = build(preorder, inorder, i+l+1, k+1, n-l-1);
        return root;
    }
};
```
