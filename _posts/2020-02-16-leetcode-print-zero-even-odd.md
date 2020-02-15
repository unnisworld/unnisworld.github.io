---
layout: post
title:  "Print Zero Even Odd"
date:   2020-02-16 00:10:00 +0530
categories: leetcode leetcode-medium Threading
---

Solution to [Print Zero Even Odd][leetcode] problem.

{% highlight java %}
class ZeroEvenOdd {
    private int n;

    Lock l = new ReentrantLock();
    Condition printZeroCondition = l.newCondition();
    Condition printEvenCondition = l.newCondition();
    Condition printOddCondition = l.newCondition();

    private volatile boolean zero = true;
    private volatile boolean odd = false;
    private volatile boolean even = false;
    private volatile boolean lastCalledEven = true;

    public ZeroEvenOdd(int n)  {
        this.n = n;
    }

    // printNumber.accept(x) outputs "x", where x is an integer.
    public void zero(IntConsumer printNumber) throws InterruptedException {
        try {
            l.lock();
            for (int i = 0; i < n; i++) {
                while(!zero)
                    printZeroCondition.await();
                printNumber.accept(0);
                zero = false;
                if(lastCalledEven) {
                    odd = true;
                    lastCalledEven = false;
                    printOddCondition.signalAll();
                }
                else {
                    even = true;
                    lastCalledEven = true;
                    printEvenCondition.signalAll();
                }
            }
        }finally{
            l.unlock();
        }
    }

    public void odd(IntConsumer printNumber) throws InterruptedException {
        try {
            l.lock();
            for(int i=1;i<=n;i=i+2) {
                while(!odd)
                    printOddCondition.await();
                printNumber.accept(i);
                odd = false;
                zero = true;
                printZeroCondition.signalAll();
            }
        }finally{
            l.unlock();
        }

    }

    public void even(IntConsumer printNumber) throws InterruptedException {
        try {
            l.lock();
            for(int i=2;i<=n;i=i+2) {
                while(!even)
                    printEvenCondition.await();
                printNumber.accept(i);
                even = false;
                zero = true;
                printZeroCondition.signalAll();
            }
        }finally{
            l.unlock();
        }
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/print-zero-even-odd/
