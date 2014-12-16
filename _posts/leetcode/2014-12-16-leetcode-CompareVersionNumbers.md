---
layout: post
title: Compare Version Numbers 
---


* [Compare Version Numbers](https://oj.leetcode.com/problems/compare-version-numbers/)

{% highlight cpp linenos %}
class Solution {
public:
    int compareVersion(string version1, string version2) {
        unsigned long  index= version1.find('.');
        
        
        
        
        int vers1First;
        string vers1;
        if (index==string::npos) {
            vers1First=atoi(version1.c_str());
            vers1="0";
        }else{
             vers1First=atoi(version1.substr(0,index).c_str());
             vers1=version1.substr(index+1);
        }

        index =version2.find('.') ;
        int vers2First;
        string vers2;
        if (index==string::npos) {
            vers2First=atoi(version2.c_str());
            vers2="0";
        }else{
            vers2First=atoi(version2.substr(0,index).c_str());
            vers2=version2.substr(index+1).c_str();
        }
        if (vers1First>vers2First) {
            return 1;
        }else if(vers1First<vers2First){
            return -1;
        }else {
            if (vers1==vers2) {
                return 0;
            }else{
                return compareVersion(vers1, vers2);
            }
        
        }
    }
};
{% endhighlight %}