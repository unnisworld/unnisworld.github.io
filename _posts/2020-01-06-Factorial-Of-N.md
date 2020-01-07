---
layout: post
title:  "Nth Factorial"
date:   2020-01-06 12:03:00 +0530
categories: algorithm easy-algorithm algo-warmup
---
Problem Statement : Write a function to return the Factorial of N, where N is the parameter to the function. 

Factorial of N or N! : `N * (N-1) * (N-2) *... * 2 * 1` where 0! is 1 by definition.

Mathematical formula :

{% highlight python %}
fact(0) = 1 
fact(n) = n * fact(n-1) for n > 0
{% endhighlight %}

## Factorial using recursion

{% highlight python %}
# time O(n)
# space O(n)
def fact(n):
	if n == 0:
		return 1
	else:
		return n * fact(n-1)
{% endhighlight %}		

Algorithm Analysis :
T(0) = 1 (by definition 0! is 1, so it takes constant time to compute 0!)
T(n) = T(n-1) + 3 (where 3 is for 3 constant operations like comparison, substraction and multiplication)

T(n) = T(n-2) + 6
T(n) = T(n-3) + 9
.
.
.
T(n) = T(n-k) + 3k
When k reaches n or in other words k=n,
T(n) = T(n-n) + 3n  
T(n) = T(0) + 3n
T(n) = 1 + 3n

T(N) is directly proportional to n,

Therefore, The time complexity of recursive factorial is O(n). As there is no extra space taken during the recursive calls other than the call stack space,the space complexity is also O(N).

A more detailed analysis of the time complexity can be found [here] [time-complexity-of-factorial].

## Optimized Factorial using recursion and memoization

Unlike the fibonacci problem where memoization improved the time complexity from O(2^n) to O(n), here even with memoization, the time complexity remains O(n). You can see that the memoization technique improves the performance of subsequent calls for factorial of a number. The answer has to be computed and stored once for all input n's.

{% highlight python %}
# time O(n)
# space O(n)
def fact(n, memoize = {0:1}):
	if n in memoize:
		return memoize[n]
	else:
		result = n * fact(n-1, memoize)
		memoize[n] = result
		return result
{% endhighlight %}

[time-complexity-of-factorial]: https://stackoverflow.com/questions/2327244/complexity-of-recursive-factorial-program