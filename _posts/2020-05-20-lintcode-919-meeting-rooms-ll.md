---
layout: post
title:  "LintCode 919 : Meeting Rooms ll same as LeetCode 253. Meeting Rooms II"
date:   2020-05-20
categories: lintcode-medium PriorityQueue Microsoft
---

Solution to [Meeting Rooms 2][leetcode] Problem. A gentle intro to [PriorityQueue][pq] is available [here][pq].


{% highlight java %}
public class Solution {
    /**
     * @param intervals: an array of meeting time intervals
     * @return: the minimum number of conference rooms required
     */
    public int minMeetingRooms(List<Interval> intervals) {
        // Write your code here
        Collections.sort(intervals, (a,b) -> a.start - b.start);
        
        PriorityQueue<Interval> pq = new PriorityQueue<>(intervals.size(), 
            (a,b) -> a.end - b.end);
        
        for(Interval i : intervals) {
            if(!pq.isEmpty() && i.start >= pq.peek().end) {
                Interval ir = pq.poll(); // we can reuse a room
            }
            
            pq.offer(i);
        }
        
        return pq.size();
    }
}
{% endhighlight %}

Time complexity : O(N Log N)
1. Sort takes N Log N.
2. Insert to PQ happens N times. Each insert/remove costs Log(N). So, all PQ operations also will result in N Log N time.

Space complexity : O(N). Worst case we will store all entries in PQ.

Another solution that does not use PriorityQueue.
{% highlight java %}
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        int[][] endTimeSortedIntervals = intervals.clone();
        Arrays.sort(intervals, (a,b) -> a[0] - b[0]);
        Arrays.sort(endTimeSortedIntervals, (a,b) -> a[1] - b[1]);
        
        int rc = 0;
        int j = 0;
        for(int[] i : intervals) {
            if(endTimeSortedIntervals[j][1] <= i[0]) {
                j++;
            } else {
                rc++;
            }
        }
        return rc;
    }
}
{% endhighlight %}

[leetcode]: https://www.lintcode.com/problem/meeting-rooms-ii/description
[pq]: https://www.educative.io/edpresso/min-heap-vs-max-heap
