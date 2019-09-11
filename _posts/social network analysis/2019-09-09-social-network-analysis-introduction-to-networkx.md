---
layout: post
title: Social Network Analysis in Python - Introduction to NetworkX
categories: [Social Network Analysis]
tags: ["#python &nbsp; #networkx"]
---
<p align="left"> <span style="color:darkblue; font-family:Calibri; font-size: 110%;"> <em> #python &nbsp;  #networkx </em></span> </p>

![background-picture]({{site.baseurl}}/assets/networkx.png)

<br>
NetworkX is a Python library for working with graphs and perform analysis on them. 
It has built-in many fancy features like algorithms for creating specific graphs genres, 
or some centrality measures. But in this article we concentrate on work at grassroots - how 
to create graph, add and remove nodes and edges, add weighted edges, inspect graph properties an visualize graphs. 

<p style="
border:1px; 
border-style:solid; 
border-color:#E0E0E0; 
padding: 1em;
margin: 25px;
width: 90%;"  
>“By definition, a Graph is a collection of nodes (vertices) along with identified pairs of nodes 
(called edges, links, etc). In NetworkX, nodes can be any hashable object e.g., a text string, 
an image, an XML object, another Graph, a customized node object, etc.”
<br> <cite>&mdash; NetworkX documentation </cite>
</p>

Content below is based on very good NetworkX [documentation](https://networkx.github.io/documentation/stable/) where you can go deeper into NetworkX. 
In this post you may see simple examples how to use code.

<p style="
border:3px; 
border-style:solid; 
border-color:#42649c; 
padding: 1em;
width: 65%;
"
> <strong>Contents:</strong> 
<br>
<strong>1. </strong> Create a graph 
<br> 
<strong>2. </strong> Add nodes, edges, weighted edges to a graph
<br> 
<strong>3. </strong> Add attributes to graphs, nodes, edges
<br>
<strong>4. </strong> Check a graph properties
<br> 
<strong>5. </strong> Access edges and neighbors 
<br> 
<strong>6. </strong> Draw graphs
<br> 
<strong>7. </strong> Graphs I/O in GML format
</p>

<div style="line-height:50%;"> <br> </div>
## 1. Create a graph

### Create an empty graph


```python
# Import library
import networkx as nx
```


```python
# Create an empty graph - collection of nodes
G = nx.Graph()
```


```python
# Create a directed graph using connections from the previous graph G
H = nx.DiGraph(G)
```


```python
# Clear the graph from all nodes and edges 
# it deletes also graph attributes, nodes attributes and edges attributes.
G.clear()
```

### Create a graph from list of edges


```python
# Create a list of edges (list of tuples)
edgelist = [(0, 1), (1, 2), (2, 3)]
```


```python
# Create a graph
H = nx.Graph(edgelist)
```


```python
# Draw a graph
%matplotlib inline

# Draw a plot
nx.draw(H, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```
&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_11_1.png)


### Create a graph from an adjacency matrix


```python
# Create an adjacency matrix
import numpy as np
adj_m = np.array([[0, 1, 1],
                  [1, 1, 1],
                  [0, 1, 0]])
```


```python
# Create a graph
G = nx.from_numpy_matrix(adj_m)
```


```python
# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_12_0.png)


### Create a chain graph


```python
# Create a chain graph (5 nodes from 0 to 4)
H = nx.path_graph(5)
```


```python
# Draw the graph
nx.draw(H, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```

&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_13_0.png)



## 2. Add nodes, edges, weighted edges to a graph

### Add nodes to a graph


```python
# Create an empty graph
G = nx.Graph()
```


```python
# Add a node 
G.add_node(1)

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_15_0.png)



```python
# Add a list of nodes
G.add_nodes_from([2, 3])

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)

```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_16_0.png)



```python
# Create a chain graph (5 nodes from 0 to 4)
H = nx.path_graph(5)
# Show created nodes
H.nodes
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeView((0, 1, 2, 3, 4))

```python
# Add nodes from the graph H to the graph G (nodes 1,2,3 are overwrited)
G.add_nodes_from(H)
G.nodes
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeView((1, 2, 3, 0, 4))



We can see above that numbers play role of something like keys of particular nodes in graph. And this nodes may be overwritten. 


```python
# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_20_0.png)



```python
# Add a node as a string label
G.add_node("la") # adds node "la"
G.nodes
```

&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>

    NodeView((1, 2, 3, 0, 4, 'la'))




```python
# Add nodes as single string elements
G.add_nodes_from("la")  # adds 2 nodes: 'l', 'a'
G.nodes
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeView((1, 2, 3, 0, 4, 'la', 'l', 'a'))



