---
layout: post
title: "Leetcode 692. Top K Frequent Words"
date: 2023-12-30
categories: leetcode leetcode-medium Heap PriorityQueue Kth-problem
---

Solution to [Top K Frequent Wordsy][leetcode] problem.

{% highlight java %}
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        HashMap<String, Integer> freqMap = new HashMap<String, Integer>();

        for(String word : words) {
            int curFreq = freqMap.getOrDefault(word, 0);
            freqMap.put(word, ++curFreq);
        }

		PriorityQueue<String> minHeap = new PriorityQueue<String>(
			(s1, s2) -> {
				if (freqMap.get(s1) == freqMap.get(s2)) return s2.compareTo(s1);
				return freqMap.get(s1) - freqMap.get(s2);
			});

        for(Map.Entry<String, Integer> e : freqMap.entrySet()) {
			minHeap.add(e.getKey());
			
			if (minHeap.size() > k) {
				System.out.println("Evicting "+ minHeap.poll());
			}
		}

        List<String> r = new ArrayList<String>();
        System.out.println("Heap contains ");
		while(minHeap.size() > 0) {
            String e = minHeap.poll();
			System.out.println(e);
            r.add(e);
		}

        Collections.reverse(r);

        return r;
    }
}
{% endhighlight %}

Checkout [this nice solution with explanation][nice-solution] in leetcode community.

[leetcode]:https://leetcode.com/problems/top-k-frequent-words/description/
[nice-solution]:https://leetcode.com/problems/top-k-frequent-words/solutions/4428763/java-hashmap-heap-priorityqueue/