---
layout: post
title:  "Dijkstra’s Algorithm"
date:   2020-01-08 08:35:00 +0530
categories: algorithm graph ShortestPath DijkstrasAlgorithm
---
Dijkstra’s algorithm, lets you answer “What’s the shortest path to X?” for `weighted graphs`. Dijkstra’s algorithm only works with directed acyclic graphs, called DAGs for short. In other words, If there are cycles in graphs, Dijkstra’s algorithm doesn’t work.

# WORKING WITH DIJKSTRA’S ALGORITHM

When you work with Dijkstra’s algorithm, each edge in the graph has a number associated with it. These are called weights.

Given below is a weighted graph where numbers on the edges denotes the travel time to reach from one vertex to another. If we apply the normal BFS algorithm on this graph, the shortest path from Start to Finish would be (Start)->(A)->(Finish). The travel time for this path is 6 + 1 = 7 minutes. On an Eyeball inspection we can see that there is a path with shorter travel time, (Start)->(B)->(A)->(Finish) which has a total travel time of 2 + 3 + 1 = 6 minutes.

{% highlight python %}
       (A)
       /|\		
     6/	| \1
     /  |  \
    /  3|   \
(Start) |  (Finish)
    \   |   / 
     \  |  /  
     2\ | /5
       \|/ 
       (B)
 {% endhighlight %}

Let's apply Dijkstra’s algorithm and see whether we are able to get the same shortest path. There are four steps to Dijkstra’s algorithm:
1.  Find the cheapest node. This is the node you can get to in the least amount of time.

2.  Check whether there’s a cheaper path to the neighbors of this node. If so, update their costs.

3.  Repeat until you’ve done this for every node in the graph.

4.  Calculate the final path. (Coming up in the next section!)

 Step 1: The cheapest node from Start is Node B. 
 Step 2: Update the distance from Start to all Nodes in the table.
 {% highlight python %}
 			Node   | Time to Node
 			A      | 6
 			B      | 2
 			Finish | Infinity (infinity because we do not know the actual distance) 
 {% endhighlight %}

Step 3: Select B and move to B as B is the cheapest node.
Step 4: Update the distance table based on distance from B to each of these nodes.
{% highlight python %}
			Node   | Time to Node
			A      | 5 (2 + 3)
			B      | 2
			Finish | 7 (5 + 2) 
 {% endhighlight %}

Step 5: Find the next cheapest node, which is A.
Step 6: Update the cost for Node A's neighbours
{% highlight python %}
			Node   | Time to Node
			A      | 5
			B      | 2
			Finish | 6 (2 + 3 + 1)		
 {% endhighlight %}

 # We need 3 hashtables 
 1. To represent the Graph
 2. To represent the cost from Start to the given node. If cost is unknown we put infinity.
 3. To track the parent node of a given node

 How do we represent a Graph with weight using HashTable? Based on our earlier strategy we would have represented the connection from "Start" to A and B as follows,

{% highlight python %}
graph = {}
graph["Start"] = ["A", "B"]
{% endhighlight %} 

You may have a look at the visualization [here] [Python-tutor-1].

But, where do we put the weight corresponding to A and B? Again, hashtable comes to our rescue. Instead of placing an Array within a HashTable entry, we are going to place a HashTable within the HashTable.  

{% highlight python %}
graph={}
graph["Start"] = {}
graph["Start"]["A"] = 6
graph["Start"]["B"] = 2
{% endhighlight %} 

Just to reiterate the point, in earlier representation of Graph graph["Start"] would return a List containing the neighbours of `"Start"` node, namely `["A", "B"]`.

In the new representation, graph["Start"] would return a HashTable who's key/value pair represents the neighbour node and the distance of neighbour node from `"Start"` node, namely `{"A" : 6, "B", 2}`. 

Again, the best way to understand this is to visualize it using [PythonTutor] [Python-tutor-2].

[Python-tutor-1]: http://www.pythontutor.com/visualize.html#code=graph%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%5B%22A%22,%20%22B%22%5D&cumulative=false&curInstr=2&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

[Python-tutor-2]: http://www.pythontutor.com/visualize.html#code=graph%3D%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%5B%22A%22%5D%20%3D%206%0Agraph%5B%22Start%22%5D%5B%22B%22%5D%20%3D%202&cumulative=false&curInstr=4&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false






