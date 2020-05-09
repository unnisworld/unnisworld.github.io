---
layout: post
title:  "Lintcode 928 : Longest Substring with At Most Two Distinct Characters"
date:   2020-05-08
categories: leetcode-medium lintcode sliding-window string
---

Solution to [Longest Substring with At Most Two Distinct Characters][lintcode] Problem.

{% highlight java %}
public class Solution {
    /**
     * @param s: a string
     * @return: the length of the longest substring T that contains at most 2 distinct characters
     */
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        // Write your code here
        Map<Character, Integer> freqMap = new HashMap<>();
        int distCharCount = 0;
        int max = 0;
        int ws = 0;
        for(int we=0; we < s.length(); we++) {
            if(freqMap.containsKey(s.charAt(we))) {
                freqMap.put(s.charAt(we), freqMap.get(s.charAt(we)) + 1);
            } else {
                freqMap.put(s.charAt(we), 1);
                distCharCount++;
            }

            while(distCharCount > 2) {
                char charToBeRemoved = s.charAt(ws);
                int freq = freqMap.get(charToBeRemoved);
                if(freq == 1) {
                    distCharCount--;
                    freqMap.remove(charToBeRemoved);
                } else {
                    freqMap.put(charToBeRemoved, freq-1);
                }
                ws++;
            }
            
            max = Math.max(max, (we-ws) + 1);
        }
        return max;
    }
}
{% endhighlight %}

[lintcode]: https://www.lintcode.com/problem/longest-substring-with-at-most-two-distinct-characters/description