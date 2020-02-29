---
layout: post
title:  "Minimum Index Sum of Two Lists"
date:   2020-02-29 16:15:00 +0530
categories: leetcode leetcode-simple LinkedList
---

Solution to [Isomorphic Strings][leetcode] problem.

{% highlight java %}
class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        Map<String, Integer> list2Map = listToMap(list2);
        
        List<String> result = new ArrayList<>();
        int previousMatchScore = Integer.MAX_VALUE;
        for(int i=0;i<list1.length;i++) {
            if (list2Map.get(list1[i]) != null) {
                int score = i + list2Map.get(list1[i]);
                if (score <= previousMatchScore) {
                    previousMatchScore = score;
                    result.add(list1[i]);
                }
            }
        }
        
        return result.toArray(new String[result.size()]);
    }
    
    private Map<String, Integer> listToMap(String[] list) {
        Map<String, Integer> listMap = new LinkedHashMap<>();
        for(int i=0;i<list.length;i++) {
            listMap.put(list[i], i);
        }
        return listMap;
    }
        
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/minimum-index-sum-of-two-lists/
