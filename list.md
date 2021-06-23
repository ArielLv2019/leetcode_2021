## reverse Linked List
```
https://leetcode.com/problems/reverse-linked-list/
Given the head of a singly linked list, reverse the list, and return the reversed list.

Example 1:
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

Example 2:
Input: head = [1,2]
Output: [2,1]

Example 3:
Input: head = []
Output: []

```
### 解题思路
++ 首先定义要返回的新链表为空： tail=nullptr;
++ 从头到尾遍历要逆转的链表，将每一个节点查到新链表的头部。head->next = tail, tail = head;
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        
        ListNode* tail = nullptr;
        
        while(head != nullptr){
            //一定要用一个临时值先保存旧链表的下一个要处理的节点
            auto next = head->next; 
            head->next = tail;
            tail = head;
            head = next;
        }
        
        return tail;
    }
};
```
## linked-list-cycle
```
https://leetcode.com/problems/linked-list-cycle/
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.
 
Example 1:
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

Example 2:
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

Example 3:
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```
+ 解题思路
++ Topic： 快慢指针
++ 用两个指针pFast，pSlow，每一次pFast走两步，pSlow走一步，如果两者相遇，就说明有环，返回true；否则返回false
```cpp
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
        ListNode *pSlow=head, *pFast=head;
        while(pFast != nullptr && pFast->next != nullptr){
            pFast = pFast->next->next;
            pSlow = pSlow->next;
            if(pFast == pSlow){
                return true;
            }
        }
        
        return false;
    }
};
``` 
## linked-list-cycle-ii/
```
https://leetcode.com/problems/linked-list-cycle-ii/
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Notice that you should not modify the linked list.

 

Example 1:
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.

Example 2:
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.

Example 3:
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```
+ 解题思路
++ Topic：快慢指针
++ 快慢指针如果相遇，就让慢指针pSlow重新指向头节点，然后快慢指针各移动一步到两者相遇结束。两指针再次相遇的第一个节点就是环的入口
```cpp
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
    ListNode *detectCycle(ListNode *head) {
        ListNode *pSlow=head, *pFast=head;
        while(pFast != nullptr && pFast->next != nullptr){
            pFast = pFast->next->next;
            pSlow = pSlow->next;
            if(pFast == pSlow){
                pSlow = head;
                while(pSlow != pFast){
                    pFast = pFast->next;
                    pSlow = pSlow->next;
                }
                return pSlow;
            }
        }
        return nullptr;
    }
};
```
