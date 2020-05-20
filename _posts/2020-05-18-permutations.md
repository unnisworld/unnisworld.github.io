---
layout: post
title:  "Permutations"
date:   2020-05-17
categories: permutation 
---

{% highlight java %}
public class GeneratePermutations {
    public static void main(String[] args) {
        String str = "GOD";
        permutate("", str);
    }

    private static void permutate(String curString, String remainingString) {
        if(remainingString.length() == 0) {
            System.out.println(curString);
            return;
        }

        for(int i=0;i<remainingString.length();i++) {
            String newCurString = curString + remainingString.charAt(i);
            String newRemainingString = remainingString.substring(0,i) +
                    remainingString.substring(i+1);
            permutate(newCurString, newRemainingString);
        }
    }
}

{% endhighlight %}

[desc]: https://www.techiedelight.com/generate-permutations-string-java-recursive-iterative/
