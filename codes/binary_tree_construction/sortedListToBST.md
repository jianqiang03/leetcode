## Convert Sorted List to Binary Search Tree

http://oj.leetcode.com/problems/convert-sorted-list-to-binary-search-tree/

time: O(n), space: O(logn)

### Solution 1
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

### Solution 2

```
class Solution {
public:
    TreeNode* sortedListToBST(ListNode* head) {
        if(!head) return nullptr;
        current_ = head;
        int count = 0;
        ListNode* cur = head;
        while(cur) {
            count++;
            cur = cur->next;
        }
        return buildTree(0, count-1);
    }
private:
    TreeNode* buildTree(int l, int r) {
        if(l > r) return nullptr;
        int m = (l+r)/2;
        TreeNode* leftChild = buildTree(l, m-1);
        TreeNode* root = new TreeNode(current_->val);
        root->left = leftChild;
        current_ = current_->next;
        root->right = buildTree(m+1, r);
        return root;
    }
private:
    ListNode* current_;
};
```
