* [Find Minimum in Rotated Sorted Array](https://oj.leetcode.com/problems/find-minimum-in-rotated-sorted-array/)  
 
```   
class Solution {
public:
    int findMin(vector<int> &num) {
        int result = 0;
        long left = 0;
        long right = num.size()-1;
        long middle;
        while (left <= right) {
            if (left == right) {
                result = num[left];
                break;
            }
            if (num[left]<num[right]) {
                result = num[left];
                break;
            }else{
                middle = (left + right)/2;
                if (left == middle) {
                    left = middle + 1;
                }
                else if (num[left]<num[middle]) {
                    left = middle;
                }else{
                    right = middle;
                }
            }
        }
        return result;
    }
};
```
* [Maximum Product Subarray](https://oj.leetcode.com/problems/maximum-product-subarray/)

```
class Solution {
public:
    int maxProduct(int A[], int n) {
       int result = A[0];
       int mini = A[0];
       int maxi = A[0];
        for(int i=1;i<n;i++)
        {
           int a = min(maxi*A[i],mini*A[i]);
           int b = max(mini*A[i],maxi*A[i]);
           mini = min(A[i],a);
           maxi = max(A[i],b);
           result = max(result,maxi);
        }
        return result;
    }
};
```
* [Reverse Words in a String](https://oj.leetcode.com/problems/reverse-words-in-a-string/)

```
class Solution {
public:
    void reverseWords(string &s) {
        string result;
        istringstream iss(s);
        do{
            string word;
            iss>>word;
            result=word+" "+result;
        }while (iss);
        result = result.substr(1,result.length()-2);
        s=result;
    }
};
```
* [Evaluate Reverse Polish Notation](https://oj.leetcode.com/problems/evaluate-reverse-polish-notation/)

```
class Solution {
public:
    int evalRPN(vector<string> &tokens) {
        stack<int> stack;
        for (int i=0; i<tokens.size(); i++) {
            string s = tokens[i];
            if (s=="+" || s == "-" || s== "*" || s=="/" ) {
                int a = stack.top();
                stack.pop();
                int b = stack.top();
                stack.pop();
                if (s == "+") {
                    stack.push(a+b);
                }else if(s == "-"){
                    stack.push(b-a);
                }else if(s == "*"){
                    stack.push(a*b);
                }else if(s == "/"){
                    stack.push(b/a);
                }
            }else{
                stack.push( atoi(s.c_str()));
            }
        }
        return stack.top();
    }
};
```
* [Max Points on a Line](https://oj.leetcode.com/problems/max-points-on-a-line/)

```
/**
 * Definition for a point.
 * struct Point {
 *     int x;
 *     int y;
 *     Point() : x(0), y(0) {}
 *     Point(int a, int b) : x(a), y(b) {}
 * };
 */
 #include <cmath>
 
class Solution {
public:
    int maxPoints(vector<Point> &points) {
        int maxNum = 0;
        unordered_map<float, int> mp;
        for (int i=0; i< points.size(); i++) {
            mp.clear();
            int dup = 1;
            for (int j = i+1; j<points.size(); j++) {
                if (points[i].x == points[j].x && points[i].y == points[j].y) {
                    dup++;
                    continue;
                }
                
                if (points[i].x == points[j].x) {
                    mp[INT_MAX]++;
                }else{
                    mp[(float)(points[i].y-points[j].y)/(points[i].x-points[j].x)]++;
                }
            }
            
            maxNum = dup > maxNum ? dup : maxNum;
            for (unordered_map<float, int>::iterator it = mp.begin();it!=mp.end();it++)
            {
                if (it->second + dup  > maxNum) {
                    maxNum = it->second+dup;
                }
            }
        }
        
        
        return maxNum;
    }
};
```
* [Sort List](https://oj.leetcode.com/problems/sort-list/)

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
```
* [Insertion Sort List](https://oj.leetcode.com/problems/insertion-sort-list/)

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
```


