---
layout: post
title: Sort List 
---

* [Sort List](https://oj.leetcode.com/problems/sort-list/)

{% highlight cpp linenos %}
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
    ListNode *findMiddle(ListNode *node){
        ListNode *fast=node;
        ListNode *slow=node;
        while (fast->next != NULL && fast->next->next != NULL) {
            slow = slow -> next;
            fast = fast -> next -> next;
        }
        return slow;
    }
    ListNode *sortList(ListNode *head) {
        if (head == NULL || head -> next == NULL) {
            return head;
        }
        
        ListNode *middle = findMiddle(head);
        ListNode *next = middle -> next;
        middle -> next = NULL;
        return mergeList(sortList(head),sortList(next));
    }
    
    ListNode *mergeList(ListNode *list1,ListNode *list2){
        ListNode *re =new ListNode(-1);
        ListNode *cur = re;
        while (list1 != NULL && list2 != NULL) {
            if (list1 -> val < list2 -> val) {
                cur -> next = list1 ;
                list1 = list1 -> next;
            }else{
                cur -> next = list2;
                list2 = list2 -> next;
            }
            cur = cur -> next;
        }
        
        cur ->next = list1 != NULL ? list1 : list2 ;
        return re->next;
        
    }
    
};
{% endhighlight %}