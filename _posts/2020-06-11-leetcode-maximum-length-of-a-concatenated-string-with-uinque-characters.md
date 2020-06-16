---
layout: post
title:  "Leetcode 1239 : Maximum Length of a Concatenated String with Unique Characters"
date:   2020-06-16 14:00:00 +0530
categories: leetcode leetcode-medium DFS Backtracking String
---

Solution to [Maximum Length of a Concatenated String with Unique Characters][leetcode] problem.

{% highlight java %}
class Solution {
    
    int maxLen = 0;
    
    public int maxLength(List<String> arr) {
        findMaxLen(arr, 0, "");
        
        return maxLen;
    }
    
    private void findMaxLen(List<String> arr, int ndx, String curStr) {
		if(!isUnique(curStr)) {
			return;
		} 
		maxLen = Math.max(maxLen, curStr.length());
		
		for(int i=ndx;i<arr.size();i++) {
			if(isUnique(arr.get(i))) {
				findMaxLen(arr, i + 1, curStr + arr.get(i));
			}
		}
	}

	private static boolean isUnique(String curStr) {
		int[] cnt = new int[26];
		for(char c : curStr.toCharArray()) {
			if (++cnt[c - 'a'] > 1) return false;
		}
		
		return true;
	}
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/
