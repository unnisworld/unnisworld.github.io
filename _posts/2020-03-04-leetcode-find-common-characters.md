---
layout: post
title:  "Find Common Characters"
date:   2020-03-07 11:35:00 +0530
categories: leetcode leetcode-simple Character-Array-Problem
---

Solution to [Path Sum][leetcode] problem. I came up with this solution, but was blown away when I saw the  solution by [Lazy Coder][lazy-coder].

{% highlight java %}
class Solution {
    public List<String> commonChars(String[] A) {
        int[] baseCharCount = countChars(A[0]);
        
        for(int i=1;i<A.length;i++) {
            adjustBaseCharCountToMinCount(baseCharCount, A[i]);
        }
        
        return convertCharCountToString(baseCharCount);
    }
    
    private List<String> convertCharCountToString(int[] baseCharCount) {
        final int asciiCodeOfa = 97;
        List<String> res = new ArrayList<>();
        for(int i=0;i<baseCharCount.length;i++) {
            for(int j=0;j<baseCharCount[i];j++) {
                res.add("" + (char)(asciiCodeOfa + i));  
            }
        }
        
        return res;
    }
    
    private void adjustBaseCharCountToMinCount(int[] baseCharCount, String s) {
        int[] currentStringCharCount = countChars(s);
        for(int i=0;i<26;i++) {
            baseCharCount[i] = Math.min(baseCharCount[i], currentStringCharCount[i]);
        }    
    }
    
    private int[] countChars(String s) {
        int[] result = new int[26];
        for(char c : s.toCharArray()) {
            result[c - 'a']++;
        }
        
        return result;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-common-characters/
