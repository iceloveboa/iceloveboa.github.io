---
layout: post
title: Find Minimum in Rotated Sorted Array 
---

* [Find Minimum in Rotated Sorted Array](https://oj.leetcode.com/problems/find-minimum-in-rotated-sorted-array/)  
 
{% highlight cpp linenos %}
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
{% endhighlight %}