### Remove nodes from the graph


```python
# Remove a node
G.remove_node(2)

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_24_0.png)



```python
# Remove nodes from an iterable container
G.remove_nodes_from([3,4])

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_25_0.png)


### Add edges to a graph


```python
# Create an empty graph
G = nx.Graph()

# Add an edge between node 1 and node 2
G.add_edge(1, 2)

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_27_0.png)


We can see above that if an edge is created - all needed non-existing nodes are created as well.


```python
# Create a tuple with 2, 3
e = (2, 3)
type(e)
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    tuple




```python
# Use the tuple to create an edge between nodes 2 and 3
G.add_edge(*e)
G.edges
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeView([(1, 2), (2, 3)])




```python
# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_31_0.png)



```python
# Create a chain graph (5 nodes from 0 to 4)
H = nx.path_graph(5)
# Add edges to graph G from graph H
G.add_edges_from(H.edges)
G.edges
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeView([(1, 2), (1, 0), (2, 3), (3, 4)])




```python
# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_33_0.png)



```python
# Add an edge between node 3 and non-existing node m - which is automatically
#                                                                  created
G.add_edge(3, 'm')
```


```python
# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_35_0.png)


### Remove edges from a graph


```python
# Remove an edge
G.remove_edge(1, 2)

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_37_0.png)



```python
# Remove edges from an iterable container
G.remove_edges_from([(2, 3),(3,4)])

# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_38_0.png)


### Add weighted edges to a graph


```python
# Create an empty graph
G = nx.Graph()

# Add an edge with weight as a tuple with a dictionary inside on a 3rd position  
G.add_edge(0, 1, weight=2.8)
```


```python
G.edges
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeView([(0, 1)])




```python
# Compute a position of the graph elements (needed to visualize weighted graphs)
pos = nx.spring_layout(G)
# Draw the graph
nx.draw(G, pos = pos, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
# Add weights to the graph picture
nx.draw_networkx_edge_labels(G, pos)
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {(0, 1): Text(0.0, 0.0, "{'weight': 2.8}")}




&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_42_1.png)


### Create Erdős-Rényi graph

For an example we use Erdős-Rényi graph generation. It takes only one short line of code. This is a simple and powerful way of creating graphs. Method "erdos_renyi_graph()" takes 2 arguments. 1st is number of nodes, and second one is probability that a node will get an edge connection with every other particular node. So if more nodes, probability of node having any edge rise.


```python
# Import library
import random
import numpy as np

# Generate Erdos-renyi graph 
G = nx.gnp_random_graph(6,0.4) # (gnp alias from: G-raph, N-odes, 
                               #                    P-robability)
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_45_0.png)


### Add random weights to the graph


```python
# add random weights 
for u,v,d in G.edges(data=True):
    d['weight'] = round(random.random(),2) # there we may set distribution
    # in this loop we iterate over a tuples in a list
    #                    u - is actually 1st node of an edge
    #                    v - is second node of an edge
    #                    d - is dict with weight of edge

# Extract tuples of adges, and weights from the graph
edges,weights = zip(*nx.get_edge_attributes(G,'weight').items())
print(weights, edges)

# Compute a position of graph elements (needed to visualize weighted graphs)
pos = nx.spring_layout(G)
# draw graph
nx.draw(G, pos = pos, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
# Add weights to graph picture
nx.draw_networkx_edge_labels(G, pos)
```

&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    (0.67, 0.28, 0.31, 0.61, 0.66, 0.13, 0.63) ((0, 2), (0, 4), (0, 5), (1, 2), (2, 3), (2, 5), (4, 5))
    
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {(0, 2): Text(0.05587924164442272, 0.03572413385076614, "{'weight': 0.67}"),
	 (0, 4): Text(-0.09144909073877293, -0.6331454386897136, "{'weight': 0.28}"),
	 (0, 5): Text(-0.18708205101864206, -0.43166771273736326, "{'weight': 0.31}"),
	 (1, 2): Text(0.36606551732176823, 0.4975472153877831, "{'weight': 0.61}"),
	 (2, 3): Text(-0.03165513391993038, 0.6029900698900599, "{'weight': 0.66}"),
	 (2, 5): Text(-0.14019660265009343, -0.12965270150716987, "{'weight': 0.13}"),
	 (4, 5): Text(-0.2875249350332891, -0.7985222740476496, "{'weight': 0.63}")}

