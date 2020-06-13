---
layout: post
title:  "Leetcode 1472 : Design Browser History"
date:   2020-06-13 14:20:00 +0530
categories: leetcode leetcode-medium Stack
---

Solution to [Design Browser History][leetcode] problem.

{% highlight java %}
class BrowserHistory {
    
    private Stack<String> bs = new Stack<>();
    private Stack<String> fs = new Stack<>();
    private String curPage;
    
    public BrowserHistory(String homepage) {
        curPage = homepage;
    }
    
    public void visit(String url) {
        bs.push(curPage);
        curPage = url;
        fs.clear();
    }
    
    public String back(int steps) {
        while(steps > 0 && !bs.isEmpty()) {
            fs.push(curPage);
            curPage = bs.pop();
            steps--;
        }
        
        return curPage;
    }
    
    public String forward(int steps) {
        while(steps > 0 && !fs.isEmpty()) {
            bs.push(curPage);
            curPage = fs.pop();
            steps--;
        }
        
        return curPage;
    }
}

/**
 * Your BrowserHistory object will be instantiated and called as such:
 * BrowserHistory obj = new BrowserHistory(homepage);
 * obj.visit(url);
 * String param_2 = obj.back(steps);
 * String param_3 = obj.forward(steps);
 */
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/design-browser-history/
