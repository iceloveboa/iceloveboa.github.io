---
layout: post
title: Dungeon Game 
---

* [Dungeon Game](https://oj.leetcode.com/problems/dungeon-game/)

{% highlight cpp linenos %}
class Solution {
public:
    int calculateMinimumHP(vector<vector<int> > &dungeon) {
        int n = dungeon.size();
        int m = dungeon[0].size();
        int dp[n][m];
        memset(dp, 0, sizeof(dp));
        dp[n-1][m-1] = max(-dungeon[n-1][m-1]+1,1);
        for (int i= n-1; i>=0; i--) {
            for (int j = m-1; j>=0; j--) {
                if (i<n-1) {
                    dp[i][j]=max(dp[i+1][j]-dungeon[i][j],1);
                }
                if (j<m-1) {
                    if (dp[i][j]) {
                        dp[i][j]=min(max(dp[i][j+1]-dungeon[i][j],1),dp[i][j]);
                    }else{
                        dp[i][j]=max(dp[i][j+1]-dungeon[i][j],1);
                    }
                }
            }
        }
        return dp[0][0];
    }
};
 {% endhighlight %}   