&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_47_2.png)


Note that positions of nodes may differ from the unweighted graph, but structure of the graph is the same

<div style="line-height:20%;"> <br> </div>
## 3. Add attributes to a graph, nodes and edges

### Add attributes to a graph


```python
# Create a graph
G = nx.Graph()
# Add 'day' attribute to the graph with "Friday" value
G = nx.Graph(day = "Friday")
G.graph
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {'day': 'Friday'}




```python
# Change an attribute value
G.graph['day'] = "Monday"
G.graph
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {'day': 'Monday'}




```python
# Delete graph attribute
del G.graph['day']
```


```python
G.graph
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {}



### Add attributes to nodes


```python
# Create a graph
G = nx.Graph()
```


```python
# Add an attribute "time" with value, for node 1
G.add_node(1, time='5pm')
```


```python
# Add the attribute "time" with value, for node 3
G.add_nodes_from([3], time='2pm')
```


```python
# Check attributes of 1 node
G.nodes[1]
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {'time': '5pm'}




```python
# Check attributes of 3 node
G.nodes[3]
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {'time': '2pm'}




```python
# Add an attribute "room" with value, for node 1
G.nodes[1]['room'] = 714
G.nodes.data()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeDataView({1: {'time': '5pm', 'room': 714}, 3: {'time': '2pm'}})




```python
# delete particular node attribute
del G.nodes[1]['room']
```


