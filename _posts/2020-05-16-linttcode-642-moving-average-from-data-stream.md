---
layout: post
title:  "LinttCode 642 : Moving Average from Data Stream"
date:   2020-05-16
categories: leetcode-easy leetcode slidingwindow
---

Solution to [Moving Average from Data Stream][leetcode] Problem. Here is a [nice video][utube] which explains the approach.

{% highlight java %}
public class MovingAverage {
    
    private Queue<Integer> q;
    private int maxSize;
    private double sum;
    /*
    * @param size: An integer
    */public MovingAverage(int size) {
        // do intialization if necessary
        maxSize = size;
        q = new LinkedList<>();
    }

    /*
     * @param val: An integer
     * @return:  
     */
    public double next(int val) {
        // write your code here
        if(q.size() == maxSize) {
            sum -= q.remove();
        }
        
        sum += val;
        q.add(val);
        
        return sum/q.size();
    }
}
{% endhighlight %}
[leetcode]: https://www.lintcode.com/problem/moving-average-from-data-stream/description
[utube]: https://www.youtube.com/watch?v=E-kjYOZEBxY
