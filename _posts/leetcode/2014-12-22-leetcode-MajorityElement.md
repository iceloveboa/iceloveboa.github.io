---
layout: post
title: Majority Element 
---

* [Majority Element](https://oj.leetcode.com/problems/majority-element/)

{% highlight cpp linenos %}
class Solution {
public:
    int majorityElement(vector<int> &num) {
        map<int, long> times;
        long n = num.size();
        for (int i=0; i<num.size(); i++) {
            long temp = times[num[i]];
            if (temp >= n/2) {
                return num[i];
            }else{
                 times[num[i]]++;
            }
        }
        
        
    }
};
{% endhighlight %}