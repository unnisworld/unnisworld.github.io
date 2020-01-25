---
layout: post
title:  "Integer to Roman Conversion"
date:   2020-01-25 08:48:00 +0530
categories: leetcode-medium leetcode general-algo 
---

Solution to [integer to roman conversion leetcode problem][leetcode-integer-to-roman].

{% highlight java %}
class Solution {
    public String intToRoman(int num) {
        StringBuilder resultStore = new StringBuilder();
        String[] st = new String[] {"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C", "CD", "D", "CM", "M"};
        int[] nt = new int[]       { 1,    4,   5,    9,   10,  40,   50,  90,   100, 400,  500, 900,  1000};

        int mutableNum = num;

        for (int i=nt.length-1; i>=0; i--) {
            if (mutableNum == 0)
                break;
            if (nt[i] == mutableNum) {
                resultStore.append(st[i]);
                break;
            }
            else if (nt[i] < mutableNum) {
                int otherFactor = mutableNum / nt[i];
                for(int j=0;j<otherFactor;j++)
                    resultStore.append(st[i]);

                mutableNum = mutableNum % nt[i];
            }
        }

        return resultStore.toString();
    }

}
{% endhighlight %}

[leetcode-integer-to-roman]: https://leetcode.com/problems/integer-to-roman/
