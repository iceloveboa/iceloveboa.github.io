---
layout: post
title: Reverse Words in a String 
---

* [Reverse Words in a String](https://oj.leetcode.com/problems/reverse-words-in-a-string/)

{% highlight cpp linenos %}
class Solution {
public:
    void reverseWords(string &s) {
        string result;
        istringstream iss(s);
        do{
            string word;
            iss>>word;
            result=word+" "+result;
        }while (iss);
        result = result.substr(1,result.length()-2);
        s=result;
    }
};
{% endhighlight %}