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

* [LRU Cache](https://oj.leetcode.com/problems/lru-cache/)

```
struct UsedFreq {
    int key;
    int value;
    int times;
    UsedFreq()
    {
        key = 0;
        value = 0;
        times = 0;
    }
    UsedFreq(int _key,int _value,int _times){
        key = _key;
        value = _value;
        times = _times;
    }
};

class LRUCache{
public:
    unordered_map<int,list<UsedFreq>::iterator> _cachs;
    int _capacity;
    int _used;
    list<UsedFreq> its;
    LRUCache(int capacity) {
        _capacity = capacity;
        _cachs.clear();
        its.clear();
        _used = 1;
    }
    
    int get(int key) {
        unordered_map<int,list<UsedFreq>::iterator>::iterator it = _cachs.find(key);
        if (it!= _cachs.end()) {
            its.erase(it->second);
            its.push_front(UsedFreq(key,it->second->value,_used++));
            _cachs[key] = its.begin();
            return _cachs[key]->value;
        }else{
            return -1;
        }
    }
    
    void set(int key, int value) {
        unordered_map<int,list<UsedFreq>::iterator>::iterator it = _cachs.find(key);
        if (it!= _cachs.end()) {
            its.erase(it->second);
            its.push_front(UsedFreq(key,value,_used++));
            _cachs[key] = its.begin();
        }else{
            if (_cachs.size()==_capacity) {
                _cachs.erase((--its.end())->key);
                its.erase(--its.end());
               
            }
            
            its.push_front(UsedFreq(key,value,_used++));
            _cachs[key] = its.begin();
                }
    }
};
```
* [Binary Tree Preorder Traversal](https://oj.leetcode.com/problems/binary-tree-preorder-traversal/)


```
//Recursive
class Solution {
public:
    
    vector<int> re;
    
    vector<int> preorderTraversal(TreeNode *root) {
        if (root!=NULL) {
            re.push_back(root->val);
            preorderTraversal(root->left);
            preorderTraversal(root->right);
        }
        return re;
    }
};
    
//iteratively
class Solution {
public:
    vector<int> preorderTraversal(TreeNode *root) {
        vector<int> re;
        stack<TreeNode*> nodes;
        TreeNode *current = root;
        if (root!=NULL) {
             nodes.push(current);
        }
       
        while (!nodes.empty() || current != NULL) {
            while (current!=NULL) {
                if (current != root) {
                    nodes.push(current);
                }
                re.push_back(current->val);
                current = current->left;
            }
            
            TreeNode *node = nodes.top();
            current = node->right;
            nodes.pop();
            
           
        }
        
        return re;
    }
};
```

* [Binary Tree Postorder Traversal](https://oj.leetcode.com/problems/binary-tree-postorder-traversal/)

```
//Recursive
class Solution {
public:

    vector<int> re;
    
    vector<int> postorderTraversal(TreeNode *root) {
        if (root!=NULL) {
            postorderTraversal(root->left);
            postorderTraversal(root->right);
            re.push_back(root->val);
        }
        return re;
    }
};

//iteratively
class Solution {
public:
    
    vector<int> re;
    
    vector<int> postorderTraversal(TreeNode *root) {
        
        vector<int> re;
        stack<TreeNode *> nodes;
        TreeNode *current = root;
        if(current!=NULL)
            nodes.push(current);
        TreeNode *pre = root;
        while (!nodes.empty()) {
            current = nodes.top();
            if ((current->left==NULL&&current->right==NULL)||(pre==current->left || pre==current->right)) {
                re.push_back(current->val);
                pre=current;
                nodes.pop();
                
            }
            else{
                if (current->right!=NULL) {
                    nodes.push(current->right);
                }
                if (current->left!=NULL) {
                    nodes.push(current->left);
                }
            }
            
            
        }
        return re;
    }
};
```

