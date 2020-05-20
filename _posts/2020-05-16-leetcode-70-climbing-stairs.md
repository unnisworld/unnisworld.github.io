---
layout: post
title:  "LeetCode 28 : Implement strStr()"
date:   2020-05-16
categories: leetcode-easy leetcode String
---

Solution to [Implement strStr][leetcode] Problem. Here is a [nice video][utube] which explains the approach.

{% highlight java %}
class Solution {
    public int climbStairs(int n) {
        if(n == 1 || n == 2)
            return n;
        int[] dp = new int[n+1];
        // fill base cases
        dp[1] = 1; // how many ways can you climb 1 stairs
        dp[2] = 2; // how many ways can you climb 2 stairs
        
        for(int i=3;i<=n;i++) {
            dp[i] = dp[i-1] + dp[i-2];
         }
        
        return dp[n];
    }
}
{% endhighlight %}
[leetcode]: https://leetcode.com/problems/climbing-stairs/
[utube]: https://www.youtube.com/watch?v=uHAToNgAPaM
