---
layout: post
title: Binary Tree Postorder Traversal 
---

* [Binary Tree Postorder Traversal](https://oj.leetcode.com/problems/binary-tree-postorder-traversal/)

{% highlight cpp linenos %}
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
{% endhighlight %}