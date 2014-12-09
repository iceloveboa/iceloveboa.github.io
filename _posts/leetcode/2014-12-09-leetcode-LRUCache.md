---
layout: post
title: LRU Cache 
---

* [LRU Cache](https://oj.leetcode.com/problems/lru-cache/)

{% highlight cpp linenos %}
struct UsedFreq {
    int key;
    int value;
    int times;
    UsedFreq()
    {
        key = 0;
        value = 0;
        times = 0;
    }
    UsedFreq(int _key,int _value,int _times){
        key = _key;
        value = _value;
        times = _times;
    }
};

class LRUCache{
public:
    unordered_map<int,list<UsedFreq>::iterator> _cachs;
    int _capacity;
    int _used;
    list<UsedFreq> its;
    LRUCache(int capacity) {
        _capacity = capacity;
        _cachs.clear();
        its.clear();
        _used = 1;
    }
    
    int get(int key) {
        unordered_map<int,list<UsedFreq>::iterator>::iterator it = _cachs.find(key);
        if (it!= _cachs.end()) {
            its.erase(it->second);
            its.push_front(UsedFreq(key,it->second->value,_used++));
            _cachs[key] = its.begin();
            return _cachs[key]->value;
        }else{
            return -1;
        }
    }
    
    void set(int key, int value) {
        unordered_map<int,list<UsedFreq>::iterator>::iterator it = _cachs.find(key);
        if (it!= _cachs.end()) {
            its.erase(it->second);
            its.push_front(UsedFreq(key,value,_used++));
            _cachs[key] = its.begin();
        }else{
            if (_cachs.size()==_capacity) {
                _cachs.erase((--its.end())->key);
                its.erase(--its.end());
               
            }
            
            its.push_front(UsedFreq(key,value,_used++));
            _cachs[key] = its.begin();
                }
    }
};
{% endhighlight %}