```python
# Print nodes attributes
G.nodes.data()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeDataView({1: {'time': '5pm'}, 3: {'time': '2pm'}})




```python
# Print nodes attributes
for k, v in G.nodes.items():
    print(f'{k:<4} {v}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1    {'time': '5pm'}
    3    {'time': '2pm'}
    


```python
# Delete 'time' attributes from all nodes in a loop
for k, v in G.nodes.items():
    del G.nodes[k]['time']
```


```python
# Print node attributes
for k, v in G.nodes.items():
    print(f'{k:<4} {v}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1    {}
    3    {}
    

### Add attributes to an edges


```python
# Create a graph
G = nx.Graph()
```


```python
# Add weighted edge to graph    
G.add_edge(1, 2, weight=4.7 )

# Compute position of the graph elements
pos = nx.spring_layout(G)
# Draw the graph
nx.draw(G, pos = pos, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
# Add weights to a graph picture
nx.draw_networkx_edge_labels(G, pos)
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {(1, 2): Text(2.220446049250313e-16, 0.0, "{'weight': 4.7}")}




&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_69_1.png)


Weights are one type of attributes. We may create custom attributes.


```python
# Add 2 edges with attribute color to the graph     
G.add_edges_from([(2, 3), (3, 4)], color='red')

# Compute a position of graph elements
pos = nx.spring_layout(G)
# Draw the graph
nx.draw(G, pos = pos, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
# Add attributes to graph picture
nx.draw_networkx_edge_labels(G, pos)
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {(1, 2): Text(-0.6545391148791944, 0.17485675574125337, "{'weight': 4.7}"),
	 (2, 3): Text(-0.07544906355289227, 0.020149585725262716, "{'color': 'red'}"),
	 (3, 4): Text(0.6545391148791944, -0.17485675574125328, "{'color': 'red'}")}




&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_71_1.png)



```python
# Another way to add an attribute
G.add_edges_from([(1, 2, {'color': 'blue'}), (2, 3, {'weight': 8})])
```


```python
# Another way to add an attribute
G.edges[1,2]['color'] = "white"
# Check added properties of edges
G.adj.items()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    ItemsView(AdjacencyView({1: {2: {'weight': 4.7, 'color': 'white'}}, 2: {1: {'weight': 4.7, 'color': 'white'}, 3: {'color': 'red', 'weight': 8}}, 3: {2: {'color': 'red', 'weight': 8}, 4: {'color': 'red'}}, 4: {3: {'color': 'red'}}}))




```python
# Print edges attributes in more readable way 
for k, v, w in G.edges.data():
    print(f'{k:<4} {v}{w}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1    2{'weight': 4.7, 'color': 'white'}
    2    3{'color': 'red', 'weight': 8}
    3    4{'color': 'red'}
    

In the printings above we can see that node 1 has connection with node 2. And this edge has attributes weight and color. Node 2 has 2 connections - with node 1 and node 3.


```python
# Add a weight for an edge 1-2
G[1][2]['weight'] = 4.7
```


```python
# or
G.edges[1, 2]['weight'] = 4.7    
```


```python
# Check attributes on edges
G.edges.data()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeDataView([(1, 2, {'weight': 4.7, 'color': 'white'}), (2, 3, {'color': 'red', 'weight': 8}), (3, 4, {'color': 'red'})])




```python
# Print edges attributes in more readable way 
for k, v, w in G.edges.data():
    print(f'{k:<4} {v}{w}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1    2{'weight': 4.7, 'color': 'white'}
    2    3{'color': 'red', 'weight': 8}
    3    4{'color': 'red'}
    


```python
# Delete edge attribute 
del G[2][3]['color']
```


```python
# Print edges attributes 
for k, v, w in G.edges.data():
    print(f'{k:<4} {v}{w}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1    2{'weight': 4.7, 'color': 'white'}
    2    3{'weight': 8}
    3    4{'color': 'red'}
    


```python
G.edges.data()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeDataView([(1, 2, {'weight': 4.7, 'color': 'white'}), (2, 3, {'weight': 8}), (3, 4, {'color': 'red'})])




```python
# Delete edge attributes "weight"
for n1, n2, d in G.edges(data=True):
    if "weight" in d:
        del d["weight"]
```


```python
# Print edges attributes 
for k, v, w in G.edges.data():
    print(f'{k:<4} {v}{w}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    1    2{'color': 'white'}
    2    3{}
    3    4{'color': 'red'}
    

## 4. Check a graph properties

### Prepare a graph


```python
# Create a chain graph
G = nx.path_graph(5)
# Draw the graph
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_87_0.png)


### Check properties


```python
# Check number of nodes
G.number_of_nodes()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    5




```python
# Check number of edges
G.number_of_edges()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    4



### Nodes View


```python
# All nodes overview
G.nodes()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeView((0, 1, 2, 3, 4))




```python
# or
list(G.nodes)
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    [0, 1, 2, 3, 4]




```python
# or
G.nodes.items()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    ItemsView(NodeView((0, 1, 2, 3, 4)))




```python
# or
G.nodes.data()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeDataView({0: {}, 1: {}, 2: {}, 3: {}, 4: {}})




```python
# or
G.nodes.data('span')
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    NodeDataView({0: None, 1: None, 2: None, 3: None, 4: None}, data='span')



### Edges View


```python
# All edges overview
G.edges
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeView([(0, 1), (1, 2), (2, 3), (3, 4)])




```python
# or
list(G.edges)
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    [(0, 1), (1, 2), (2, 3), (3, 4)]




```python
# or
G.edges.items()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    ItemsView(EdgeView([(0, 1), (1, 2), (2, 3), (3, 4)]))




```python
# or (weights visible)
G.edges.data()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeDataView([(0, 1, {}), (1, 2, {}), (2, 3, {}), (3, 4, {})])




```python
# or (weights visible)
G.edges.data('span')
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeDataView([(0, 1, None), (1, 2, None), (2, 3, None), (3, 4, None)])




```python
# or (for an iterable container of nodes) - all edges associated with this 
#                                                       subset of nodes
G.edges([2, 'm'])
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    EdgeDataView([(2, 1), (2, 3)])



### Node degree View


```python
# Check degree of particular nodes
G.degree
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    DegreeView({0: 1, 1: 2, 2: 2, 3: 2, 4: 1})




```python
# list degrees in column (":<4" makes 4 spaces between numbers)
for v, d in G.degree():
    print(f'{v:<4} {d}')
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    0    1
    1    2
    2    2
    3    2
    4    1


```python
# or (for the one particular node)
G.degree[1]
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    2




```python
# or (for the iterable container of nodes)
G.degree([2, 3])
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    DegreeView({2: 2, 3: 2})



### Adjacency view


```python
# Check an adjacency matrix - neighbourhood between nodes
G.adj
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    AdjacencyView({0: {1: {}}, 1: {0: {}, 2: {}}, 2: {1: {}, 3: {}}, 3: {2: {}, 4: {}}, 4: {3: {}}})




```python
# Print a dictionary in a dictionary in more readable way 
from pprint import pprint
pprint(dict(G.adj))
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {0: AtlasView({1: {}}),
	 1: AtlasView({0: {}, 2: {}}),
	 2: AtlasView({1: {}, 3: {}}),
	 3: AtlasView({2: {}, 4: {}}),
	 4: AtlasView({3: {}})}
    


```python
# Check neighbors of particular node
list(G.adj[3])

```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    [2, 4]




```python
# or
G[3]
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    AtlasView({2: {}, 4: {}})




```python
# or
list(G.neighbors(3))
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    [2, 4]



## 5. Accessing edges and neighbors 


```python
# Create a graph
G = nx.Graph()
G.add_weighted_edges_from([(1, 2, 0.125), (1, 3, 0.75), (2, 4, 1.2), 
                           (3, 4, 0.375)])

# Compute position of graph elements
pos = nx.spring_layout(G)
# Draw the graph
nx.draw(G, pos = pos, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
# Add weights to a graph picture
nx.draw_networkx_edge_labels(G, pos)

```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    {(1, 2): Text(-0.11306457583748142, 0.3689242447964494, "{'weight': 0.125}"),
	 (1, 3): Text(-0.7453632597697203, -0.1911266592810591, "{'weight': 0.75}"),
	 (2, 4): Text(0.74536325976972, 0.19112665928105907, "{'weight': 1.2}"),
	 (3, 4): Text(0.11306457583748117, -0.3689242447964495, "{'weight': 0.375}")}




&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_116_1.png)


### 1st method for edges + weights extraction


```python
# Get 'weight' attributes
nx.get_edge_attributes(G,'weight').items()
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    dict_items([((1, 2), 0.125), ((1, 3), 0.75), ((2, 4), 1.2), ((3, 4), 0.375)])




```python
# Build up variables
edges,weights = zip(*nx.get_edge_attributes(G,'weight').items())
```


```python
# Edges overview
edges # tuple of tuples
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    ((1, 2), (1, 3), (2, 4), (3, 4))




```python
# Weights overview
weights # tuple
```


&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    (0.125, 0.75, 1.2, 0.375)



### 2nd method for edges + weights extraction


```python
for (u, v, wt) in G.edges.data('weight'):
    print('(%d, %d, %.3f)' % (u, v, wt))
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    (1, 2, 0.125)
    (1, 3, 0.750)
    (2, 4, 1.200)
    (3, 4, 0.375)
    

### 2nd method for edges + weights extraction with condition


```python
for (u, v, wt) in G.edges.data('weight'):
    if wt < 0.5: print('(%d, %d, %.3f)' % (u, v, wt))
```
&nbsp; &nbsp; <span style="color:#808080; font-family:Calibri; font-size: 85%">Output: </span>

    (1, 2, 0.125)
    (3, 4, 0.375)
    

## 6. Draw graphs

### Figure size changing


```python
# Import libraries
import networkx as nx
import matplotlib.pyplot as plt

# Graph creation
G = nx.erdos_renyi_graph(20, 0.30)

# Draw a graph
plt.figure(1) # default figure size 
plt.title("Graph") # Add title
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)

# Draw a big graph
plt.figure(2,figsize=(10,10)) # Custom figure size
plt.title("Big Graph") # Add title
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_128_0.png)



