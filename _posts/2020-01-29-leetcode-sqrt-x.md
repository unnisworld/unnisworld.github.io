---
layout: post
title:  "Sqrt x"
date:   2020-01-29 5:30:00 +0530
categories: leetcode-simple leetcode binarysearch
---

Solution to [integer to roman conversion leetcode problem][leetcode-sqrt].

{% highlight java %}
class Solution {
    public int mySqrt(int x) {
        if (x == 0 || x == 1) {
            return x;
        }

        int l = 0, r = x/2;
        while(l<=r) {
            long m = l  + (r - l)/2;
            long s = m * m;
            if (s == x || ((m+1) * (m+1) > x && s < x)) {
                return (int)m;
            } else if (s > x) {
                r = (int)(m - 1);
            } else {
                l = (int)(m + 1);
            }
        }

        return -1;
    }

}
{% endhighlight %}

[leetcode-sqrt]: https://leetcode.com/problems/sqrtx/
