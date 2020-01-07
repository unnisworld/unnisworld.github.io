---
layout: post
title:  "Quick Sort"
date:   2020-01-07 11:14:00 +0530
categories: algorithm easy-algorithm algo-warmup
---
A concise python code for quick sort is given below :

{% highlight python %}
# time O(n^2)
# average time O(n log n)
# space O(n) - The code uses duplicate arrays instead of performing inplace sorting.
#              This is done to simplify the implementation.    
def quicksort(array):
    if len(array) < 2:
        return array
    else:
        pivot = array[0]
        less = [i for i in array[1:] if i < pivot]
        greater = [i for i in array[1:] if i > pivot]
        return quicksort(less) + [pivot] + quicksort(greater)

#main
print(quicksort([10,5,2,3]))
{% endhighlight %}

Quick sort is a divide and conquer algorithm. A divide and conquer algorithm works by recursively breaking down a problem into two or more sub-problems of the same or related type, until these become simple enough to be solved directly. This implementation of the algorithm is very simple. 

Simple case of quick sort : The simple case of quick sort is when input array size is 0 or 1, in which case the array is already sorted. 
How quick sort does Recursive breakdown of problem : It picks a pivot element, in our implementation, the first element of the array. Creates two subarrays, less and greater, in such a way that less contains all elements less than pivot and greater contains all elements greater than pivot. Since pivot is a single element array, it is already sorted. Not just that, by seperating out less elements and greater elements into two different arrays, we have inadvertently found the position of pivot element in the final sorted array. Also, final sorted array = quicksort([less]) + [pivot] + quicksort([greater]).

## Time complexity analysis of quick sort
The time complexity analysis of quick sort is slightly tricky. The worst case time complexity of quick sort is O(n^2) and the average case complexity is O(n log n). Even with such bad Big(O), Quick sort is still a widely popular sorting algorithm. We will get to the reasons of that in a while.

First, lets try to understand how the average case complexity of Quick sort is O(n log n). In an ideal execution flow, quick sort divides the problem space into two equal sub-problems in each iteration/recursive call. The best way to understand this would be to write down the less, pivot and greater for an array of size 8 eg: [10,7,8,6,1,5,2,3]. 

{% highlight python %}
1. array = [10,7,8,6,1,5,2,3], pivot = <10>, less = [7,8,6,1,5,2,3], greater = []
2. array = [7,8,6,1,5,2,3],    pivot = <7> , less = [6,1,5,2,3],     greater = [8]
3. array = [6,1,5,2,3],        pivot = <6>,  less = [1,5,2,3],       greater = []
4. array = [1,5,2,3],          pivot = <1>,  less = [],              greater = [5,2,3]
5. array = [5,2,3],            pivot = <5>,  less = [2,3],           greater = []
6. array = [2,3],              pivot = <2>,  less = [],              greater = [3]
7. array = [3]
{% endhighlight %}

Try tracing the execution steps using the [python-tutor] [Python Tutor live editor].

In this example, the execution went till 7 levels. The maximum levels that such an execution can go, when quick sort is able to divide the the input array into almost equal parts is, log n. If the input array size is 8, max height or level can go till 3 (because 2^3 = 8). Similarlly, if the input array size is 16, the max height or level can go till 4 (because 2^4 = 16). To say it in a different way, for every execution, quick sort divides the problem space into half (or divides it by 2). How many times can you divide 16 using 2, 4 times. How may times can you divide 8 using 2, 3 times. That's another way to understand it. 

With that, we understood that the average height of the execution stack can be `log n`. Now, in each level, we will have to do `at max n comparisons` to arrive at less and greater arrays. In other words each of the other element will have to be compared against pivot to determine whether to place that element in less or in greater. So, n comparisons in each level. That gives us a total time complexity of `O(n log n)`.

Now, we will try to understand why the above is not the worst case complexity of quick sort. Consider an already sorted array, with the pivot picking strategy that we have in place, the height of the execution stack will go upto `n`. In otherwords quick sort is not able to divide the problem space into two equal sub-problems. So, worst case height of n multiplied by n comparisons gives us worst case complexity or Big O (n^2).

Now coming to the last part, why is quick sort still popular? If you look at the worst case complexity of merge sort, it is only O(n log n). So obviously, merge sort is more stable. So, should we always use merge sort instead of quick sort. The answer is not that straight forward. There are scenarios where quick sort is preferred over merge sort. Generally for smaller datasets quick sort is preferred over merge sort. We will try to understand the reason for that. Consider, a function that prints out all elements in an array :

{% highlight python %}
def print_items(list):
  for item in list:
    print item  
{% endhighlight %}

The complexity of this function is O(n). Now consider below variant of this function,

{% highlight python %}
from time import sleep
def print_items2(list):
  for item in list:
  	sleep(1)
    print item  
{% endhighlight %}

This function, sleeps 1 second before printing out each element. But the Big O of this function is still O(n). The actual Big O of this function is O(n) + C, where C is some constant. For larger values of n, C becomes insignificant, so we ignore C in Big O analysis. But, what if n is small, then C can make a difference while comparing algorithms. This is what happens while comparing merge sort and quick sort for smaller values of n. The constant C for merge sort is really large that for smaller values of n, quick sort is better option. Another point to keep in mind is that, the performance of quick sort depends on the selection of pivot. In the implementation above we used the first element as pivot. It was done to keep the implementation simple. But that resulted in bad performace for already sorted array. A better alternative would be to pick the middle element as pivot.    

A more detailed explanation of the comparison of quick sort and merge sort is available in [gorkking-algorithms] [this excellent book].

[python-tutor] - http://www.pythontutor.com/live.html#mode=edit
[gorkking-algorithms] - https://www.amazon.in/Grokking-Algorithms-illustrated-programmers-curious/dp/1617292230
