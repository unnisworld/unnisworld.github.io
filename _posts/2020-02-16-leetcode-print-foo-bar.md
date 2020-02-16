---
layout: post
title:  "Print FooBar Alternately"
date:   2020-02-16 08:00:00 +0530
categories: leetcode leetcode-medium Threading
---

Solution to [Print FooBar Alternately][leetcode] problem.

{% highlight java %}
import java.util.concurrent.Semaphore;

class FooBar {
    private int n;
    private Semaphore semFoo;
    private Semaphore semBar;
    
    public FooBar(int n) {
        this.n = n;
        this.semFoo = new Semaphore(0);
        this.semBar = new Semaphore(0);
    }

    public void foo(Runnable printFoo) throws InterruptedException {

        for (int i = 0; i < n; i++) {
            // when i == 0, ignore semaphore check to ensure foo runs before bar
            if (i != 0) {
                this.semFoo.acquire();  
            }
            
            // printFoo.run() outputs "foo". Do not change or remove this line.
            printFoo.run();
            
            this.semBar.release();
        }
        
    }

    public void bar(Runnable printBar) throws InterruptedException {
        
        
        for (int i = 0; i < n; i++) {
            this.semBar.acquire();
            
            // printBar.run() outputs "bar". Do not change or remove this line.
            printBar.run();
        
            this.semFoo.release();
        }
        
    }
}
{% endhighlight %}

If you are confused seeing the Semaphore getting initialized to zero, read [this post][semaphore-zero].

[leetcode]: https://leetcode.com/problems/print-foobar-alternately
[semaphore-zero] : https://stackoverflow.com/questions/25563640/difference-between-semaphore-initialized-with-1-and-0
