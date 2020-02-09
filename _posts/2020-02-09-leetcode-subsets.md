---
layout: post
title:  "Find Subsets or Power set"
date:   2020-02-09 22:45:00 +0530
categories: leetcode-medium leetcode set subsets powerset
---

Solution to [return all possible subsets (the power set)][leetcode] problem.

{% highlight java %}
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        int n = nums.length;
        int twoPowN = 1 << n;
        List<List<Integer>> r = new ArrayList<>();
        
        for (int i=0;i<twoPowN;i++) {
            List<Integer> sr = new ArrayList<>();
            for(int j=0;j<n;j++) {
                int bits = 1 << j;
                if ((i & bits) > 0)
                    sr.add(nums[j]);
            }
            r.add(sr);
        }
        
        return r;
    }
    
}
{% endhighlight %}

The approach used is explained in [this geeksforgeeks link][approach].

[leetcode]: https://leetcode.com/problems/subsets/
[approach]: https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/
