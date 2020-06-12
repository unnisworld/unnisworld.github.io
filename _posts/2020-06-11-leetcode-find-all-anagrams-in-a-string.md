---
layout: post
title:  "Leetcode 438 : Find All Anagrams in a String"
date:   2020-02-22 11:36:00 +0530
categories: leetcode leetcode-medium Anagrams SlidingWindow
---

Solution to [Find All Anagrams in a String][leetcode] problem.

class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        
        int[] freq = new int[26];
        for(char c : p.toCharArray()) {
            freq[c - 'a']++;
        }
        
        int start = 0;
        int match = 0;
        for(int end=0;end<s.length();end++) {
            char c = s.charAt(end);
            freq[c - 'a']--;
            
            if(freq[c - 'a'] >= 0) {
                match++;
            }
            
            if(match == p.length()) {
                res.add(start);
            }
            
            if( (end - start)+1 == p.length()) {
                char charGoingOut = s.charAt(start);
                freq[charGoingOut - 'a']++;
                
                if(freq[charGoingOut - 'a'] > 0) {
                	match--;
                }
                start++;
            }
        }
        
        return res;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-all-anagrams-in-a-string/
