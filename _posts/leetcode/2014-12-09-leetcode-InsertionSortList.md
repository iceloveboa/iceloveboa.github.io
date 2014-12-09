---
layout: post
title: Insertion Sort List 
---

* [Insertion Sort List](https://oj.leetcode.com/problems/insertion-sort-list/)

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
    ListNode *insertionSortList(ListNode *head) {
        if (head == NULL || head -> next == NULL) {
            return head;
        }
        
        ListNode *cur = head -> next;
        head -> next = NULL;
        
        while (cur != NULL) {
            
             ListNode *next = cur -> next;
            
            ListNode *temp = head;
            ListNode *pre = temp;
            while (temp != NULL) {
                if (temp -> val > cur -> val) {
                    if (temp == head) {
                        cur -> next = head;
                        head = cur;
                    }else{
                        cur -> next = temp;
                        pre -> next = cur;
                    }
                    break;
                }else{
                    if (temp->next == NULL) {
                        temp -> next = cur;
                        cur -> next = NULL;
                        break;
                    }else{
                        pre = temp;
                        temp = temp -> next;
                    }
                }
            }

            cur = next;
        }
        
        return head;
        
        
    }
};
{% endhighlight %}