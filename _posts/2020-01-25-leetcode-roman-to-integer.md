---
layout: post
title:  "Roman to Integer Conversion"
date:   2020-01-25 12:18:00 +0530
categories: leetcode-medium leetcode general-algo 
---

Solution to [roman to integer conversion leetcode problem][leetcode-roman-to-integer].

{% highlight java %}
class Solution {
    public int romanToInt(String ip) {
        Map<String, Integer> romanSymbolTable = new LinkedHashMap<>();
        romanSymbolTable.put("I", 1);
        romanSymbolTable.put("IV", 4);
        romanSymbolTable.put("V", 5);
        romanSymbolTable.put("IX", 9);
        romanSymbolTable.put("X", 10);
        romanSymbolTable.put("XL", 40);
        romanSymbolTable.put("L", 50);
        romanSymbolTable.put("XC", 90);
        romanSymbolTable.put("C", 100);
        romanSymbolTable.put("CD", 400);
        romanSymbolTable.put("D", 500);
        romanSymbolTable.put("CM", 900);
        romanSymbolTable.put("M", 1000);
        
        int result = 0;
        if (ip == null || ip.isBlank()) {
            return -1;
        }

        if (romanSymbolTable.get(ip) != null) {
            return romanSymbolTable.get(ip);
        }

        for(int i=0;i<ip.length();i++) {
            char currentChar = ip.charAt(i);
            char nextChar = " ".toCharArray()[0];
            if (i+1 < ip.length())
                nextChar = ip.charAt(i+1);
            String key = currentChar + "" + nextChar;
            if (romanSymbolTable.get(key) != null) {
                result = result + romanSymbolTable.get(key).intValue();
                i++; //skip two chars
            } else if (romanSymbolTable.get(currentChar+"") != null) {
                result = result + romanSymbolTable.get(currentChar+"").intValue();
            } else {
                throw new RuntimeException("Unrecognized char ["+currentChar+"] in input.");
            }
        }

        return result;
    }
}
{% endhighlight %}

[leetcode-roman-to-integer]: https://leetcode.com/problems/roman-to-integer
