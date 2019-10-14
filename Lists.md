# Linked Lists

+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Linked List Cycle](#linked-list-cycle)
+ [Linked List Cycle II](#linked-list-cycle-ii)
+ [Reorder List](#reorder-list)
+ [Sort List](#sort-list)
+ [Remove Linked List Elements](#remove-linked-list-elements)
+ [Reverse Linked List](#reverse-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Delete Node in a Linked List](#delete-node-in-a-linked-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)

## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode prehead(0);
        ListNode *deleteList = &prehead, *buf, *listEnd = head;
        deleteList->next = head;        
        while(n--)
            listEnd = listEnd->next;
        while(listEnd){
            listEnd = listEnd->next;
            deleteList = deleteList->next;
        }
        buf = deleteList->next->next;
        delete(deleteList->next);
        deleteList->next = buf;     
        return prehead.next;         
    }
};
```
## Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/
```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;        
        ListNode *first = l1, *second = l2, *buf;
        if(first->val >= second->val){
            buf = l2;
            second = second->next;
        }
        else{
            buf = l1;
            first = first->next;
        }        
        while(first != NULL && second != NULL){
            if(first->val > second->val){
                buf->next = second;
                second = second->next;
            }
            else{
                buf->next = first;
                first = first->next;
            }
	    buf = buf->next;
        }
        if(first == NULL)
            buf->next = second;
        else
            buf->next = first;
        if(l1->val < l2->val)
            return l1;
        return l2;        
    }
};
```
## Linked List Cycle
https://leetcode.com/problems/linked-list-cycle/
```C++
class Solution {
public:
    bool hasCycle(ListNode *head){
        ListNode *fast = head, *slow = head;
	while(fast != NULL && fast->next != NULL && fast != slow){
	    slow = slow->next;
	    fast = fast->next->next;
	}
	if (fast == NULL || fast->next == NULL)
            return false;
        return true;        
    }
};
```
## Linked List Cycle II
https://leetcode.com/problems/linked-list-cycle-ii/
```C++
class Solution {
public:
     ListNode *detectCycle(ListNode *head) {
        ListNode *fast = head, *slow = head;
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if(fast == slow)
            break;
        }
        if (fast == NULL || fast->next == NULL)
            return NULL;
        slow = head;
        while (fast != slow){
            fast = fast->next;
            slow = slow->next;
        }
        return slow;       
    }
};
```
## Reorder List
https://leetcode.com/problems/reorder-list/
```C++
class Solution {
public:
    void reorderList(ListNode* head) {        
        if(head == NULL || head->next == NULL || head->next->next == NULL)
            return;
        ListNode *first = head, *second = middleNode(head), *buf1 = head, *buf2;
        buf2 = second = reverseList(second);
        while(first != NULL && second != NULL){
            buf1 = first->next;
            buf2 = second->next;
            first->next = second;
            second->next = buf1;
            first = buf1;
            second = buf2;
        }   
    }
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head->next;
        while (fast && fast->next) {              
            fast = fast->next->next;           
            head = head->next;
        }
        fast = head->next;
        head->next = NULL;
        return fast;
    }
    ListNode* reverseList(ListNode* head) {
        ListNode* left = NULL, *cur = head, *right;     	
        while(cur != NULL){
            right = cur->next;
            cur->next = left;
            left = cur;
            cur = right;
        }          
        return left;   
    } 
};
```
## Sort List
https://leetcode.com/problems/sort-list/
```C++
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        if(head == NULL || head->next == NULL)
            return head;
        return mergeTwoLists(sortList(head), sortList(middleNode(head)));
    }
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head->next;
        while (fast && fast->next) {              
            fast = fast->next->next;           
            head = head->next;
        }
        fast = head->next;
        head->next = NULL;
        return fast;
    }
     ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;        
        ListNode *first = l1, *second = l2, *buf;
        if(first->val >= second->val){
            buf = l2;
            second = second->next;
        }
        else{
            buf = l1;
            first = first->next;
        }        
        while(first != NULL && second != NULL){
            if(first->val > second->val){
                buf->next = second;
                second = second->next;
            }
            else{
                buf->next = first;
                first = first->next;
            }
	    buf = buf->next;
        }
        if(first == NULL)
            buf->next = second;
        else
            buf->next = first;
        if(l1->val < l2->val)
            return l1;
        return l2;        
    }
};
```
## Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/
```C++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        while(head && head->val == val)
            head = head->next;
        if(head == NULL)
            return NULL;
        ListNode* cur = head;
        while(cur->next != NULL){
            if(cur>next->val == val)
                cur->next = cur->next->next;
            else
                cur = cur->next;            
        }
        return head;   
    }
};
```
## Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/
```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* left = NULL, *cur = head, *right;        	
        while(cur != NULL){
            right = cur->next;
            cur->next = left;
            left = cur;
            cur = right;
        }          
        return left;   
    }   
};
```
## Palindrome Linked List
https://leetcode.com/problems/palindrome-linked-list/
```C++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if(head == NULL)
            return true;
        ListNode *first = head, *second = middleNode(head);
        second = reverseList(second);
        while(second){
            if(first->val != second-> val)
                return false;
            first = first->next;
            second = second->next;
        }
        return true;
    }
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head->next;
        while (fast && fast->next) {              
            fast = fast->next->next;           
            head = head->next;
        }
        fast = head->next;
        head->next = NULL;
        return fast;
    }
    ListNode* reverseList(ListNode* head) {
        ListNode* left = NULL, *cur = head, *right;        	
	
        while(cur != NULL){
            right = cur->next;
            cur->next = left;
            left = cur;
            cur = right;
        }          
        return left;   
    }   
};
```
## Delete Node in a Linked List
https://leetcode.com/problems/delete-node-in-a-linked-list/
```C++
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;        
    }
};
```
## Middle of the Linked List
https://leetcode.com/problems/middle-of-the-linked-list/
```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
    	ListNode* fast = head->next;
        while (fast && fast->next) {
            head = head->next;    
            fast = fast->next->next;       
        }
        if(fast)
            head = head->next;
      return head;
    }
};
```
## Intersection of Two Linked Lists
https://leetcode.com/problems/intersection-of-two-linked-lists/
```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA == NULL || headB == NULL)
            return NULL;
        ListNode *listA = headA, *listB = headB;
        int i = 0,j = 0, k;
        while(listA->next != NULL){
            listA = listA->next;
            i++;
        }
        while(listB->next != NULL){
            listB = listB->next;
            j++;
        }
        if(listA != listB)
            return 0;
        listA = headA, listB = headB;
        if(j <= i){
            k = i - j;
            for(i = 0; i < k; i++)
                listA = listA->next;
            while(listA != listB)
                listA = listA->next, listB = listB->next;
            return listA;            
        }
        else{
            k = j - i;
            for(j = 0; j < k; j++)
                listB = listB->next;
            while(listA != listB)
                listA = listA->next, listB = listB->next;
            return listB;
        }        
    }
};
```
