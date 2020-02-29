---
layout: post
title:  "Isomorphic Strings"
date:   2020-02-29 16:15:00 +0530
categories: leetcode leetcode-simple LinkedList
---

Solution to [Isomorphic Strings][leetcode] problem.

{% highlight java %}
// Reading this helps - https://www.educative.io/edpresso/how-to-check-if-two-strings-are-isomorphic
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length())
            return false;
        
        Map<Character, Character> mapping = new HashMap<>();
        Set<Character> charsAlreadyUsedForMapping = new HashSet<Character>();
        for(int i=0;i<s.length();i++) {
            char sc = s.charAt(i);
            char tc = t.charAt(i);
            // already a mapping exists for this char
            if (mapping.get(sc) != null) 
            {
                if (mapping.get(sc) != tc) { 
                    // the exiting mapping is not same as required mapping in t
                    return false;
                }
            } 
            else // no mapping exists 
            { 
                // if the char is already mapped you cannot use it again
                if (charsAlreadyUsedForMapping.contains(tc)) {
                    return false;
                }
                mapping.put(sc, tc);
                charsAlreadyUsedForMapping.add(tc);
            }
        }
        
        return true;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/isomorphic-strings/
