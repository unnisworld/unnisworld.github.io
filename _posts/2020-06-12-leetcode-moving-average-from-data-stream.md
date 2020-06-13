---
layout: post
title:  "Leetcode 346 : Moving Average from Data Stream"
date:   2020-06-12 23:20:00 +0530
categories: leetcode leetcode-easy Queue
---

Solution to [Moving Average from Data Stream][leetcode] problem.

{% highlight java %}
class MovingAverage {
    
    LinkedList<Integer> q = new LinkedList<>();
    int size = 0;
    int sum = 0;

    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.size = size;
    }
    
    public double next(int val) {
        q.add(val);
        sum += val;
        
        if(q.size() > size) {
            int e = q.remove();
            sum -= e;
        }
        
        return sum * 1.0 / q.size();
    }
}
{% endhighlight %}

Solution using array

{% highlight java %}
class MovingAverage {
    
    int size = 0;
    int sum = 0;
    int[] data;
    int ptr = 0;
    int curSize = 0;

    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.data = new int[size];
        this.size = size;
    }
    
    public double next(int val) {
        ptr = ptr % size;
        
        sum -= data[ptr];
        data[ptr++] = val;
        sum += val;
        
        if(curSize < size)
            curSize++;
        
        return sum * 1.0 / curSize;
    }
}
{% endhighlight %}


[leetcode]: https://leetcode.com/problems/moving-average-from-data-stream/
