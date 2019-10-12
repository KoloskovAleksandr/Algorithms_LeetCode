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
	while(Achill != NULL && Achill->next != NULL && Achill != slow){
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
        ListNode *first = head, *second = middleNode(head), *tort1 = head, *tort2;
        tort2 = second = reverseList(second);
        while(first != NULL && second != NULL){
            tort1 = first->next;
            tort2 = second->next;
            first->next = second;
            second->next = tort1;
            first = tort1;
            second = tort2;
        }   
    }
    ListNode* middleNode(ListNode* head) {
        ListNode* tort = head, *buf;
        int length = 0;
        while(tort != NULL){
            tort = tort->next;
            length++;
        }
        if(length % 2)
            length = length / 2 + 1;
        else
            length = length / 2;
        tort = head;
        for(int i = 0; i < length - 1; i++)
            tort = tort->next;
            buf = tort->next;
            tort->next = NULL; 
        return buf;
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
        ListNode* tort = head, *buf;
        int length = 0;
        while(tort != NULL){
            tort = tort->next;
            length++;
        }
        length = length / 2;
        tort = head;
        for(int i = 0; i < length - 1; i++)
            tort = tort->next;
            buf = tort->next;
            tort->next = NULL; 
        return buf;
    }
     ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL && l2 == NULL)
            return NULL;
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;
        
        ListNode *i = l1, *j = l2, *k;
        if(i->val >= j->val){
            k = l2;
            j = j->next;
        }
        else{
            k = l1;
            i = i->next;
        }        
        while(i != NULL && j != NULL){
            if(i->val > j->val){
                k->next = j;
                j = j->next;
                k = k->next;
            }
            else{
                k->next = i;
                i = i->next;
                k = k->next;
            }
        }
        if(i == NULL)
            k->next = j;
        else
            k->next = i;
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
        ListNode* tort = head;
        while(tort->next != NULL){
            if(tort->next->val == val)
                tort->next = tort->next->next;
            else
                tort = tort->next;            
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
        int i = 1;
        ListNode *first = head, *second = middleNode(head);
        second = reverseList(second);
        while(first && second && i){
            if(first->val != second-> val)
                i = 0;
            first = first->next;
            second = second->next;
        }
        if(i)
            return true;
        return false;       
    }
    ListNode* middleNode(ListNode* head) {
        ListNode* tort = head, *buf;
        int length = 0;
        while(tort != NULL){
            tort = tort->next;
            length++;
        }
        if(length % 2)
            length = length / 2 + 1;
        else
            length = length / 2;
        tort = head;
        for(int i = 0; i < length - 1; i++)
            tort = tort->next;
            buf = tort->next;
            tort->next = NULL; 
        return buf;
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
        ListNode* tort = head;
        int length = 0;
        while(tort != NULL){
            tort = tort->next;
            length++;
        }
        length = length / 2;
        tort = head;
        for(int i = 0; i < length; i++)
            tort = tort->next;
        return tort;
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
