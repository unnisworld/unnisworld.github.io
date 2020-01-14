---
layout: post
title:  "Dijkstra’s Algorithm"
date:   2020-01-08 10:10:00 +0530
categories: algorithm graph ShortestPath DijkstrasAlgorithm
---
## A Gentle introduction to Dijkstra’s algorithm
Dijkstra’s algorithm, lets you answer “What’s the shortest path to X?” for `weighted graphs`. Remember, [BFS Algorithm][BSF-Algo] does the same thing for unweighted graphs. 

Dijkstra’s algorithm only works with directed acyclic graphs, called DAGs for short. In other words, If there are cycles in graphs, Dijkstra’s algorithm doesn’t work.

Dijkstra’s algorithm doesn’t work for graphs with negative weight edges. For graphs with negative weight edges, Bellman–Ford algorithm can be used

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

There are three steps to Dijkstra’s algorithm:

1.  `Find the next cheapest node`. This is the node you can get to, from your current location, in the least amount of time. Since you are starting from your `Start` position, the first cheapest node will be B.

2.  `Update total costs table`. Iterate over each of the neighbours of the current_cheapest_node and update the costs_table entry for the neighbour node. We need to keep in mind that costs_table entry keep track of the total cost incured to reach each node while following the `shortest known path` from the Start node. The costs_table is updated only if the new calculated cost is less than the current cost present in costs_table. Or in otherwords, the costs_table is updated only if the cost of new path is less than the cost of existing path.
 
3.  `Repeat` `1` followed by `2`, until you’ve done this for every node in the graph. We repeat this for every node only if our aim is to calcuate the shortest path to all the nodes present in the Graph from the Start node. If we are interested only in shortest distance from the source to a single target, we can break the for loop when the picked cheapest vertex is equal to the target node.

4.  Now you are done with Dijkstras algorithm. The cost of shortest path to all the Nodes is available in costs_table. Similarly, the actual Shortest path from Finish to Start (or any Node) can be deduced by backtracking on the parents_table. I will explain how to do this later.

Let's apply Dijkstra’s algorithm on our example Graph and see whether we are able to get the same shortest path that we got through manual inspection.

Step 1: Pick the cheapest node from costs_table. The generic algorithm to find the cheapest node is very simple. We just iterate over the entire costs_table and pick the least cost node that is not yet processed/visited. You may have this question in mind, the Algorithm says pick the least cost node from the current position. But the costs_table contains the summation of cost from the Start position. How does this approach (to find cheapest node) still work? That's because the cost to reach the current node from Start Node is a constant, say X. Then, what we have in costs_table is [X + w1, X + w2, X + w3] etc where w1, w2, w3 are edge weights of neighbours n1, n2, n3. With or without the X there, we will always get the least cost node, because comparing X + w1, X + w2 and X + w3 is same as comparing w1, w2 and w3.

At the very beginning of the iteration, the entries in costs_table are simple entries, meaning they are the distance from Start node to all other nodes.
{% highlight python %}
      Node   | Total cost to reach the Node
      A      | 6
      B      | 2
      Finish | Infinity (infinity because there is no direct path from Start to Finish and we do not know the actual distance)
{% endhighlight %}

From the costs_table we pick least cost node, which is Node B. 

Step 2: Update the costs_table for each of the neighbours of least cost node (currently Node B). Formula used will be new_cost = cost_to_reach_least_cost_node +  neighbours_edge_weight, which is new_cost = costs_table[least_cost_node] + neighbours_edge_weight, which is same as new_cost = costs_table[least_cost_node] + graph[least_cost_node][neighbour]. We replace the cost table entry only if new_cost is less than the existing cost. In otherwords, we replace the cost table entry only if new path is better than the existing path.

Since B is the least cost node, we get all neighbours of B, using graph[B].keys(). This will return A and Finish. So, try to update the costs_table entries for A and Finish. Current costs_table entry for A is 6, and the new_cost is costs_table[B] + edge_weight = 2 + 3 = 5. Since, new_cost is less that current entry we update the costs_table with new value.  

{% highlight python %}
      Node   | Total cost to reach the Node
      A      | 5
      B      | 2
      Finish | Infinity (infinity because there is no direct path and we do not know the actual distance)
{% endhighlight %}

Now, for Finish the current cost is Infinity. new_cost = costs_table[B] + edge_weight = 2 + 5 = 7.

