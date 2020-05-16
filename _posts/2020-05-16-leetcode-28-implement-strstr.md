---
layout: post
title:  "LeetCode 28 : Implement strStr()"
date:   2020-05-16
categories: leetcode-easy leetcode String
---

Solution to [Implement strStr][leetcode] Problem. Here is a [nice video][utube] which explains the approach.

{% highlight java %}
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty())
            return 0;
        
        int m = haystack.length(); int n = needle.length();
        if(m < n)
            return -1;
        
        for(int i=0;i<= (m-n);i++) {
            int j;
            for(j=0;j<n;j++) {
                if(haystack.charAt(i+j) != needle.charAt(j))
                    break;
            }
            
            if(j==n) {
                return i;
            }
        }
        
        return -1;
    }
}
{% endhighlight %}
[leetcode]: https://leetcode.com/problems/implement-strstr/
[utube]: https://www.youtube.com/watch?v=TsxFvVy_5m0
