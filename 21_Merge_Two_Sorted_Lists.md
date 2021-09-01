# 21. Merge Two Sorted Lists
###### tags: `Leetcode`
###### Difficulty: easy
### Description

>**Problem**
>Merge two sorted linked lists and return it as a sorted list.   
>The list should be made by splicing together the nodes of the first two lists.

>**Example**
>1.
>Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
>2.
>Input: l1 = [], l2 = []
Output: []
>3.
>Input: l1 = [], l2 = [0]
Output: [0]

>**Given**
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
```


### Solution 
* DummyHeadNode with Iteration

Runtime: 4 ms, faster than 83.05% of C online submissions for Merge Two Sorted Lists.  
Memory Usage: 6.2 MB, less than 59.08% of C online submissions for Merge Two Sorted Lists.

```c
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode*now_node;  
    struct ListNode new_head={
        .val = 0,
        .next= NULL
    };
    now_node = &new_head;
     
    if(l1 == l2 && l2 == NULL)
        return NULL;
   
    while(l1 && l2){
        if(l2->val < l1->val){
            now_node->next = l2;
            now_node = l2;
            l2 = l2->next; 
        }
        else{
            now_node->next = l1;
            now_node = l1;
            l1 = l1->next;
        }     
    }

    if(!l2)
        now_node->next = l1;   
    if(!l1)
        now_node->next = l2;
    
    return new_head.next;          
}
```

*  Recursion

Runtime: 5 ms, faster than 9.82% of C online submissions for Merge Two Sorted Lists.  
Memory Usage: 6.2 MB, less than 43.97% of C online submissions for Merge Two Sorted Lists.

```c
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* node = NULL;
    if (!l1)
        return l2;
    if (!l2)
        return l1;
    if (l1->val < l2->val){
        node = l1;
        node->next = mergeTwoLists(l1 = l1->next,l2);
    }
    else{
        node = l2;
        node->next = mergeTwoLists(l1,l2 = l2->next);
    }   
    return node;
}
```
