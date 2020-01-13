---
layout: post
title:  "Dijkstra’s Algorithm"
date:   2020-01-08 10:10:00 +0530
categories: algorithm graph ShortestPath DijkstrasAlgorithm
---
Dijkstra’s algorithm, lets you answer “What’s the shortest path to X?” for `weighted graphs`. Remember, [BFS Algorithm][BSF-Algo] does the same thing for unweighted graphs. Dijkstra’s algorithm only works with directed acyclic graphs, called DAGs for short. In other words, If there are cycles in graphs, Dijkstra’s algorithm doesn’t work.

# WORKING WITH DIJKSTRA’S ALGORITHM

When you work with Dijkstra’s algorithm, each edge in the graph has a number associated with it. These are called weights.

Given below is a weighted graph where numbers on the edges denotes the travel time to reach from one vertex to another. If we apply the normal BFS algorithm on this graph, the shortest path from Start to Finish would be (Start)->(A)->(Finish) or even (Start)->(B)->(Finish). The travel time for this path is 6 + 1 = 7 minutes (or 2 + 5 = 7 mins). On an Eyeball inspection we can see that there is a path with shorter travel time, (Start)->(B)->(A)->(Finish) which has a total travel time of 2 + 3 + 1 = 6 minutes.

{% highlight python %}
         ( A )
       `/``|` \		
      6/   |   \1
      /    |    \
     /    3|     \
    /      |     `\`  
(Start)    |   (Finish)
   \       |      `/` 
    \      |      /  
    2\     |     /5
      \    |    /
       \   |   /
       `\` |  /
         ( B )

 `Red tick` indicates an Arrow.        
 {% endhighlight %}

Let's apply Dijkstra’s algorithm and see whether we are able to get the same shortest path. There are four steps to Dijkstra’s algorithm:
1.  `Find the next cheapest node`. This is the node you can get to, from your current location, in the least amount of time. Since you always start from your `Start` position, the first cheapest node will be B.

2.  `Update total cost table`. Check whether there’s a cheaper path to the neighbors of this node. If so, update their costs in the total cost table. For a path to qualify as cheaper path, the `new_total_cost` must be less than the `current_total_cost` entry present in `total cost table`.

3.  `Repeat` `1` followed by `2`, until you’ve done this for every node in the graph.

4.  `Calculate the final path`. (Coming up later!)

Let's apply this algorithm on our Graph and see.

 Step 1: The cheapest node from `Start` Node is Node `B`.

 Step 2: Update the total_distance table. Formula used will be total_distance[node] distance from `Start` to all Nodes in the table.

 {% highlight python %}
 			Node   | Time to Node
 			A      | 6
 			B      | 2
 			Finish | Infinity (infinity because we do not know the actual distance) 
 {% endhighlight %}

Step 3: Select B and move to B as B is the cheapest node.

Step 4: Update the distance table based on distance from B to each of these nodes. We need to keep two things in mind, 

  `1.` That the `distance table` tracks the shortest distance. We compute the new shortest distance by adding the distance from `Start` to `the current node` with the `distance from current node` to the node which is the `hashtable key`.

  `2.` The `distance table` is updated with new distance only if the newly computed distance is less than the current entry.

{% highlight python %}
    Node   | Time to Node
    A      | 5 (2+3, `dist from Start to B` + `dist from B to A`)
    B      | 2
    Finish | 7 (2+5, `dist from Start to B` + `dist from B to Finish`) 
 {% endhighlight %}

Step 5: Find the next cheapest `unvisited` node from the cost table, which will be `Node A`.

Step 6: Update the cost for Node A's neighbours
{% highlight python %}
			Node   | Time to Node
			A      | 5
			B      | 2
			Finish | 6 (2 + 3 + 1)		
 {% endhighlight %}

 ## Datastructures required to implement Dijkstra's Algorithm
 1. To `represent the Graph`.
 2. To `represent the cost from Start to the given node`. If cost is unknown we put infinity.
 3. To `track the parent node` of a given node

 How do we `represent the Graph` with weight using HashTable? Based on our earlier strategy we would have represented the connection from "Start" to A and B as follows,

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

## Dijkstra's Algorithm
{% highlight python %}
def find_lowest_cost_node(costs_table, processed_nodes):
    lowest_cost = float("inf")
    lowest_cost_node = None
    # Go through each node.
    for node in costs_table:
        cost = costs_table[node]
        # If it's the lowest cost so far and hasn't been processed yet...
        if cost < lowest_cost and node not in processed_nodes:
            # ... set it as the new lowest-cost node.
            lowest_cost = cost
            lowest_cost_node = node
    return lowest_cost_node

def dijkstras_algo(graph, costs_table, parents_table, processed_nodes):
    # Find the lowest-cost node that you haven't processed yet.
    current_lowest_cost_node = find_lowest_cost_node(costs_table, processed_nodes)
    # If you've processed all the nodes, this while loop is done.
    while current_lowest_cost_node is not None:
        total_cost_to_reach_the_current_lowest_cost_node = costs_table[current_lowest_cost_node]
        # Go through all the neighbors of current_lowest_cost_node.
        neighbors = graph[current_lowest_cost_node]
        for n in neighbors.keys():
            neighbour_node_edge_weight = neighbors[n]
            new_cost_to_reach_neighbour = total_cost_to_reach_the_current_lowest_cost_node + neighbour_node_edge_weight
            # If it's cheaper to get to this neighbor by going through this node...
            current_cost_to_reach_neighbour = costs_table[n]
            if  new_cost_to_reach_neighbour < current_cost_to_reach_neighbour:
                # ... update the cost for this node.
                costs_table[n] = new_cost_to_reach_neighbour
                # This node becomes the new parent for this neighbor.
                parents_table[n] = current_lowest_cost_node
        # Mark the node as processed.
        processed_nodes.append(current_lowest_cost_node)
        # Find the next node to process, and loop.
        current_lowest_cost_node = find_lowest_cost_node(costs_table, processed_nodes)
    
    print("Cost from the start to each node:")
    print(costs_table)
    #TODO : Add code to print shortest path
    
#Main
# the graph
graph = {}
graph["start"] = {}
graph["start"]["a"] = 6
graph["start"]["b"] = 2

graph["a"] = {}
graph["a"]["fin"] = 1

graph["b"] = {}
graph["b"]["a"] = 3
graph["b"]["fin"] = 5

graph["fin"] = {}

# the costs table
infinity = float("inf")
costs_table = {}
costs_table["a"] = 6
costs_table["b"] = 2
costs_table["fin"] = infinity

# the parents table
parents_table = {}
parents_table["a"] = "start"
parents_table["b"] = "start"
parents_table["fin"] = None

processed_nodes = []

#Dijkstra's Algorithm takes as input 
#1. The Graph
#2. The costs table, which keeps track of the cost to reach each node
#   as we traverse through different lowest cost nodes.
#3. Parents table, this table is used to keep track of the parent node
#   for each lowest cost node that was picked during the algorithm execution.
#   The real use of this list is to build the actual shortest path at the end.
#4. List of Processed nodes to avoid duplicate processing. Every graph algorithm requires
#   such a list to keep track of already processed nodes. Otherwise, the algorithm will
#   go in infinate loop.
dijkstras_algo(graph, costs_table, parents_table, processed_nodes)

{% endhighlight %}

You may spend sometime playing around with the [Live code][Dijkstra-Live] to get a hang of it. You may notice that the parents table is not really used in the given code. We will get to that later. For now, just keep in mind that this table will be required to print the actual path from "Start" to "Finish".

[BSF-Algo]: https://unnisworld.github.io/algorithm/graph/bfs/shortestpath/2020/01/08/Graph-BFS.html

[Python-tutor-1]: http://www.pythontutor.com/visualize.html#code=graph%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%5B%22A%22,%20%22B%22%5D&cumulative=false&curInstr=2&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

[Python-tutor-2]: http://www.pythontutor.com/visualize.html#code=graph%3D%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%5B%22A%22%5D%20%3D%206%0Agraph%5B%22Start%22%5D%5B%22B%22%5D%20%3D%202&cumulative=false&curInstr=4&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

[Dijkstra-Live]: http://www.pythontutor.com/visualize.html#code=def%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%3A%0A%20%20%20%20lowest_cost%20%3D%20float%28%22inf%22%29%0A%20%20%20%20lowest_cost_node%20%3D%20None%0A%20%20%20%20%23%20Go%20through%20each%20node.%0A%20%20%20%20for%20node%20in%20costs_table%3A%0A%20%20%20%20%20%20%20%20cost%20%3D%20costs_table%5Bnode%5D%0A%20%20%20%20%20%20%20%20%23%20If%20it's%20the%20lowest%20cost%20so%20far%20and%20hasn't%20been%20processed%20yet...%0A%20%20%20%20%20%20%20%20if%20cost%20%3C%20lowest_cost%20and%20node%20not%20in%20processed_nodes%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%23%20...%20set%20it%20as%20the%20new%20lowest-cost%20node.%0A%20%20%20%20%20%20%20%20%20%20%20%20lowest_cost%20%3D%20cost%0A%20%20%20%20%20%20%20%20%20%20%20%20lowest_cost_node%20%3D%20node%0A%20%20%20%20return%20lowest_cost_node%0A%0Adef%20dijkstras_algo%28graph,%20costs_table,%20parents_table,%20processed_nodes%29%3A%0A%20%20%20%20%23%20Find%20the%20lowest-cost%20node%20that%20you%20haven't%20processed%20yet.%0A%20%20%20%20current_lowest_cost_node%20%3D%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%0A%20%20%20%20%23%20If%20you've%20processed%20all%20the%20nodes,%20this%20while%20loop%20is%20done.%0A%20%20%20%20while%20current_lowest_cost_node%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20total_cost_to_reach_the_current_lowest_cost_node%20%3D%20costs_table%5Bcurrent_lowest_cost_node%5D%0A%20%20%20%20%20%20%20%20%23%20Go%20through%20all%20the%20neighbors%20of%20current_lowest_cost_node.%0A%20%20%20%20%20%20%20%20neighbors%20%3D%20graph%5Bcurrent_lowest_cost_node%5D%0A%20%20%20%20%20%20%20%20for%20n%20in%20neighbors.keys%28%29%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20neighbour_node_edge_weight%20%3D%20neighbors%5Bn%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20new_cost_to_reach_neighbour%20%3D%20total_cost_to_reach_the_current_lowest_cost_node%20%2B%20neighbour_node_edge_weight%0A%20%20%20%20%20%20%20%20%20%20%20%20%23%20If%20it's%20cheaper%20to%20get%20to%20this%20neighbor%20by%20going%20through%20this%20node...%0A%20%20%20%20%20%20%20%20%20%20%20%20current_cost_to_reach_neighbour%20%3D%20costs_table%5Bn%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20%20new_cost_to_reach_neighbour%20%3C%20current_cost_to_reach_neighbour%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20...%20update%20the%20cost%20for%20this%20node.%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20costs_table%5Bn%5D%20%3D%20new_cost_to_reach_neighbour%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20This%20node%20becomes%20the%20new%20parent%20for%20this%20neighbor.%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20parents_table%5Bn%5D%20%3D%20current_lowest_cost_node%0A%20%20%20%20%20%20%20%20%23%20Mark%20the%20node%20as%20processed.%0A%20%20%20%20%20%20%20%20processed_nodes.append%28current_lowest_cost_node%29%0A%20%20%20%20%20%20%20%20%23%20Find%20the%20next%20node%20to%20process,%20and%20loop.%0A%20%20%20%20%20%20%20%20current_lowest_cost_node%20%3D%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%0A%20%20%20%20%0A%20%20%20%20print%28%22Cost%20from%20the%20start%20to%20each%20node%3A%22%29%0A%20%20%20%20print%28costs_table%29%0A%20%20%20%20%23TODO%20%3A%20Add%20code%20to%20print%20shortest%20path%0A%20%20%20%20%0A%23Main%0A%23%20the%20graph%0Agraph%20%3D%20%7B%7D%0Agraph%5B%22start%22%5D%20%3D%20%7B%7D%0Agraph%5B%22start%22%5D%5B%22a%22%5D%20%3D%206%0Agraph%5B%22start%22%5D%5B%22b%22%5D%20%3D%202%0A%0Agraph%5B%22a%22%5D%20%3D%20%7B%7D%0Agraph%5B%22a%22%5D%5B%22fin%22%5D%20%3D%201%0A%0Agraph%5B%22b%22%5D%20%3D%20%7B%7D%0Agraph%5B%22b%22%5D%5B%22a%22%5D%20%3D%203%0Agraph%5B%22b%22%5D%5B%22fin%22%5D%20%3D%205%0A%0Agraph%5B%22fin%22%5D%20%3D%20%7B%7D%0A%0A%23%20the%20costs%20table%0Ainfinity%20%3D%20float%28%22inf%22%29%0Acosts_table%20%3D%20%7B%7D%0Acosts_table%5B%22a%22%5D%20%3D%206%0Acosts_table%5B%22b%22%5D%20%3D%202%0Acosts_table%5B%22fin%22%5D%20%3D%20infinity%0A%0A%23%20the%20parents%20table%0Aparents_table%20%3D%20%7B%7D%0Aparents_table%5B%22a%22%5D%20%3D%20%22start%22%0Aparents_table%5B%22b%22%5D%20%3D%20%22start%22%0Aparents_table%5B%22fin%22%5D%20%3D%20None%0A%0Aprocessed_nodes%20%3D%20%5B%5D%0A%0A%23Dijkstra's%20Algorithm%20takes%20as%20input%20%0A%231.%20The%20Graph%0A%232.%20The%20costs%20table,%20which%20keeps%20track%20of%20the%20cost%20to%20reach%20each%20node%0A%23%20%20%20as%20we%20traverse%20through%20different%20lowest%20cost%20nodes.%0A%233.%20Parents%20table,%20this%20table%20is%20used%20to%20keep%20track%20of%20the%20parent%20node%0A%23%20%20%20for%20each%20lowest%20cost%20node%20that%20was%20picked%20during%20the%20algorithm%20execution.%0A%23%20%20%20The%20real%20use%20of%20this%20list%20is%20to%20build%20the%20actual%20shortest%20path%20at%20the%20end.%0A%234.%20List%20of%20Processed%20nodes%20to%20avoid%20duplicate%20processing.%20Every%20graph%20algorithm%20requires%0A%23%20%20%20such%20a%20list%20to%20keep%20track%20of%20already%20processed%20nodes.%20Otherwise,%20the%20algorithm%20will%0A%23%20%20%20go%20in%20infinate%20loop.%0Adijkstras_algo%28graph,%20costs_table,%20parents_table,%20processed_nodes%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false