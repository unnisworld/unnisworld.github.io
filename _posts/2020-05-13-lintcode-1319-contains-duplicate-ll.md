---
layout: post
title:  "LintCode 1319 : Contains Duplicate ll"
date:   2020-05-13
categories: leetcode-easy leetcode array
---

Solution to [Contains Duplicate ll][leetcode] Problem.


1. Solution using HashMap.

{% highlight java %}
public class Solution {
    /**
     * @param nums: the given array
     * @param k: the given number
     * @return:  whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k
     */
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Map<Integer, Integer> indexMap = new HashMap<>();
        for(int i=0;i < nums.length;i++) {
            if ( indexMap.containsKey(nums[i]) && (i - indexMap.get(nums[i]) <= k))
                return true;
                
            indexMap.put(nums[i], i);    
        }
        
        return false;
    }        
}
{% endhighlight %}

2. Solution using HashSet and sliding window.

{% highlight java %}
public class Solution {
    /**
     * @param nums: the given array
     * @param k: the given number
     * @return:  whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k
     */
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        int ws = 0;
        Set<Integer> set  = new HashSet<>();
        for(int we = 0;we < nums.length;we++) {
            if(we - ws > k) {
                set.remove(nums[ws]);
                ws++;
            }
            
            if(set.contains(nums[we])) {
                return true;
            }
            set.add(nums[we]);
        }
        
        return false;
    }
           
}
{% endhighlight %}

[leetcode]: https://www.lintcode.com/problem/contains-duplicate-ii
