---
layout: post
title: Maximum Product Subarray 
---


* [Maximum Product Subarray](https://oj.leetcode.com/problems/maximum-product-subarray/)

{% highlight cpp linenos %}
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
{% endhighlight %}