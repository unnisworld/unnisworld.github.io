---
layout: post
title:  "LeetCode 48 : Rotate Image"
date:   2020-05-21
categories: leetcode-medium leetcode array matrix
---

Solution to [Rotate Image][leetcode] Problem. Here is a [nice video][utube] which explains the approach.

{% highlight java %}
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        // Steps : 
        //  1. Transpose the matrix : means - change row to column
        for(int i=0;i< n;i++) {
            for(int j=i;j< n;j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
        
        // 2. Reverse the rows
        for(int i=0;i<n; i++) {
            for(int j=0;j< n/2;j++) {
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[i][n - j - 1];
                matrix[i][n - j - 1] = tmp;
            }
        }
        
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/rotate-image/
[utube]: https://www.youtube.com/watch?v=SA867FvqHrM
