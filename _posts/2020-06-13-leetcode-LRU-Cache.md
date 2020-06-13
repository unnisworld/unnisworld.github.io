---
layout: post
title:  "Leetcode 146 : LRU Cache"
date:   2020-06-13 15:29:00 +0530
categories: leetcode leetcode-medium LinkedList
---

Solution to [LRU Cache][leetcode] problem.

{% highlight java %}
class LRUCache {
    
    private Map<Integer, Node> cache;
    private int c;
    private Node head = new Node(0, 0);
    private Node tail = new Node(0, 0);

    public LRUCache(int capacity) {
        this.cache = new HashMap<>(capacity);
        this.c = capacity;
        
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        int res = -1;
        if(cache.containsKey(key)) {
            Node n = cache.get(key);
            removeFromQ(n);
            addToQ(n);
            res = n.val;
        }
        
        return res;
    }
    
    public void put(int key, int value) {
        if(cache.containsKey(key)) {
            Node n = cache.get(key);
            n.val = value;
            removeFromQ(n);
            addToQ(n);
            return;
        }
        
        if(cache.size() == c) {
            Node nodeToBeRemoved = head.next;
            cache.remove(nodeToBeRemoved.key);
            removeFromQ(nodeToBeRemoved);
        }
        
        Node n = new Node(key, value);
        cache.put(key, n);
        addToQ(n);
    }
    
    private void removeFromQ(Node n) {
        n.prev.next = n.next;
        n.next.prev = n.prev;
    }
    
    private void addToQ(Node n) {
        n.next = tail;
        n.prev = tail.prev;
        tail.prev.next = n;
        tail.prev = n;
    }
    
    class Node {
        Node next, prev;
        int key;
        int val;
        
        Node(int key, int val) {
            this.key = key;
            this.val = val;
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/lru-cache/