{% highlight python %}
      Node   | Total cost to reach the Node
      A      | 5
      B      | 2
      Finish | 7
{% endhighlight %}

Step 3: Add B to processed/visited nodes list. Update parents_table entry for A and Finish this way, parents_table[A]='B' and parents_table[Finish]='B'. Basically, we are keeping a track of the path that we are following. We will discuss about why this is needed later.

Step 4: Pick the next least cost node from costs_table. This time, it will return A. B is not returned because, B is in the processed_nodes list.

Step 5: From here we can loop back to Step 2. But for the purpose of illustration, we will walk through the entire execution flow. So, in this step we update the costs_table for each of the neighbours of A based on the formula explained in Step 2. Node A has only one neighbour, Finish. The current cost for Finish is 7. The new_cost = costs_table[A] + edge_weight = 5 + 1 = 6. Hurrah!, we found a new path which is better than the currenty known best path. It takes only 6 mins to reach Finish through A compared to the previous time which was 7 mins. So we update the cost table accordingly.

{% highlight python %}
      Node   | Total cost to reach the Node
      A      | 5
      B      | 2
     `Finish | 6`
{% endhighlight %}

Step 6: Add A to processed/visited nodes list. Update parents_table entry for Finish. Basically, we will set parents_table[Finish]='A' to indicate that the path to Finish is through A.

Step 7: We again call find_lowest_cost_node, which will return the Finish node.

Step 8: There are no neighbours for Finish node. So, updation of costs_table gets skipped.

Step 9: We again go back to find_lowest_cost_node. This time it will return None, as all of the nodes are in the processed/visited node list. That marks the end of Dijkstra's algorithm execution. At this point, costs_table will have the cost of shortest path from Start node to any given node. For example, costs_table[Finish] will give cost of Shortest path from Start node to Finish node.

Step 10: In order to print the actual shortest path, we need to backtrack using the parents_table. parents_table['Finish'] will give parent of Finish. We will have to do this for every parent node, until we reach the Start node.

# Datastructures required to implement Dijkstra's Algorithm

1. HashTable to `represent the Graph`. It is actually a HashTable of HashTable. I will explain it later.
2. HashTable to `represent the cost from Start to the given node`. If cost is unknown we put infinity.
3. List to `track the parent node` of a given node

How do we `represent the Graph` with weight using HashTable? Based on our earlier strategy, we would have represented the connection from "Start" to A and B as follows,

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

## Naive Implementation of Dijkstra's Algorithm in Python
The aim here is to keep the code as simple as possible to understand. Some of the variable names have been stretched to the limit of identifier length possible in other languages. Thankfully, in Python identifiers are unlimited in length. Since the focus is on understanding the crux of the algorithm, some of the steps that is necessary to invoke the algorithm, like the initialization of parents_table and costs_table, has been hardcoded in Main method based on the example Graph that we are using for this blog. In subsequent iterations we will try to improve this implementation.

I could have written the algorithm in couple of different ways, One is to have a findShortestPath() method which takes a Graph, Start Node and End Node as input. Another is to take only the Graph and Start Node as parameter and compute the shortest path to every other Node in the Graph. Here, we have taken a different approach, thinking that it will keep things simple. We have an implementation called dijkstras_algo() which when executed with a set of necessary inputs, produces the results in costs_table and parents_table. After the execution of the routine, you will be able to get the cost of shortest path from Start node to any Node in the graph by looking up the entry in costs_table with that Node as the key. Similarly, you will be able to print the exact Shortest path by backtracking the entries in parents_table. 

While analysing the algorithm, a question that can popup in your mind is, we are not specifying the Start Node and Finish node. Then, how does this algorithm work? For now, you can skip this section and come back and read the explanation if such a question pops up later. If you carefully look at the costs_table initialization code, you will notice that the entry for Start node is missing. Basically, we have made those entries with the assumption that we are starting from the Start node and made entries for all other nodes based on the travel time of those nodes from the Start node. So the Start node problem is taken care of that way. Now for the Finish node, since the algorithm just computes the Shortest path for the entire Nodes in the Graph, this implementation does not need a Finish node value to break from the execution loop. It depends on the entries in processed_nodes to identify that all nodes are processed.

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
            # If it's cheaper to get to this neighbor by going through the current_lowest_cost_node...
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
    
