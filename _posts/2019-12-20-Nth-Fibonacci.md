---
layout: post
title:  "Nth Fibonacci"
date:   2019-12-20 17:47:00 +0530
categories: algorithm easy-algorithm
---
Problem Statement : Write a function to return the Nth Fibonacci number, where N is the parameter to the function. 

Fibonacci series : `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...`

Mathematical formula :

{% highlight python %}
fib(1) = 0, fib(2) = 1 
fib(n) = fib(n-1) + fib(n-2) for n > 2
{% endhighlight %}

A naive implementation to calculate `Nth Fibonacci` using recursion will be :

{% highlight python %}
# time O(2^n)
# space O(n)
def getNthFib(n):
    if n == 2:
        return 1
    elif n == 1:
        return 0
    else:
        return getNthFib(n - 1) + getNthFib(n - 2)

def main():
    # This should print 34 as answer
    print(getNthFib(10))

main()  
{% endhighlight %}

The Java implementation of the same would be : 

{% highlight java %}
public class Main {
    public static void main(String[] args) {
      System.out.println(getNthFibonacci(10));
    }
    
    public static int getNthFibonacci(int n) {
      if (n == 2)
        return 1;
      if (n == 1)
        return 0;
        
      return getNthFibonacci(n - 1) + getNthFibonacci(n - 2); 
    }  
}
{% endhighlight %}

The time complexity of this approach is 2^n (`exponential`). That's because, at every step except for the base case, the problem gets divided into 2 sub problems and this happens n times, which gives 2^n. For a more thorough mathematical analysis of the time complexity using [recurrence relation] [recurrence-relation], have a look at this [Youtube video] [time-complexity-of-fib-sequence].

[recurrence-relation]: https://mathinsight.org/definition/recurrence_relation
[time-complexity-of-fib-sequence]: https://www.youtube.com/watch?v=pqivnzmSbq4   
