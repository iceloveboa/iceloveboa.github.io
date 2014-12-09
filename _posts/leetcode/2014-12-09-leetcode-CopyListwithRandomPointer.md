---
layout: post
title: Copy List with Random Pointer 
---

* [Copy List with Random Pointer](https://oj.leetcode.com/problems/copy-list-with-random-pointer/)

{% highlight cpp linenos %}
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    RandomListNode *copyRandomList(RandomListNode *head) {
        if (!head) {
            return NULL;
        }
        
        map<RandomListNode*,RandomListNode*> visited;
        
        RandomListNode *re = new RandomListNode(head->label);
        RandomListNode *temp = head;
        visited[head]=re;
        while (temp) {
            if (temp->random) {
                if (!visited[temp->random]) {
                    RandomListNode *t = new RandomListNode(temp->random->label);
                    visited[temp->random]=t;
                    visited[temp]->random=t;
                }else{
                    visited[temp]->random=visited[temp->random];
                }
            }else{
                visited[temp]->random = NULL;
            }
            
            if (temp->next) {
                if (!visited[temp->next]) {
                    RandomListNode *t = new RandomListNode(temp->next->label);
                    visited[temp->next]=t;
                    visited[temp]->next = t;
                }else{
                    visited[temp]->next = visited[temp->next];
                }
            }else{
                visited[temp]->next = NULL;
            }
            
            temp = temp->next;
            
        }

        return re;

    }
};
{% endhighlight %}