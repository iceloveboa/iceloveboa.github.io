---
layout: post
title: Binary Tree Preorder Traversal
---

* [Binary Tree Preorder Traversal](https://oj.leetcode.com/problems/binary-tree-preorder-traversal/)


{% highlight cpp linenos %}
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
{% endhighlight %}
