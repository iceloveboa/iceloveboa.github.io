---
layout: post
title: Maximum Subarray 
---

* [Maximum Subarray](https://oj.leetcode.com/problems/maximum-subarray/)


{% highlight cpp linenos %}
class Solution {
public:
    int maxSubArray(int A[], int n) {
        int maxsum=A[0];
        int cursum=A[0];
        for (int i=1; i<n; i++) {
            if (cursum<0) {
                cursum=A[i];
            }else{
                 cursum+=A[i];
            }
            if (cursum>maxsum) {
                maxsum=cursum;
            }
        }
        return maxsum;
    }
};
{% endhighlight %}