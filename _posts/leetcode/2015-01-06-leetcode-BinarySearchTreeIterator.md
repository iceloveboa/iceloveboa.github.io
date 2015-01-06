---
layout: post
title: Binary Search Tree Iterator  
---

* [Binary Search Tree Iterator ](https://oj.leetcode.com/problems/binary-search-tree-iterator/)

{% highlight cpp linenos %}
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class BSTIterator {
private:
    list<TreeNode> reOrderList;
    list<TreeNode>::iterator current;
public:
    BSTIterator(TreeNode *root) {
        if (root) {
            middleOrder(root);
        }
     
        current = reOrderList.begin();
    }
    
    void middleOrder(TreeNode *node){
        if (node->left) {
            middleOrder(node->left);
        }
        TreeNode temp = TreeNode(node->val);
        reOrderList.push_back(temp);
        if (node->right) {
            middleOrder(node->right);
        }
    }
    
    /** @return whether we have a next smallest number */
    bool hasNext() {
        list<TreeNode>::iterator next = current++;
        current--;
        if (next != reOrderList.end()) {
            return true;
        }else{
            return false;
        }
    }
    
    /** @return the next smallest number */
    int next() {
        return (current++)->val;
    }
};
/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
 {% endhighlight %}   