---
layout: post
title: Excel Sheet Column Title 
---

* [Excel Sheet Column Title](https://oj.leetcode.com/problems/excel-sheet-column-title/)

{% highlight cpp linenos %}
class Solution {
public:
    string convertToTitle(int n) {
        string re = "";
        while (n>26) {
            int i = n % 26 ;
            if(i==0){
                re.insert(0, 1,'Z');
                n = n/26 -1;
            }else{
                re.insert(0, 1,i+'A'-1);
                n = n/26;
            }
        }
        
         re.insert(0, 1,n+'A'-1);
     
        return re;
    }
};
{% endhighlight %}