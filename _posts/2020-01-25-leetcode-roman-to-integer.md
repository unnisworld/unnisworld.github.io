---
layout: post
title:  "Roman to Integer Conversion"
date:   2020-01-25 12:18:00 +0530
categories: leetcode-medium leetcode general-algo 
---

Solution to [roman to integer conversion leetcode problem][leetcode-roman-to-integer].

{% highlight java %}
class Solution {
    public int romanToInt(String s) {
        Map<String, Integer> riMap = Map.of(
                "M", 1000, 
                "D",  500, 
                "C",  100, 
                "L",   50, 
                "X",   10, 
                "V",    5, 
                "I",    1);

        int sum = 0;
        int len = s.length();
        for (int ndx = 0; ndx < len - 1; ndx++) 
        {
            int cur = riMap.get(String.valueOf(s.charAt(ndx)));
            int nxt = riMap.get(String.valueOf(s.charAt(ndx + 1)));

            if (cur < nxt) {
                sum -= cur;
            } else {
                sum += cur;
            }       
        }

        sum += riMap.get(String.valueOf(s.charAt(len-1)));

        return sum;
    }
}
{% endhighlight %}

[leetcode-roman-to-integer]: https://leetcode.com/problems/roman-to-integer
