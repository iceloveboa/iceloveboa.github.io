---
layout: post
title: Fraction to Recurring Decimal
---

* [Fraction to Recurring Decimal](https://oj.leetcode.com/problems/fraction-to-recurring-decimal/)

{% highlight cpp linenos %}
class Solution {justtest
public:
    string fractionToDecimal(int numerator, int denominator) {
        map<long long,long long> indexs;
        string re;
        
        if (numerator == 0) {
            return "0";
        }
        
        long long remainder;
        long long number = numerator;
        long long denom = denominator;
        if ((double)number/(double)denom < 0) {
            re.append("-");
        }
        number = abs(number);
        denom = abs(denom);
        
        
            long long integer = number / denom;
            remainder = number % denom;
            re.append(to_string(integer));
            if (remainder == 0) {
                return re;
            }else{
                re.append(".");
            }
        
        
        int index=0;
        while (indexs.find(remainder)==indexs.end()) {
            indexs[remainder]=index++;
            remainder = remainder*10;
            if (remainder>=denom) {
                long long integer = remainder / denom;
                remainder = remainder % denom;
                re.append(to_string(integer));
                if (remainder == 0) {
                    return re;
                }
            }else{
                re.append("0");
            }
        }
        
        unsigned long  dotpos = re.find('.');
        re.insert(dotpos+indexs[remainder]+1, "(");
        re.append(")");
        return re;
    }
    
};
{% endhighlight %}