---
layout: post
title:  "Merge Sort"
date:   2020-05-17
categories: sort 
---

{% highlight java %}
import java.util.Arrays;

public class MergeSort {
    public static void main(String[] args) {
        int[] a = {5,1,6,2,3,4,7,8,9,10};
        sort(a, 0, a.length-1);

        System.out.println("Sorted array :"+ Arrays.toString(a));
    }

    private static void sort(int[] a, int l, int r) {
        if (l >= r)
            return;

        int m = (l+r)/2;
        sort(a, l, m);
        sort(a, m+1, r);

        merge(a,l, m, r);
    }

    private static void merge(int[] a, int l, int m, int r) {
        int n1 = m - l + 1;   // +1 is needed : think 0, 4, 9
        int n2 = r - m;

        int[] L = new int[n1];
        int[] R = new int[n2];

        for(int i=0;i<n1;i++)
            L[i] = a[l+i];
        for(int i=0;i<n2;i++)
            R[i] = a[m+1+i];

        // Initial indexes of first and second subarrays
        int i=0, j=0;

        // initial index of merge array
        int k = l;
        while(i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                a[k++] = L[i++];
            } else {
                a[k++] = R[j++];
            }
        }

        while(i<n1)
            a[k++] = L[i++];

        while(j<n2)
            a[k++] = R[j++];
    }
}

{% endhighlight %}

[desc]: https://leetcode.com/problems/k-closest-points-to-origin/discuss/220235/Java-Three-solutions-to-this-classical-K-th-problem.
