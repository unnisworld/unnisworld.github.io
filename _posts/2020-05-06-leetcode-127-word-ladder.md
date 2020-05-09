---
layout: post
title:  "Leetcode 127 : Word Ladder"
date:   2020-05-06
categories: leetcode-medium leetcode BFS
---

Solution to [Word Ladder][leetcode] Problem. This [video][utube] has the explanation.

{% highlight java %}
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> set = new HashSet<>();
        for(String s : wordList)
            set.add(s);
        
        if(!set.contains(endWord))
            return 0;
        
        Queue<String> q = new LinkedList<>();
        q.add(beginWord);
        int level = 1;
        while(!q.isEmpty()) {
            int qs = q.size();
            for(int i=0;i<qs;i++) {
                String curWord = q.poll();
                char[] curWordChars = curWord.toCharArray();
                for(int j=0;j<curWordChars.length;j++) {
                    char originalChar = curWordChars[j];
                    for(char c='a';c<='z';c++) {
                        if(curWordChars[j] == c) continue;
                        curWordChars[j] = c;
                        String newWord = String.valueOf(curWordChars);
                        if(endWord.equals(newWord)) 
                            return level + 1;
                        
                        if(set.contains(newWord)) {
                            q.offer(newWord);
                            set.remove(newWord);
                        }    
                    }
                    curWordChars[j] = originalChar;
                }
                
            }
            
            level++;
        }
        
        return 0;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/word-ladder/
[utube]: https://www.youtube.com/watch?v=M9cVl4d0v04