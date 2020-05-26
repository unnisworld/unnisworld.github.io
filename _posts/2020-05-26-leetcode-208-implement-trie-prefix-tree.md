---
layout: post
title:  "LeetCode 208 : Implement Trie"
date:   2020-05-26
categories: leetcode-medium leetcode Trie Tree
---

Solution to [Implement Trie][leetcode] Problem.

{% highlight java %}
public class Trie {

    private TrieNode root = new TrieNode();

    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("apple");
        trie.insert("app");
        trie.insert("application");
        trie.insert("bat");
        trie.insert("batminton");

        List<String> suggestions = trie.suggest("ba");
        System.out.println(suggestions);
    }

    public List<String> suggest(String prefix) {
        List<String> suggestions = new ArrayList<>();
        TrieNode cur = searchPrefix(prefix);

        if(cur != null) {
            collectAllWords(cur, prefix, suggestions);
        }

        return suggestions;
    }

    private void collectAllWords(TrieNode cur, String prefix, List<String> words) {
        if(cur == null)
            return;
        if(cur.isEnd()) {
            words.add(prefix);
        }

        for(int i=0;i<cur.children.length;i++) {
            collectAllWords(cur.children[i], prefix + (char)('a' + i), words);
        }
    }

    public void insert(String word) {
        TrieNode cur = root;
        for(char c : word.toCharArray()) {
            if(!cur.containsKey(c)) {
                cur.put(c, new TrieNode());
            }
            cur = cur.get(c);
        }
        cur.setEnd();
    }

    public boolean search(String word) {
        TrieNode node = searchPrefix(word);
        return node != null && node.isEnd();
    }

    public TrieNode searchPrefix(String prefix) {
        TrieNode cur = root;
        for(char c : prefix.toCharArray()) {
            if(cur.containsKey(c)) {
                cur = cur.get(c);
            } else {
                return null;
            }
        }
        return cur;
    }

    static class TrieNode {
        private static int CHARS = 26;
        private boolean isEnd;
        private TrieNode[] children;

        public TrieNode() {
            children = new TrieNode[CHARS];
        }

        public void put(char ch, TrieNode node) {
            children[ch - 'a'] = node;
        }

        public TrieNode get(char ch) {
            return children[ch - 'a'];
        }

        public boolean isEnd() {
            return isEnd;
        }

        public void setEnd() {
            isEnd = true;
        }

        public boolean containsKey(char ch) {
            return children[ch - 'a'] != null;
        }
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/implement-trie-prefix-tree/
