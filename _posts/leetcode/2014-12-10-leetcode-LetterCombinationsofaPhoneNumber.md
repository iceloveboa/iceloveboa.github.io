---
layout: post
title: Letter Combinations of a Phone Number
---


* [Letter Combinations of a Phone Number](https://oj.leetcode.com/problems/letter-combinations-of-a-phone-number/)

{% highlight cpp linenos %}
class Solution {
public:
    
    map<char, string> digs;
    Solution(){
        digs['2']="abc";
        digs['3']="def";
        digs['4']="ghi";
        digs['5']="jkl";
        digs['6']="mno";
        digs['7']="pqrs";
        digs['8']="tuv";
        digs['9']="wxyz";
    }
    vector<string> letterCombinations(string digits) {
        vector<string> result;
        letterCombinationsPart(digits, 0, "", result);
        
        return result;
    }
    
    
    void letterCombinationsPart(string digits,int index,string current,vector<string> &result){
        if (index==digits.size()) {
            result.push_back(current);
        }else{
            string ele = digs[digits[index]];
            for (int i=0; i<ele.size(); i++) {
                current+=ele[i];
                letterCombinationsPart(digits, index+1, current, result);
                current.erase(current.size()-1,1);
            }
        }
        
    }
};

{% endhighlight %}
