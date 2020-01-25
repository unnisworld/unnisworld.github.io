---
layout: post
title:  "Integer to Roman Conversion"
date:   2020-01-25 08:48:00 +0530
categories: leetcode-medium leetcode general-algo 
---

Solution to [integer to roman conversion leetcode problem][leetcode-integer-to-roman].

{% highlight java %}
import java.util.LinkedHashMap;
import java.util.Map;

public class IntToRoman {

    private static Map<Integer, String> romanSymbolTable = new LinkedHashMap<>();

    static {
        romanSymbolTable.put(1, "I");
        romanSymbolTable.put(4, "IV");
        romanSymbolTable.put(5, "V");
        romanSymbolTable.put(9, "IX");
        romanSymbolTable.put(10, "X");
        romanSymbolTable.put(40, "XL");
        romanSymbolTable.put(50, "L");
        romanSymbolTable.put(90, "XC");
        romanSymbolTable.put(100, "C");
        romanSymbolTable.put(400, "CD");
        romanSymbolTable.put(500, "D");
        romanSymbolTable.put(900, "CM");
        romanSymbolTable.put(1000, "M");
    }

    public static void main(String[] args) {
        System.out.println(intToRoman(6));
        System.out.println(intToRoman(101));
    }

    public static String intToRoman(int num) {
        int numForProcessing = num;

        StringBuilder builder = new StringBuilder();

        while (numForProcessing > 0) {
            if (romanSymbolTable.containsKey(numForProcessing)) {
                builder.append(romanSymbolTable.get(numForProcessing));
                numForProcessing = 0;
            } else {
                int additionFactor = getLargestPossibleAdditionFactor(numForProcessing);
                builder.append(romanSymbolTable.get(additionFactor));
                numForProcessing = numForProcessing - additionFactor;
            }
        }

        return builder.toString();
    }

    private static int getLargestPossibleAdditionFactor(int numForProcessing) {
        int temp = 0;
        for (int key : romanSymbolTable.keySet()) {
            if (key < numForProcessing) {
                temp = key;
            } else {
                break;
            }
        }
        return temp;
    }
}
{% endhighlight %}

A more concise solution is given below :

{% highlight java %}
    public String intToRoman(int num) {
        String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < values.length; i++) {
            if (num == 0) break;
            if (values[i] <= num) {
                int times = num / values[i];
                for (int j = 0; j < times; j++) {
                    sb.append(symbols[i]);
                }
                num = num % values[i];
            }
        }
        return sb.toString();
    }
{% endhighlight %}

[leetcode-integer-to-roman]: https://leetcode.com/problems/integer-to-roman/