&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_128_1.png)


### Draw 2 graphs on 1 chart


```python
# Create graph
G = nx.erdos_renyi_graph(20, 0.20)

# Draw graphs with "nx.draw" and subplots 
# Nr 121, 122 are for 2 graphs on 1 chartplt.subplot(121)

# Draw graph 1
plt.subplot(121)
plt.title("Graph 1")
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)

# Draw graph 2
plt.subplot(122)
plt.title("Graph 2")
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_130_0.png)


### Draw 4 graphs on 1 chart with kwargs

In the situation where we have to define arguments for many subplots we may use "kwargs" (keyworded arguments) feature. 
It allows us to define a dictionary contains keys with values, which become arguments of a function. Clear explanation 
of this feature you may find [there](https://pythontips.com/2013/08/04/args-and-kwargs-in-python-explained/).


```python
# Create graph
G = nx.erdos_renyi_graph(20, 0.30)

# Define **kwargs - dictionary with arguments for a function
kwargs = {
    'node_color': 'pink',
    'node_size': 200,
    'width': 2, # 
    }

# Draw graphs with options
# Nr 221, 222, 223, 224 are for 4 graphs on 1 chart
plt.subplot(221)
nx.draw(G, with_labels=True, font_weight='bold', **kwargs)
plt.subplot(222)
nx.draw(G, with_labels=True, font_weight='bold', **kwargs)
plt.subplot(223)
nx.draw(G, with_labels=True, **kwargs)
plt.subplot(224)
nx.draw(G, with_labels=True, **kwargs)

