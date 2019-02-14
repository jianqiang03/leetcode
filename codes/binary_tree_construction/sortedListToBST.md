## Convert Sorted List to Binary Search Tree

http://oj.leetcode.com/problems/convert-sorted-list-to-binary-search-tree/

time: O(n), space: O(logn)

```
class Solution {
public:
    TreeNode* sortedListToBST(ListNode* head) {
        if(!head) return nullptr;
        return buildTree(head, nullptr);
    }
private:
    TreeNode* buildTree(ListNode* head, ListNode* tail) {
        if(head == tail) return nullptr;
        ListNode* fast = head, *slow = head;
        while(fast != tail && fast->next != tail) {
            slow = slow->next;
            fast = fast->next->next;
        }
        TreeNode* root = new TreeNode(slow->val);
        root->left = buildTree(head, slow);
        root->right = buildTree(slow->next, tail);
        return root;
    }
};
```
