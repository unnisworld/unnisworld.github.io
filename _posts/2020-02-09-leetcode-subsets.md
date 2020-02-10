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

# Alternate approach using Recursion

This approach is a direct port of the [python code provided][alt-approach-1] in the leetcode discussion.

{% highlight java %}
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> path = new ArrayList<Integer>();

        dfs(nums, 0, path, ans);
        return ans;
    }
    
    private void dfs(int[] nums, int ndx, List<Integer> path, List<List<Integer>> ans)     {
        ans.add(path);

        for(int i=ndx;i<nums.length;i++){
            List<Integer> npath = new ArrayList<Integer>(path);
            npath.add(nums[i]);
            ndx = ndx + 1;
            dfs(nums, ndx, npath, ans);
        }
    }
    
}
{% endhighlight %}


[leetcode]: https://leetcode.com/problems/subsets/
[approach]: https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/
[alt-approach-1]: https://leetcode.com/problems/subsets-ii/discuss/485407/python-easy-understanding-method
