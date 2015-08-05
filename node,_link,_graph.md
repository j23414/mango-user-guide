# Graph Data

Defining graphs in GEL requires first defining a **nodetype** and **linktype**. Enter the following GEL commands into the GEL console (bottom right) to define different nodetypes.

```
node(string name) nt;            // most basic nodetype
node(string name, int count) nt; // also contains node attribute count
node(string id, int count=3) nt; // contains a default value for count
```

In the same way, you can define a **linktype** with its associated link attributes.

```
link[] lt;
link[float weight, string type="undirected"] lt;
link<float weight, string type="directed"> lt;
```

There are some system-defined attributes appended to nodes and links. The **desc** command will display the contents of a node and link type. You can also expand the nt and lt in the **Data** panel

```
desc nt;
desc lt;
```

**Visual attributes** of nodes and links are denoted by an underscore prefix. These represent 3D coordinates (_x,_y,_z), color(_r,_g,_b), text and other visual attributes. The user should not define visual attributes as they are already included in the type definition.

```
node(string name,float _x) nt; //Will throw a syntax error
```

Defining a Graph in GEL with the following commands:

```
node(string name) nt;
link[float weight,int count]lt;
graph(nt,lt)simple={("node1")[0.1,1]("node2")[0.2,2]("node3"),
node1[0.3,3]node3};
desc simple; //show node and link types
dump simple; //show graph contents
```

Importing a Graph from a file with the following commands:

```
node(stringname)in_nt;
link[floatweight]in_lt;
graph(in_nt,in_lt)the40=import("the40.csv");
```

Creating a Random Graph with 64 nodes.

```
graph(nt,lt) ran64=random(64);    //50% connectivity, default
graph(nt,lt) com64=random(64,100); //complete graph
```

Click on the ran64 and the40. You'll notice that both of them seem to only show one node. However, since by default, the position of all nodes are _x=0, _y=0, and _z=0, you will only see one node. Click on simple and type the following:

```
layout("cube");
dump simple;
```

Notice how the xyz coordinates are now different for each node. Try the following commands and watch the effect on the simple visualization:

```
foreach node in simple set_x=rand(-3,3),_y=rand(-3,3),_z=rand(-3,3);
foreach node in simple set_r=rand(),_g=rand(),_b=rand();
foreach node in simple set_r=rand(),_g=rand(),_b=rand();
foreach link in simple set_r=rand(),_g=rand(),_b=rand();
```

Export graphs
```
export("simplenew.tsv","tsv",simple); //saves simple as a tab delimited file
save "state.txt"; //saves all graphs as GEL commands
```

Reload graphs

```
clear;           //clears all graph data
run "state.txt"; //reload saved graph data
```

You can access specific attributes in a graph using the following:
```
node(string name) nt;
link[float weight] lt;
graph(nt,lt) g = {("node1")[1.0]("node2")};

g.node."node1"._x=10;
g.link."node1":"node2".weight=10;
```