#Main
# Start of Graph building
graph = {}
graph["Start"] = {}
graph["Start"]["A"] = 6
graph["Start"]["B"] = 2

graph["A"] = {}
graph["A"]["Finish"] = 1

graph["B"] = {}
graph["B"]["A"] = 3
graph["B"]["Finish"] = 5

graph["Finish"] = {}
# End of Graph building

# Initialize the parents table
# TODO : Can this be automated?
parents_table = {}
parents_table["A"] = "Start"
parents_table["B"] = "Start"
parents_table["Finish"] = None

# Initialize the costs table
# TODO : Add code to compute this based on 
# "Start" and "End" node inputs
infinity = float("inf")
costs_table = {}
costs_table["A"] = 6
costs_table["B"] = 2
costs_table["Finish"] = infinity

# List to keep track of visited nodes
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

# Print the results

print("Cost from the start to each node:", end=" ")
print(costs_table)

print("Shortest path from Start to Finish:", end= " ")

parent = "Finish"
while parent:
    print(parent, end="<-")
    parent = parents_table.get(parent, None)

{% endhighlight %}

You may spend sometime playing around with the [Live code][Dijkstra-Live] to get a hang of it.

Before we analyse this algorithm any further, one thing that we want to verify is the correctness of the implementation for atleast basic cases. For this I used the graph from [Geeks for Geeks][Geeks-for-Geeks-Graph-Question-1] and the output can be seen [here][Geeks-for-Geeks-Graph-Solution-1].

[BSF-Algo]: https://unnisworld.github.io/algorithm/graph/bfs/shortestpath/2020/01/08/Graph-BFS.html

[Python-tutor-1]: http://www.pythontutor.com/visualize.html#code=graph%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%5B%22A%22,%20%22B%22%5D&cumulative=false&curInstr=2&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

[Python-tutor-2]: http://www.pythontutor.com/visualize.html#code=graph%3D%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%5B%22A%22%5D%20%3D%206%0Agraph%5B%22Start%22%5D%5B%22B%22%5D%20%3D%202&cumulative=false&curInstr=4&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

