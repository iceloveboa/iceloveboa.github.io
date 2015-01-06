---
layout: post
title: Factorial Trailing Zeroes 
---

* [Factorial Trailing Zeroes](https://oj.leetcode.com/problems/factorial-trailing-zeroes/)

{% highlight cpp linenos %}
class Solution {
public:
    int trailingZeroes(int n) {
        if(n>=5)
        return n/5+trailingZeroes(n/5);
        else return 0;
    }
};
 {% endhighlight %}   