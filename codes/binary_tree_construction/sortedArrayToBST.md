## Convert Sorted List to Binary Search Tree

http://oj.leetcode.com/problems/convert-sorted-array-to-binary-search-tree/ 

time: O(n), space: O(n)

```
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if(nums.empty()) return nullptr;
        return buildTree(nums, 0, nums.size()-1);
    }
private:
    TreeNode* buildTree(vector<int>& nums, int l, int r) {
        if(l > r) return nullptr;
        int m = (l+r)/2;
        TreeNode* root = new TreeNode(nums[m]);
        root->left = buildTree(nums, l, m-1);
        root->right = buildTree(nums, m+1, r);
        return root;
    }
};
```
