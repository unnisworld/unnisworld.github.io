---
layout: post
title:  "Python Lists"
date:   2019-12-20 17:47:00 +0530
categories: python list
---

In Python, a list is a dynamic array. You can create one like this:

{% highlight python %}
lst = [] # Declares an empty list named lst
{% endhighlight %}

Or you can fill it with items:

{% highlight python %}
lst = [1,2,3]
{% endhighlight %}

You can add items using "append":

{% highlight python %}
lst.append('a')
{% endhighlight %}

You can iterate over elements of the list using the for loop:

{% highlight python %}
for item in lst:
    # Do something with item
{% endhighlight %}

Or, if you'd like to keep track of the current index:

{% highlight python %}
for idx, item in enumerate(lst):
    # idx is the current idx, while item is lst[idx]
{% endhighlight %}

To remove elements, you can use the del command or the remove function as in:

{% highlight python %}
del lst[0] # Deletes the first item
lst.remove(x) # Removes the first occurence of x in the list
{% endhighlight %}

Note, though, that one cannot iterate over the list and modify it at the same time; to do that, you should instead iterate over a slice of the list (which is basically a copy of the list). As in:

{% highlight python %}
for item in lst[:]: # Notice the [:] which makes a slice
       # Now we can modify lst, since we are iterating over a copy of it
{% endhighlight %}

Taken from this [Stackoverflow response][stackoverflow-link].

[stackoverflow-link]: https://stackoverflow.com/questions/2910864/in-python-how-can-i-declare-a-dynamic-array               