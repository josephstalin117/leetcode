Given a singly linked list, determine if it is a palindrome.

#### Example1:
```
Input: 1->2
Output: false
```

#### Example2:
```
Input: 1->2->2->1
Output: true
```

#### Follow up:
Could you do it in O(n) time and O(1) space?

#### Solution
1. use fast / slow pointers to find the middle node and see whether the list has odd/even number of elements.
2. Reverse the right half the list, and compare with the left half
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
    bool isPalindrome(ListNode* head) {
        ListNode* slow=head;
        ListNode* fast=head;
        while(fast && fast->next){
            slow=slow->next;
            fast=fast->next->next;
        }
        if(fast){
            slow=slow->next;
        }
        slow=reverse(slow);
        while(slow){
            if(slow->val!=head->val){
                return false;
            }
            slow=slow->next;
            head=head->next;
        }
        return true;
    }
private:
    ListNode* reverse(ListNode* head){
        ListNode* prev=nullptr;
        ListNode* next=nullptr;
        while(head){
            next=head->next;
            head->next=prev;
            prev=head;
            head=next;
        }
        return prev;
    }
};
```