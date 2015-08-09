#GEL Reference

**center**

Resets x,y,z values so the center of the graph is within the viewing window.
Center the given graph. If the name of one of the nodes is supplied, it will center the visualization on that node.

```
center(graph); 
center(graph,"jack");
```

**clear**

clear all data and graph objects from Mango

```
clear;
```

**clearconsole**

clear the console panel. 

```
clearconsole();
```

**delete**

delete variables, graphs, node or link types

```
delete var1,graph2,node3,link4;
```

**desc**

Describes the named data objects. Prints out data type as well as data value.
If no data objects are given, describes all data objects in memory.

```
desc var1, graph2, node3, link4;
```

**exec**

Executes a given Gel script. No returning to the code.

```
exec "command.txt";
```

**exp**

Exponential function. Raise natural e to the given value power.

```
double v = exp(3); // e^3
```

**export**

export(string filename, string format, graph one, graph two, …)
filename: name of file to save the exported graph(s)

format: either “csv” or “tsv” for Excel or “dot” for Graphviz
one, two, …: name of selected graphs to export; all graphs will be exported if none is specified.

Note: do not use the import/export functions to save your data. Instead, use the save and run/exec commands to save your data in the native Gel language format.

```
node(string name) nt;
link[] lt;
graph(nt,lt) ran=random(10);
export(“ran.csv”, “csv”, ran);
```

**foreach**

foreach scans through all nodes and all links in a graph and allow certain attributes to be set accordingly. The where clause is optional but if it is specified, only nodes or links satisfying the condition will be modified.

```
foreach node in graph_abc where count>2 set count=2;
foreach link in graph_abc set weight=(in.count+out.count)/2.0;
```

**graph**

Compound data type declaration. All declarations can take on initialization values
or (in the case of node or link types) default attribute values.

```
graph(node_type, directed) g1; 
// declared a graph with node_type and directed link type

graph(node_type, undirected) g2 = { ("node1", 1)[12.0f,2.0]("node2",2) };
```

**getwd**

returns a string of the current working directory

```
string s = getwd();
print getwd();
```

**help**

display all help topics by default. look up a particular function

```
help;                // display all help topics
help verbose;  // display verb description
help rand;       // display rand function description
```

**import**

graph = import(string filename, string delimiter)

filename: name of graph data file to be imported
delimiter: character(s) that separate fields in a line

Note: do not use the import/export functions to save your data. Instead, use the save and run/exec commands to save your data in the native Gel language format.

import a graph from a delimited file into Mango.

```
node(string name) nt;
link[]lt;
graph(nt,lt) net = import("net.csv",",");
graph(nt,lt) net = import("net.tsv", "\t");
```

**int**

integers, one of the four primitive data types

```
int i = 0;
i=40;
```

**layout**

preset graph layouts, applied to the currently viewed and selected graph in the canvas area.

layout(type)
type: either "random", "cube", or "circle"

```
layout("circle");
layout("random");
layout("cube");
```

**link**

compound data type declaration, necessary for defining the graph type

```
link [float weight, double value, ...] undirected; // defined an undirected link type
link <float weight, double value, ...> directed; // defined a directed link type

link[] lt;
link[weight] lt;
link<float transferspeed> lt;
```

**list**

list the named data objects. If no data objects are given, list all data objects in memory.

```
list var1, graph2, node3, link4;
```

**log**

natural log of a value

```
double d = 315.3;
double logd = log(d);
```

**node**

compound data type declaration, necessary for defining the graph type. 

node(string name, int count, ...) nodetype;

```
node(string name) nt;
node(string id) nt;
node(string id, int age) nt;
```
 
**print**

only scalar expressions can be given to the print command

```
print "The number of nodes in graph A is ", nodes(A);
print "Sum of nodes in graph A and B is ", nodes(A)+nodes(B);
```

**rand**

generates a random number between a min and max value. By default, min value equals 0.0 and max value is 1.0.

```
double min = -5;
double max = 7;
double v = rand(min,max);
```

**random**

graph = random(int nodes, double percent, int loop, int seed)

nodes: number of nodes in the random graph
percent: percent of connected links among nodes
loop: 0 no loop back to the same node; 1 otherwise
seed: seed to random number generator; 0 automatic

```
node(string name) nt;
link[] lt;
graph(nt,lt) ran = random(10);  // 10 nodes with 50% connectivity
ran = random(10,0.25);             // 10 nodes with 25% connectivity  
```

**run**

run the gel script file and then the next command (if any)

```
run "command.txt";
```

**save**

save the named data objects to be loaded back into Mango later. If no data objects are given, all data objects in memory are saved to the given filename. Saved file is a Gel script that can be loaded back using the run or exec commands.

```
save "data.txt", var1, graph2,node3, link4;
```

**select**

Either nodes or links can be the selection target. In the where clause a boolean condition can be specified for the selection. Special in and out value are defined: in node selection, in and out denote the in-degree and out-degree of each node being considered for selection. In link selection in and out denote the nodes connected by each link under consideration, whose attributes can be accessed as in.count or out.name

```
subgraph = select node from graph_abc where count>10 && in>2;
subgraph = select link from graph_abc where weight>5.0 && in.count>2;
```

**setwd**

pops a window to set the working directory, can also return the string of the working directory

```
setwd();
string wk = setwd();
print setwd();
```

**string**

string and characters, one of the four primitive data types

```
string s = "hello world";
string c = "c";
```

**sin**

trigonometric sin function given the angle in radians

```
double s = sin(3.14);
```

**tan**

trigonometric tan function given the angle in radians

```
double v = tan(315.5);
```

**verb**

set Gel verbose level 
* n=0 Gel reports critical errors that stops it 
* n=1 Gel reports data redefinitions or deletions 
* n=2 Gel echo typed commands (default level) 
* n=3 Gel echos scalar computation results 
* n=4 Gel echos resulted graph node and link types 
* n=5 Gel echos resulted graph complete information

```
verb 3; // set verbose level to 3
verb;  //check current verbose level
```

