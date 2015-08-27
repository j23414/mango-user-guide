# GEL Data Structures

GEL provides four basic data primitives *string*, *int*, *float*, and *double* as well as aggregate data types *node*, *link* and *graph*. Understanding these basic data types and their behaviors has helped standardize the way we work with heterogeneous graphs.

Graphs
----
Most of the time, when we are thinking about "graphs" or "networks" we are thinking about a set of nodes and edges. A set of people and their friend network. Or a set of towns and the interconnected highway system. Therefore, when designing a graph data type, we must have a way to identify nodes and links.  Nodes can be identified by unique names. Gel uses string ids, unlike other programs which uses a unique number id. This reduces the mapping from name to number that is required when comparing nodes in multiple graphs. 

Since links connect pairs of nodes, links are identified by the pair of node names. 

The major strength of Mango is that it can also deal with graph attributes. Nodes and links may have a set of attributes associated with them. For example, in a social network, an individual named "Bob" may have an age, birth date, home address, height and weight. 

![](img21.png)




