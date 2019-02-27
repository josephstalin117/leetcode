Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.
#### Example1:
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```
![Alt text](./images/141-1.png)

#### Example2:
```
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```
![Alt text](./images/141-2.png)

#### Example3:
```
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```
![Alt text](./images/141-3.png)

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
    bool hasCycle(ListNode *head) {
    	unordered_set<ListNode*> seen;
    	while (head) {
      		if (seen.count(head)) return true;
      		seen.insert(head);
      		head = head->next;
    	}
    	return false;
    }
};
```

#### Solution2
```
//是使用两个指针，一个fast，一个slow。这样如果存在环最终而这回相等，如果不存在环，就会空指针。代码入下：
class Solution {
public:
    bool hasCycle(ListNode *head) {
        auto slow = head;
        auto fast = head;
        while (fast) {
            if (!fast->next) return false;
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) return true;
        }
        return false;
    }
};
```