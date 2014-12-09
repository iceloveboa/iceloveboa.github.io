---
layout: post
title: Evaluate Reverse Polish Notation 
---

* [Evaluate Reverse Polish Notation](https://oj.leetcode.com/problems/evaluate-reverse-polish-notation/)

{% highlight cpp linenos %}
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
{% endhighlight %}