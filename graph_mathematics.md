# Graph Mathematics

One of the strengths of Gel is its set of graph mathematics. Each graph is treated as a unit that can be added, subtracted, or otherwise combined with each other. Gel takes care of attribute conflict and merging. 

For a more intuitive introduction, take a look at the visual summary of graph mathematics section below. To understand graph mathematics from a tutorial, see section two. For the rigorous theoreticians among you, see section three.

**Topics**
* A visual summary of graph mathematics
* A gel tutorial demonstrating graph mathematics
* A theoretical explaination of graph mathematics

##A visual summary of graph mathematics

The following figure provides a visual of graph mathematics on two starting graphs: $$G_A$$ and $$G_B$$. New nodes and links from the right operand are shown in bold. Graph operations have dotted and non-dotted versions depending on node-centric or link-centric operations.

![](imgs/img20.png)

## A Gel tutorial demonstrating graph mathematics

What might you want to do with two graphs? You may want to combine them together. 

```
graph(nt,lt) A;
graph(nt,lt) B;

graph(nt,lt) C = A-A;
```
What do you expect to happen? Try the code. Your results should be similar to those below.

Notice how *A-A* resulted in graph *A* with no links. That is because '-' and '+' results in subtraction and addition of links. To subtract and add nodes put a dot '.' in front of the operators. 

```
graph(nt,lt) C = A.-A;
```

This results in the empty graph.


## A theoretical explaination of graph mathematics

A graph is defined as a set of nodes ($$V$$) and links ($$E$$) where a node represents an entity and a link represents a relationship between a pair of entities.

$$
G=\{V,E\} \quad \text{where} \quad V=\{v_1,v_2,v_3,...,v_n\} \quad \text{and} \quad \quad E\subset \{(v_i,v_j)|v_i,v_j \in V\}
$$

In practice, graphs have additional annotations called **attributes**. Currently, Gel provides four basic data primitives string, int, float and double as well as aggregate data types node ($$V_{attr}$$), link ($$E_{attr}$$) and graph.

$$
V_{attr}=\{a_1,a_2,a_3,...,a_{m1}|type(a_i)\in \{int, float, double, string\}\}
$$

$$
E_{attr}=\{a_1,a_2,a_3,...,a_{m2}|type(a_i)\in \{int, float, double, string\}\}
$$

Graph mathematics allow graph level operations. When two graphs are combined, node and link attributes must be combined in an intuitive manner. What happens when node and link attribute conflict occurs. The graph on the left (left operand) values take precedence. The exception to this is if the left operand has default values. Then the new data from the right will be incorporated into the new resulting graph.

Suppose you have two graphs $$G_A$$ and $$G_B$$:

$$
G_A=\{V_A,E_A\} \quad \text{and} \quad G_B=\{V_B,E_B\}
$$

Part of the confusion of combining and subsetting multiple graphs is what to do with the nodes and links. Gel provides dotted and non-dotted mathematics to specify node-centric or link-centric operations.

In order to merge links and nodes in two graphs use the dotted addition operator.

$$
G_A\ .+G_B=\{V_A \cup V_B, E_A \cup V_B\}
$$

However, if you are only concerned with nodes in $$G_A$$ such as a set of important genes or locations and only want to overlay new links from $$G_B$$, use the non-dotted addition operator.

$$
G_A +G_B=\{V_A, E_A \cup \{(v_i,v_j)|v_i,v_j \in V_A, (v_i,v_j) \in E_B\}\}
$$

In a similar fashion, the subtraction operator has a dotted and non-dottted version.

$$
G_A\ .-G_B=\{V_A \setminus V_B, E_A \setminus V_B\}
$$

$$
G_A -G_B=\{V_A, E_A \setminus V_B\}
$$

