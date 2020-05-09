---
layout: post
title:  "Leetcode 3 : Longest Substring Without Repeating Characters"
date:   2020-05-07
categories: leetcode-medium leetcode sliding-window string
---

Solution to [Longest Substring Without Repeating Characters][leetcode] Problem.

{% highlight java %}
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int winStart = 0;
        int ans = 0;
        Map<Character, Integer> seenChars = new HashMap<>();    
        for(int winEnd = 0; winEnd < s.length(); winEnd++) {
            char curChar = s.charAt(winEnd);
            if(seenChars.containsKey(curChar)) {
                System.out.println("string before adjustment "+ s.substring(winStart, winEnd+1));
                // To understand why Math.max is needed use i/p "abba".
                winStart = Math.max(seenChars.get(curChar) + 1, winStart);
                System.out.println("string after adjustment "+ s.substring(winStart, winEnd+1));
            }
            ans = Math.max(ans, (winEnd-winStart) + 1);
            seenChars.put(curChar, winEnd);
        }
        
        return ans;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/longest-substring-without-repeating-characters/