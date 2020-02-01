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
        if (x<2)
            return x;
        
        long l=1, r=x/2;
        while(l<=r) {
            long m=l+(r-l)/2;
            
            if ((m*m) == x || ((m+1)*(m+1) > x && (m*m) < x))
                return (int)m;
            else if (m*m > x) 
                r=m-1;
            else
                l=m+1;
        }
        
        return -1;
    }

}
{% endhighlight %}

[leetcode-sqrt]: https://leetcode.com/problems/sqrtx/
