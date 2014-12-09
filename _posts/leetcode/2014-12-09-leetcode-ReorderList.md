---
layout: post
title: Reorder List 
---

* [Reorder List](https://oj.leetcode.com/problems/reorder-list/)

{% highlight cpp linenos %}
class Solution {
public:
    ListNode* findmiddle(ListNode *head){
        ListNode *step1=head;
        ListNode *step2=head->next;
        while (step2!=NULL && step2->next != NULL) {
            step1 = step1->next;
            step2 = step2->next->next;
        }
        ListNode *middle = step1->next;
        step1->next = NULL;
        return middle;
    }
    
    ListNode* reverseList(ListNode *head){
        
        if (head == NULL) {
            return head;
        }
        
        ListNode *pre = NULL;
        ListNode *cur = head;
        ListNode *next;
        while (cur!=NULL) {
            next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
        
        return pre;
    }
    
    ListNode* linkList(ListNode *head1,ListNode *head2){
        if (head1==NULL) {
            return head1;
        }
        ListNode *head=head1;
        ListNode *cur1=head1;
        ListNode *cur2=head2;
        while (cur1!=NULL && cur2!=NULL) {
            ListNode *temp1= cur1->next;
            ListNode *temp2= cur2->next;
            cur1->next=cur2;
            cur2->next=temp1;
            cur1 = temp1;
            cur2 = temp2;
        }
    
        return head;
    }
    
    void reorderList(ListNode *head) {
        ListNode *head1;
        ListNode *head2;
        if (head == NULL) {
            return;
        }
       
        head1 = head;
        head2 = reverseList(findmiddle(head));
        head = linkList(head1, head2);
    }
};
{% endhighlight %}