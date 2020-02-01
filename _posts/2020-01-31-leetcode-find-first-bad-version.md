---
layout: post
title:  "Find Minimum in rotated sorted array"
date:   2020-02-01 10:00:00 +0530
categories: leetcode-simple leetcode binarysearch
---

Solution to [Find first bad version][leetcode] problem.

{% highlight java %}
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        if (n < 0)
            return n;
        if (n==0)
            return isBadVersion(0) ? 0 : -1;
        
        int l=0, r=Integer.MAX_VALUE;
        int lastBad = -1;
        while(l<=r) {
            int m = l + (r-l)/2;
            
            if (isBadVersion(m)) { // Check for older bad version.
                lastBad=m;
                r=m-1;
            } else { // versions till m are fine. Check versions greater than m.
                l=m+1;
            }
        }
        
        return lastBad;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/first-bad-version/
