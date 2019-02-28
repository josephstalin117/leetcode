Reverse a singly linked list.

#### Example:
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

#### Follow up:
A linked list can be reversed either iteratively or recursively. Could you implement both?

#### Solution1
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;
        ListNode* next;
        while (curr) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
};
```

#### Solution2
通过递归调用，直接进入到最后一个指针元素，此时作为最新的头结点，循环跳出来后，head->next的下一个指向head自己 然后head->next赋值为空，从而完成两个元素之间的调换。newhead从头到尾都是没有变化的，因为没人去改变他，所以在递归返回的时候，也是可以从头到尾的返回同一个数值的。
```
//递归版本
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == NULL || head -> next == NULL){
            return head;
        }
	    ListNode* newHead = reverseList(head -> next);
	    head -> next -> next  = head ;
	    head -> next = NULL;
	    return newHead;
    }
};
```