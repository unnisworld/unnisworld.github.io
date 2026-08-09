---
layout: post
title:  "Find first bad version"
date:   2020-02-01 10:00:00 +0530
categories: leetcode-simple leetcode binarysearch
---

Solution to [Find first bad version][leetcode] problem.

{% highlight java %}
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int l=1, r=n;

        while(l < r) {
            int m = l + (r - l)/2;
            if (isBadVersion(m)) 
            {
                r = m;
            } else {
                l = m + 1;
            }
        }

        return l;        
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/first-bad-version/
