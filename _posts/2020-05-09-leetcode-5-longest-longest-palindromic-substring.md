---
layout: post
title:  "Leetcode 5 : Longest Palindromic Substring"
date:   2020-05-07
categories: leetcode-medium leetcode string palindrom
---

Solution to [Longest Palindromic Substring][leetcode] Problem. See this [video][utube] for a nice explanation.

{% highlight java %}
class Solution {
    
    int resultStart;
    int resultLength;
    
    public String longestPalindrome(String s) {
        int strLen = s.length();
        if(strLen < 2)
            return s;
        
        for(int start=0;start<strLen-1;start++) {
            expandRange(s, start, start);
            expandRange(s, start, start + 1);
        }
        
        return s.substring(resultStart, resultStart + resultLength);
    }
    
    private void expandRange(String str, int begin, int end) {
        while(begin >=0 && end < str.length() && 
             str.charAt(begin) == str.charAt(end)) {
            begin--; end++;
        }
        
        if(resultLength < (end - begin - 1)) {
            resultStart = begin + 1;
            resultLength = end - begin - 1;
        }
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/longest-palindromic-substring/
[utube]: https://www.youtube.com/watch?v=DK5OKKbF6GI