---
layout: post
title:  "Leetcode 211 : Add and Search Word - Data structure design"
date:   2020-06-13 15:29:00 +0530
categories: leetcode leetcode-medium Trie
---

Solution to [Add and Search Word - Data structure design][leetcode] problem.

{% highlight java %}
class WordDictionary {

    TrieNode root;
    /** Initialize your data structure here. */
    public WordDictionary() {
        root = new TrieNode();
    }
    
    /** Adds a word into the data structure. */
    public void addWord(String word) {
        TrieNode cur = root;
        for(char c : word.toCharArray()) {
            if(!cur.containsKey(c)) {
                cur.put(c, new TrieNode());
            }
            cur = cur.get(c);
        }
        cur.setWordEnd();
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        return searchRecursive(root, word, 0);
    }
    
    private boolean searchRecursive(TrieNode cur, String word, int pos) {
        if(pos == word.length()) {
            return cur.isWordEnd();
        }
        if(cur == null) {
            return false;
        }
        
        char c = word.charAt(pos);
        if(c == '.') {
            for(char c2 : cur.children.keySet()) {
                if(searchRecursive(cur.get(c2), word, pos+1)) {
                    return true;
                }
            }
        }
        
        if(!cur.containsKey(c)) {
            return false;
        }
        
        return searchRecursive(cur.get(c), word, pos+1);
    }
    
    static class TrieNode {
        private Map<Character, TrieNode> children = new HashMap<>();
        private boolean isWordEnd;
        
        public void put(Character c, TrieNode node) {
            children.put(c, node);
        }
        
        public TrieNode get(Character c) {
            return children.get(c);
        }
        
        public void setWordEnd() {
            isWordEnd = true;
        }
        
        public boolean isWordEnd() {
            return isWordEnd;
        }
        
        public boolean containsKey(Character c) {
            return children.containsKey(c);
        }
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/add-and-search-word-data-structure-design/
