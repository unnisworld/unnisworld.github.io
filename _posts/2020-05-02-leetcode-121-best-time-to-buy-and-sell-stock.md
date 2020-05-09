---
layout: post
title:  "Leetcode 121 : Best Time to Buy and Sell Stock"
date:   2020-05-02
categories: leetcode-easy leetcode array
---

Solution to [Best Time to Buy and Sell Stock][leetcode] Problem. Watch this [video][utube] for more detailed explanation.

{% highlight java %}
class Solution {
    
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int minPrice = Integer.MAX_VALUE;
        for(int i=0;i<prices.length;i++) {
            if(prices[i] < minPrice) {
                minPrice = prices[i];
            } else {
                maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            }
        }
        
        return maxProfit;
    }  
} 
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
[utube]: https://www.youtube.com/watch?v=mj7N8pLCJ6w