[Dijkstra-Live]: http://www.pythontutor.com/visualize.html#code=def%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%3A%0A%20%20%20%20lowest_cost%20%3D%20float%28%22inf%22%29%0A%20%20%20%20lowest_cost_node%20%3D%20None%0A%20%20%20%20%23%20Go%20through%20each%20node.%0A%20%20%20%20for%20node%20in%20costs_table%3A%0A%20%20%20%20%20%20%20%20cost%20%3D%20costs_table%5Bnode%5D%0A%20%20%20%20%20%20%20%20%23%20If%20it's%20the%20lowest%20cost%20so%20far%20and%20hasn't%20been%20processed%20yet...%0A%20%20%20%20%20%20%20%20if%20cost%20%3C%20lowest_cost%20and%20node%20not%20in%20processed_nodes%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%23%20...%20set%20it%20as%20the%20new%20lowest-cost%20node.%0A%20%20%20%20%20%20%20%20%20%20%20%20lowest_cost%20%3D%20cost%0A%20%20%20%20%20%20%20%20%20%20%20%20lowest_cost_node%20%3D%20node%0A%20%20%20%20return%20lowest_cost_node%0A%0Adef%20dijkstras_algo%28graph,%20costs_table,%20parents_table,%20processed_nodes%29%3A%0A%20%20%20%20%23%20Find%20the%20lowest-cost%20node%20that%20you%20haven't%20processed%20yet.%0A%20%20%20%20current_lowest_cost_node%20%3D%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%0A%20%20%20%20%23%20If%20you've%20processed%20all%20the%20nodes,%20this%20while%20loop%20is%20done.%0A%20%20%20%20while%20current_lowest_cost_node%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20total_cost_to_reach_the_current_lowest_cost_node%20%3D%20costs_table%5Bcurrent_lowest_cost_node%5D%0A%20%20%20%20%20%20%20%20%23%20Go%20through%20all%20the%20neighbors%20of%20current_lowest_cost_node.%0A%20%20%20%20%20%20%20%20neighbors%20%3D%20graph%5Bcurrent_lowest_cost_node%5D%0A%20%20%20%20%20%20%20%20for%20n%20in%20neighbors.keys%28%29%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20neighbour_node_edge_weight%20%3D%20neighbors%5Bn%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20new_cost_to_reach_neighbour%20%3D%20total_cost_to_reach_the_current_lowest_cost_node%20%2B%20neighbour_node_edge_weight%0A%20%20%20%20%20%20%20%20%20%20%20%20%23%20If%20it's%20cheaper%20to%20get%20to%20this%20neighbor%20by%20going%20through%20the%20current_lowest_cost_node...%0A%20%20%20%20%20%20%20%20%20%20%20%20current_cost_to_reach_neighbour%20%3D%20costs_table%5Bn%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20%20new_cost_to_reach_neighbour%20%3C%20current_cost_to_reach_neighbour%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20...%20update%20the%20cost%20for%20this%20node.%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20costs_table%5Bn%5D%20%3D%20new_cost_to_reach_neighbour%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20This%20node%20becomes%20the%20new%20parent%20for%20this%20neighbor.%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20parents_table%5Bn%5D%20%3D%20current_lowest_cost_node%0A%20%20%20%20%20%20%20%20%23%20Mark%20the%20node%20as%20processed.%0A%20%20%20%20%20%20%20%20processed_nodes.append%28current_lowest_cost_node%29%0A%20%20%20%20%20%20%20%20%23%20Find%20the%20next%20node%20to%20process,%20and%20loop.%0A%20%20%20%20%20%20%20%20current_lowest_cost_node%20%3D%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%0A%20%20%20%20%0A%23Main%0A%23%20Start%20of%20Graph%20building%0Agraph%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%20%3D%20%7B%7D%0Agraph%5B%22Start%22%5D%5B%22A%22%5D%20%3D%206%0Agraph%5B%22Start%22%5D%5B%22B%22%5D%20%3D%202%0A%0Agraph%5B%22A%22%5D%20%3D%20%7B%7D%0Agraph%5B%22A%22%5D%5B%22Finish%22%5D%20%3D%201%0A%0Agraph%5B%22B%22%5D%20%3D%20%7B%7D%0Agraph%5B%22B%22%5D%5B%22A%22%5D%20%3D%203%0Agraph%5B%22B%22%5D%5B%22Finish%22%5D%20%3D%205%0A%0Agraph%5B%22Finish%22%5D%20%3D%20%7B%7D%0A%23%20End%20of%20Graph%20building%0A%0A%23%20Initialize%20the%20parents%20table%0A%23%20TODO%20%3A%20Can%20this%20be%20automated%3F%0Aparents_table%20%3D%20%7B%7D%0Aparents_table%5B%22A%22%5D%20%3D%20%22Start%22%0Aparents_table%5B%22B%22%5D%20%3D%20%22Start%22%0Aparents_table%5B%22Finish%22%5D%20%3D%20None%0A%0A%23%20Initialize%20the%20costs%20table%0A%23%20TODO%20%3A%20Add%20code%20to%20compute%20this%20based%20on%20%0A%23%20%22Start%22%20and%20%22End%22%20node%20inputs%0Ainfinity%20%3D%20float%28%22inf%22%29%0Acosts_table%20%3D%20%7B%7D%0Acosts_table%5B%22A%22%5D%20%3D%206%0Acosts_table%5B%22B%22%5D%20%3D%202%0Acosts_table%5B%22Finish%22%5D%20%3D%20infinity%0A%0A%23%20List%20to%20keep%20track%20of%20visited%20nodes%0Aprocessed_nodes%20%3D%20%5B%5D%0A%0A%23Dijkstra's%20Algorithm%20takes%20as%20input%20%0A%231.%20The%20Graph%0A%232.%20The%20costs%20table,%20which%20keeps%20track%20of%20the%20cost%20to%20reach%20each%20node%0A%23%20%20%20as%20we%20traverse%20through%20different%20lowest%20cost%20nodes.%0A%233.%20Parents%20table,%20this%20table%20is%20used%20to%20keep%20track%20of%20the%20parent%20node%0A%23%20%20%20for%20each%20lowest%20cost%20node%20that%20was%20picked%20during%20the%20algorithm%20execution.%0A%23%20%20%20The%20real%20use%20of%20this%20list%20is%20to%20build%20the%20actual%20shortest%20path%20at%20the%20end.%0A%234.%20List%20of%20Processed%20nodes%20to%20avoid%20duplicate%20processing.%20Every%20graph%20algorithm%20requires%0A%23%20%20%20such%20a%20list%20to%20keep%20track%20of%20already%20processed%20nodes.%20Otherwise,%20the%20algorithm%20will%0A%23%20%20%20go%20in%20infinate%20loop.%0Adijkstras_algo%28graph,%20costs_table,%20parents_table,%20processed_nodes%29%0A%0A%23%20Print%20the%20results%0A%0Aprint%28%22Cost%20from%20the%20start%20to%20each%20node%3A%22,%20end%3D%22%20%22%29%0Aprint%28costs_table%29%0A%0Aprint%28%22Shortest%20path%20from%20Start%20to%20Finish%3A%22,%20end%3D%20%22%20%22%29%0A%0Aparent%20%3D%20%22Finish%22%0Awhile%20parent%3A%0A%20%20%20%20print%28parent,%20end%3D%22%3C-%22%29%0A%20%20%20%20parent%20%3D%20parents_table.get%28parent,%20None%29&cumulative=false&curInstr=151&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false