```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_133_0.png)


### Draw a graph with more arguments specified


```python
plt.title("Graph")
nx.draw(G, # graph object 
        with_labels=True, # label of node (numbers of nodes in this case)
        node_size=500, 
        node_color="#ffcc99", 
        node_shape="o", 
        alpha=0.7, # node transparency
        linewidths=1, # linewidth of symbol borders (nodes)
        width=1, # linewidth of edges
        edge_color="purple", 
        style="dashed", # style of edges
        font_size=12, 
        fontcolor="k", 
        font_family="Consolas")
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_135_0.png)


 * with_labels (bool, optional (default=True)) – Set to True to draw labels 
    on the nodes. <br>
 * node_size (scalar or array, optional (default=300)) – Size of nodes. 
    If an array is specified it must be the same length as nodelist <br>
 * node_color (color string, or array of floats, (default=’#1f78b4’)) 
    – Node color. Can be a single color format string, or a sequence of colors 
   with the same length as nodelist. If numeric values are specified they will 
    be mapped to colors using the cmap and vmin,vmax parameters. See 
    matplotlib.scatter for more details. <br>
 * node_shape (string, optional (default=’o’)) – The shape of the node. 
    Specification is as matplotlib.scatter marker, one of ‘so^>v<dph8’. <br>
 * alpha (float, optional (default=1.0)) – The node and edge transparency <br>
 * linewidths ([None | scalar | sequence]) – Line width of symbol border 
    (default =1.0) <br>
 * width (float, optional (default=1.0)) – Line width of edges <br>
 * edge_color (color string, or array of floats (default=’r’)) – Edge color. 
     Can be a single color format string, or a sequence of colors with 
     the same length as edgelist. If numeric values are specified they will be 
     mapped to colors using the edge_cmap and edge_vmin,edge_vmax parameters. <br>
 * style (string, optional (default=’solid’)) – Edge line style 
     (solid|dashed|dotted,dashdot) <br>
 * font_size (int, optional (default=12)) – Font size for text labels <br>
 * font_color (string, optional (default=’k’ black)) – Font color string <br>
 * font_family (string, optional (default=’sans-serif’)) – Font family <br>
 
 Check more arguments in [NetworkX documentation](https://networkx.github.io/documentation/stable/reference/generated/networkx.drawing.nx_pylab.draw_networkx.html#networkx.drawing.nx_pylab.draw_networkx).
 

### Add random weights to a graph and draw as colored edges

Very interesting way for visualize weighted graph is to color its edges depending on weights. 


```python
# Generate Erdős-Rényi graph
G = nx.gnp_random_graph(10,0.3)
nx.draw(G, with_labels=True, node_color='#b2b2ff', node_size=700, 
	font_size=14)
```


&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_139_0.png)



```python
# Add random weights 
for u,v,d in G.edges(data=True):
    d['weight'] = random.random() # there we may set distribution
    # in this loop we iterate over a tuples in a list
    #                    u - is actually 1st node of an edge
    #                    v - is second node of an edge
    #                    d - is dict with weight of edge
    
# Extract tuples of adges, and weights from the graph
edges,weights = zip(*nx.get_edge_attributes(G,'weight').items())

# Compute optimized nodes positions
pos = nx.spring_layout(G)
# Draw graph
nx.draw(G, pos, edgelist=edges, 
        edge_color=weights, width=3.0, edge_cmap=plt.cm.Blues, 
        edge_vmin=-0.4, edge_vmax=1, with_labels=True,
		node_color='#b2b2ff', node_size=700, font_size=14)
```

&nbsp; &nbsp; <span style="color:blue; font-family:Calibri; font-size: 85%; font-weight: Bold">Output: </span>
![png]({{site.baseurl}}/assets/social-network-analysis-introduction-to-networkx/output_140_1.png)


Note that positions of nodes may differ from the unweighted graph, but structure of the graph is the same.

<div style="line-height:20%;"> <br> </div>

## 7. Graphs I/O in GML format 

<div style="line-height:100%;"> <br> </div>


* write <abbr title="Graph Modeling Language">GML</abbr> file `nx.write_gml(graph, "path.to.file")`

* read GML file `mygraph = nx.read_gml("path.to.file")`




<br>
### Annotation
<div class="message">
Instructions are dedicated for Windows 10 <br>
Anaconda release: 2019.03 <br>
Python version: 3.7.3 <br>
networkx==2.3 
</div>

