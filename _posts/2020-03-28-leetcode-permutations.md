---
layout: post
title:  "Permutations"
date:   2020-03-28 20:45:00 +0530
categories: leetcode leetcode-medium Permutations
---

Solution to [Permutations][leetcode] problem. It took some time for me to understand how to code it. [This video] [video] really helped in understanding how to implement it. 

If the input elements are [1,2,3], lets see how we can come up with different combinations of these elements.

First we have all 3 elements for selection. Let's call this the possible selection list (possibleSelections). We will also have another list the to keep track of already selected elements, which we will call already selected list (alreadySelected). Let's say we first select [1], we are left with [2,3] in the possible selection list. Then we pick 2, that makes the already selected list [1,2] and the possible selections list [3]. Now we pick 3, which makes alreadySelected list [1,2,3] and possibleSelections list [] or empty. That means, we have formed one possible permutation.

The execution flows through the 16 steps given below,

1.  Main calls the recursive function with possibleSelections list = [1,2,3] and alreadySelected list = [].
2.  possibleSelections=[2,3]   alreadySelected=[1]
3.  possibleSelections=[3]     alreadySelected=[1,2]
4.  possibleSelections=[]      alreadySelected=[1,2,3] --> There is nothing left to select. Add [1,2,3] to o/p 
5.  possibleSelections=[2]     alreadySelected=[1,3]
6.  possibleSelections=[]      alreadySelected=[1,3,2] --> There is nothing left to select. Add [1,3,2] to o/p 

7.  possibleSelections=[1,3]   alreadySelected=[2]
8.  possibleSelections=[3]     alreadySelected=[2,1]
9.  possibleSelections=[]      alreadySelected=[2,1,3] --> There is nothing left to select. Add [2,1,3] to o/p
10. possibleSelections=[1]     alreadySelected=[2,3]
11. possibleSelections=[]      alreadySelected=[2,3,1] --> There is nothing left to select. Add [2,3,1] to o/p  
12. possibleSelections=[1,2]   alreadySelected=[3]
13. possibleSelections=[2]     alreadySelected=[3,1]
14. possibleSelections=[]      alreadySelected=[3,1,2] --> There is nothing left to select. Add [3,1,2] to o/p
15. possibleSelections=[1]     alreadySelected=[3,2]
16. possibleSelections=[]      alreadySelected=[3,2,1] --> There is nothing left to select. Add [3,2,1] to o/p

{% highlight java %}
class Solution {
    
    public List<List<Integer>> permute(int[] nums) {
        List<Integer> possibleSelections = new ArrayList<>();
        for(int i : nums) {
            possibleSelections.add(i);
        }
        
        List<List<Integer>> answers = new ArrayList<>();
        List<Integer>  alreadySelected = new ArrayList<>();
        buildPermutations(possibleSelections, alreadySelected, answers);
        
        return answers;
    }
    
    private static void buildPermutations(List<Integer> possibleSelections,
            List<Integer> alreadySelected, List<List<Integer>> answers) {
        if(possibleSelections.size() == 0) {
            answers.add(new ArrayList(alreadySelected));
            return;
        }

        for(int i=0;i<possibleSelections.size();i++) {
            // Step 1 : select one element from possible selections
            int currentSelection = possibleSelections.get(i);
            alreadySelected.add(currentSelection);

            // Step 2 : filter out current selection from possible selections.
            List<Integer> restOfThePossibleSelections = possibleSelections.stream()
                    .filter(n -> n != currentSelection).collect(Collectors.toList());

            // Step 3 : build permutations using rest of the possible selections
            buildPermutations(restOfThePossibleSelections, alreadySelected, answers);

            // Step 4 : Remove current selection from already selected list.
            alreadySelected.remove(Integer.valueOf(currentSelection));
        }
    }
}
{% endhighlight %}

Once you understand this logic, you can try to grasp the below solution for printing permutations of a String, which is written in a more crisp way.

{% highlight java %}
public class StringPermutation {
    public static void main(String[] args) {
        String str = "ABC";

        permutate(str, "");
    }

    private static void permutate(String possibleSelections, String alreadySelected) {
        if(possibleSelections.length()==0) {
            System.out.println(alreadySelected);
        } else {
            for(int i=0;i<possibleSelections.length();i++) {
                String remaining = possibleSelections.substring(0, i) + possibleSelections.substring(i+1);
                permutate(remaining, alreadySelected + possibleSelections.charAt(i));
            }
        }
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/permutations/
[video]: https://www.youtube.com/watch?v=KukNnoN-SoY
