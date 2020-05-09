---
layout: post
title:  "Leetcode 122 : Best Time to Buy and Sell Stock II"
date:   2020-05-02
categories: leetcode-easy leetcode array
---

Solution to [Best Time to Buy and Sell Stock 2][leetcode] Problem. Watch this [video][utube] for more detailed explanation.

{% highlight java %}
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0)
            return 0;
        
        int profit = 0;
        for(int i=0;i<prices.length-1;i++) {
            if(prices[i+1] > prices[i]) {
                profit += prices[i+1] - prices[i];
            }
        }
        
        return profit;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/
[utube]: https://www.youtube.com/watch?v=blUwDD6JYaE