[Geeks-for-Geeks-Graph-Question-1]: https://www.youtube.com/watch?v=ba4YGd7S-TY

[Geeks-for-Geeks-Graph-Solution-1]: http://www.pythontutor.com/visualize.html#code=def%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%3A%0A%20%20%20%20lowest_cost%20%3D%20float%28%22inf%22%29%0A%20%20%20%20lowest_cost_node%20%3D%20None%0A%20%20%20%20%23%20Go%20through%20each%20node.%0A%20%20%20%20for%20node%20in%20costs_table%3A%0A%20%20%20%20%20%20%20%20cost%20%3D%20costs_table%5Bnode%5D%0A%20%20%20%20%20%20%20%20%23%20If%20it's%20the%20lowest%20cost%20so%20far%20and%20hasn't%20been%20processed%20yet...%0A%20%20%20%20%20%20%20%20if%20cost%20%3C%20lowest_cost%20and%20node%20not%20in%20processed_nodes%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%23%20...%20set%20it%20as%20the%20new%20lowest-cost%20node.%0A%20%20%20%20%20%20%20%20%20%20%20%20lowest_cost%20%3D%20cost%0A%20%20%20%20%20%20%20%20%20%20%20%20lowest_cost_node%20%3D%20node%0A%20%20%20%20return%20lowest_cost_node%0A%0Adef%20dijkstras_algo%28graph,%20costs_table,%20parents_table,%20processed_nodes%29%3A%0A%20%20%20%20%23%20Find%20the%20lowest-cost%20node%20that%20you%20haven't%20processed%20yet.%0A%20%20%20%20current_lowest_cost_node%20%3D%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%0A%20%20%20%20%23%20If%20you've%20processed%20all%20the%20nodes,%20this%20while%20loop%20is%20done.%0A%20%20%20%20while%20current_lowest_cost_node%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20total_cost_to_reach_the_current_lowest_cost_node%20%3D%20costs_table%5Bcurrent_lowest_cost_node%5D%0A%20%20%20%20%20%20%20%20%23%20Go%20through%20all%20the%20neighbors%20of%20current_lowest_cost_node.%0A%20%20%20%20%20%20%20%20neighbors%20%3D%20graph%5Bcurrent_lowest_cost_node%5D%0A%20%20%20%20%20%20%20%20for%20n%20in%20neighbors.keys%28%29%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20neighbour_node_edge_weight%20%3D%20neighbors%5Bn%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20new_cost_to_reach_neighbour%20%3D%20total_cost_to_reach_the_current_lowest_cost_node%20%2B%20neighbour_node_edge_weight%0A%20%20%20%20%20%20%20%20%20%20%20%20%23%20If%20it's%20cheaper%20to%20get%20to%20this%20neighbor%20by%20going%20through%20the%20current_lowest_cost_node...%0A%20%20%20%20%20%20%20%20%20%20%20%20current_cost_to_reach_neighbour%20%3D%20costs_table%5Bn%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20if%20%20new_cost_to_reach_neighbour%20%3C%20current_cost_to_reach_neighbour%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20...%20update%20the%20cost%20for%20this%20node.%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20costs_table%5Bn%5D%20%3D%20new_cost_to_reach_neighbour%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20This%20node%20becomes%20the%20new%20parent%20for%20this%20neighbor.%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20parents_table%5Bn%5D%20%3D%20current_lowest_cost_node%0A%20%20%20%20%20%20%20%20%23%20Mark%20the%20node%20as%20processed.%0A%20%20%20%20%20%20%20%20processed_nodes.append%28current_lowest_cost_node%29%0A%20%20%20%20%20%20%20%20%23%20Find%20the%20next%20node%20to%20process,%20and%20loop.%0A%20%20%20%20%20%20%20%20current_lowest_cost_node%20%3D%20find_lowest_cost_node%28costs_table,%20processed_nodes%29%0A%20%20%20%20%0A%23Main%0A%23%20Start%20of%20Graph%20building%0Agraph%20%3D%20%7B%7D%0Agraph%5B%22A%22%5D%20%3D%20%7B%7D%0Agraph%5B%22A%22%5D%5B%22B%22%5D%20%3D%2010%0Agraph%5B%22A%22%5D%5B%22C%22%5D%20%3D%2015%0A%0Agraph%5B%22B%22%5D%20%3D%20%7B%7D%0Agraph%5B%22B%22%5D%5B%22C%22%5D%20%3D%205%0Agraph%5B%22B%22%5D%5B%22D%22%5D%20%3D%2016%0A%0Agraph%5B%22C%22%5D%20%3D%20%7B%7D%0Agraph%5B%22C%22%5D%5B%22D%22%5D%20%3D%2020%0A%0Agraph%5B%22D%22%5D%20%3D%20%7B%7D%0A%23%20End%20of%20Graph%20building%0A%0A%23%20Initialize%20the%20parents%20table%0A%23%20TODO%20%3A%20Can%20this%20be%20automated%3F%0Aparents_table%20%3D%20%7B%7D%0Aparents_table%5B%22B%22%5D%20%3D%20%22A%22%0Aparents_table%5B%22C%22%5D%20%3D%20%22A%22%0Aparents_table%5B%22D%22%5D%20%3D%20None%0A%0A%23%20Initialize%20the%20costs%20table%0A%23%20TODO%20%3A%20Add%20code%20to%20compute%20this%20based%20on%20%0A%23%20%22Start%22%20and%20%22End%22%20node%20inputs%0Ainfinity%20%3D%20float%28%22inf%22%29%0Acosts_table%20%3D%20%7B%7D%0Acosts_table%5B%22B%22%5D%20%3D%2010%0Acosts_table%5B%22C%22%5D%20%3D%2020%0Acosts_table%5B%22D%22%5D%20%3D%20infinity%0A%0A%23%20List%20to%20keep%20track%20of%20visited%20nodes%0Aprocessed_nodes%20%3D%20%5B%5D%0A%0A%23Dijkstra's%20Algorithm%20takes%20as%20input%20%0A%231.%20The%20Graph%0A%232.%20The%20costs%20table,%20which%20keeps%20track%20of%20the%20cost%20to%20reach%20each%20node%0A%23%20%20%20as%20we%20traverse%20through%20different%20lowest%20cost%20nodes.%0A%233.%20Parents%20table,%20this%20table%20is%20used%20to%20keep%20track%20of%20the%20parent%20node%0A%23%20%20%20for%20each%20lowest%20cost%20node%20that%20was%20picked%20during%20the%20algorithm%20execution.%0A%23%20%20%20The%20real%20use%20of%20this%20list%20is%20to%20build%20the%20actual%20shortest%20path%20at%20the%20end.%0A%234.%20List%20of%20Processed%20nodes%20to%20avoid%20duplicate%20processing.%20Every%20graph%20algorithm%20requires%0A%23%20%20%20such%20a%20list%20to%20keep%20track%20of%20already%20processed%20nodes.%20Otherwise,%20the%20algorithm%20will%0A%23%20%20%20go%20in%20infinate%20loop.%0Adijkstras_algo%28graph,%20costs_table,%20parents_table,%20processed_nodes%29%0A%0A%23%20Print%20the%20results%0A%0Aprint%28%22Cost%20from%20the%20start%20to%20each%20node%3A%22,%20end%3D%22%20%22%29%0Aprint%28costs_table%29%0A%0Aprint%28%22Shortest%20path%20from%20Start%20to%20Finish%3A%22,%20end%3D%20%22%20%22%29%0A%0Aparent%20%3D%20%22D%22%0Awhile%20parent%3A%0A%20%20%20%20print%28parent,%20end%3D%22%3C-%22%29%0A%20%20%20%20parent%20%3D%20parents_table.get%28parent,%20None%29&cumulative=false&curInstr=144&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false