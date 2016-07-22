---
layout: post
title: Wiggle Subsequence 
---

* [Wiggle Subsequence](https://leetcode.com/problems/wiggle-subsequence/)

{% highlight cpp linenos %}
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        if (nums.size() <= 1) {
            return nums.size();
        }
        int re = 1;
        int pre = 0;
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] > nums[i-1] && pre != 1) {
                re++;
                pre = 1;
            }
            if (nums[i] < nums[i-1] && pre != -1) {
                re++;
                pre = -1;
            }
        }
        return re;
    }
};
 {% endhighlight %}   