---
layout: post
title: Spiral Matrix 
---

* [Spiral Matrix ](https://oj.leetcode.com/problems/spiral-matrix/)

{% highlight cpp linenos %}

class Solution {
public:
    vector<int> spiralOrder(vector<vector<int> > &matrix) {
        vector<int> re;
        if (matrix.size()==0){
            return re;
        }
        
        
        
        int incx=1;
        int incy=0;
        int sizexMax=(int)matrix[0].size();
        int sizeyMax=(int)matrix.size();
        int sizexMin=0;
        int sizeyMin=0;
        
        int beginx=0,beginy=0;
        
       
        re.push_back(matrix[beginy][beginx]);
      
       
        
        while (sizexMax!=sizexMin && sizeyMax!=sizeyMin) {
           
            if (beginx+incx<sizexMin) {
                incx=0;
                incy=-1;
                sizeyMax--;
                continue;
            }else if (beginx+incx<sizexMax) {
                beginx=beginx+incx;
            }else{
                incx=0;
                incy=1;
                sizeyMin++;
                continue;
            }
            
            if (beginy+incy<sizeyMin) {
                incx=1;
                incy=0;
                sizexMin++;
                continue;
            }
            else if (beginy+incy<sizeyMax) {
                beginy=beginy+incy;
            }else{
                incy=0;
                incx=-1;
                sizexMax--;
                continue;
            }
            re.push_back(matrix[beginy][beginx]);
        }
        
        return re;
        
    }
};
{% endhighlight %}