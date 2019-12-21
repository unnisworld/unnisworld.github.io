---
layout: post
title:  "Nth Fibonacci"
date:   2019-12-20 17:47:00 +0530
categories: algorithm easy-algorithm algo-warmup
---
Problem Statement : Write a function to return the Nth Fibonacci number, where N is the parameter to the function. 

Fibonacci series : `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...`

Mathematical formula :

{% highlight python %}
fib(1) = 0, fib(2) = 1 
fib(n) = fib(n-1) + fib(n-2) for n > 2
{% endhighlight %}

## Fibonacci sequence using recursion

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

The space complexity of this approach is O(n) because in total there are `n recursive calls`, each using the callstack to store execution data including the intermeidate result. 

## Optimized Fibonacci sequence using recursion and memoization

If you look at the execution sequence of the previous implementation, you can see that there are a lot of duplicate computations happening. For example, when you computing fib(5), the call to calculate fib(3) is done twice. 

{% highlight java %}
	fib(5) = fib(4) + fib(3)
	fib(5) = (fib(3) + fib(2)) + fib(3)
	fib(5) = ((fib(2) + fib(1)) + fib(2)) + (fib(2) + fib(1))
{% endhighlight %}

The idea here is to optimize the execution by introducing a cache to store the intermediate results. In the above example, first time when fib(3) is called, the result of that will be placed in a cache and when second time fib(3) is called, the result will be returned from the cache. This technique is called [Memoization] [memoization-technique]. 

Given below is the memoized version of `getNthFib`. 

{% highlight python %}
# time O(n)
# space O(n)
def getNthFib(n, memoize = {1: 0, 2: 1}):
    if n in memoize:
        return memoize[n]
    else:
        memoize[n] = getNthFib(n - 1, memoize) + getNthFib(n - 2, memoize)
        return memoize[n]

#main     
print(getNthFib(10)) 
{% endhighlight %}

With this approach the time complexity comes down to O(n). The space complexity also will be O(n), because we are storing all the intermediate results in memory.

## Iterative solution

Finally, we will look at an iterative solution which runs in O(n) time complexity and O(1) space complexity. This approach uses two temp variables (stored in lastTwoResults) to store the previous two intermediate results. The counter is initialized to 3 because, the first two results are already given as base case and its the 3rd result that we want to start computing from.

{% highlight python %}
# time O(n)
# space O(1)
def getNthFib(n):
    lastTwoResults = [0, 1]
    counter = 3

    while counter <= n:
        nextFib = lastTwoResults[0] + lastTwoResults[1]
        lastTwoResults[0] = lastTwoResults[1]
        lastTwoResults[1] = nextFib
        counter +=1

    return lastTwoResults[1] if n > 1 else lastTwoResults[0]    
        
#main     
print(getNthFib(10))
{% endhighlight %}

Hope it was a nice warmup exercise to start with the algorithm learning process.

[recurrence-relation]: https://mathinsight.org/definition/recurrence_relation
[time-complexity-of-fib-sequence]: https://www.youtube.com/watch?v=pqivnzmSbq4
[memoization-technique]: https://en.wikipedia.org/wiki/Memoization
