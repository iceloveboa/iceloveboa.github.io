---
layout: post
title: Max Points on a Line
---

* [Max Points on a Line](https://oj.leetcode.com/problems/max-points-on-a-line/)

{% highlight cpp linenos %}
/**
 * Definition for a point.
 * struct Point {
 *     int x;
 *     int y;
 *     Point() : x(0), y(0) {}
 *     Point(int a, int b) : x(a), y(b) {}
 * };
 */
 #include <cmath>
 
class Solution {
public:
    int maxPoints(vector<Point> &points) {
        int maxNum = 0;
        unordered_map<float, int> mp;
        for (int i=0; i< points.size(); i++) {
            mp.clear();
            int dup = 1;
            for (int j = i+1; j<points.size(); j++) {
                if (points[i].x == points[j].x && points[i].y == points[j].y) {
                    dup++;
                    continue;
                }
                
                if (points[i].x == points[j].x) {
                    mp[INT_MAX]++;
                }else{
                    mp[(float)(points[i].y-points[j].y)/(points[i].x-points[j].x)]++;
                }
            }
            
            maxNum = dup > maxNum ? dup : maxNum;
            for (unordered_map<float, int>::iterator it = mp.begin();it!=mp.end();it++)
            {
                if (it->second + dup  > maxNum) {
                    maxNum = it->second+dup;
                }
            }
        }
        
        
        return maxNum;
    }
};
{% endhighlight %}