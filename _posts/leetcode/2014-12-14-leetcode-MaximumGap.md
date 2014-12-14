---
layout: post
title: Maximum Gap  
---

* [Maximum Gap](https://oj.leetcode.com/problems/maximum-gap/)

{% highlight cpp linenos %}
class Solution {
public:
    int maximumGap(vector<int> &num) {
        
        if (num.size()<2) {
            return 0;
        }
        
        int max=*max_element(num.begin(), num.end());
        int min=*min_element(num.begin(), num.end());
        int n=(int)num.size();
        float distance = (float)(max-min)/(n-1);
        vector<int> maxs(n,-1);
        vector<int> mins(n,-1);
        
        for (int i=0; i<num.size(); i++) {
            int var = num[i];
            int index = (var-min)/distance;
            if (maxs[index]<var) {
                maxs[index]=var;
            }
            if (mins[index]>var || mins[index]==-1) {
                mins[index]=var;
            }
        }
        
        int preMax = maxs[0];
        int reMax = maxs[0]-mins[0];
        for (int i=1; i<n; i++) {
            if (mins[i]==-1) {
                continue;
            }
            int tempMax = mins[i]-preMax;
            if (tempMax>reMax) {
                reMax=tempMax;
            }
            
            preMax=maxs[i];
        }
        
        return reMax;
                             
    }
};
{% endhighlight %}