#GEL Reference

Some commands require parenthesis and some commands do not. This is because some of the commands are statement commands while others are functions.

**abs**

Returns the absolute value of numeric data. 

```
print abs(-2.34); // returns 2.34
print abs(3);     // returns 3
```

**acos**

Converts cosine value to angle value in radians.

```
print acos(0.5); // returns 1.047198
```

**asin**

Converts sine value to angle value in radians.

```
print sin(1);    // returns 0.841471
```

**atan**

Converts tangent value to angle value in radians.

```
print tan(0.3);    // returns 0.309336
```

**ceil**

Rounds a given value up to its ceiling integer. 

```
print ceil(3.1);    // returns 4
print ceil(2);      // returns 2
print ceil(1.5);    // returns 2
```

**center**

Centers a given graph on the xyz coordinates (0,0,0). If a node name is also given, the entire graph will be shifed so that the given node's xyz coordinates is at (0,0,0).

```
center(graph); 
center(graph,"jack"); // we focus on "jack" node
```

**clear**

Clears/removes all data and graph objects from Mango.

```
clear;
```

**clearconsole**

Clears any text from the console panel. 

```
clearconsole();
```

**clearmessage**

Clears any text from the message panel.

```
clearmessage();
```

**cos**

Converts the angle in radians to the cosine value.

```
print cos(3.14/4); // returns 0.707388
```

**delete**

Deletes variables, graphs, node or link types. See **clear** to delete all variables.

```
delete var1;
delete var1, graph2, node3, link4;
```

**desc**

Describes the named data objects by printing out data type as well as data value in the messages pane.
If no data objects are given, describes all data objects in memory.

```
desc var1;
desc var1, graph2, node3, link4;
desc;   // describes all data objects
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

**floor**

Rounds a number down to the nearest integer. 

```
print floor(3.9);   // returns 3
print floor(2);     // returns 2
print floor(1.1);   // returns 1
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

preset graph layouts, applied to the given graph **g**.

layout(type)
type: either "random", "cube", or "circle"

```
layout(g,"circle");
layout(g,"random");
layout(g,"cube");
```

**len**

Returns the number of characters in a string, length of the string.

```
print len("Hello World!");   // returns 12
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

**map**

Renames node ids based on a digraph. Multiple nodes can be mapped to the same id, combiing nodes.

```
help map;
graph = map(graph g, map_info, int keep, int loop)
  g: graph whose nodes are to be mapped, or renamed
  map_info: mapping information. Can be a graph or an attribute name
    If a graph, it should be directed, and its links define the map
    If an attribute name, it should be defined in nodes on graph a
  keep: 0 will discard unmappped nodes or nodes whose map attribute
    contains a null string; 1 will collect them unchanged to output
  loop: 0 will discard self-pointing loops in output; 1 otherwise
```

**match**

Compares sequence (dna/protein/other letter) data in two graphs. Creates a new graph depending on the minimal sequence match length. Can also determine DNA reverse complement matches.

```
help match;
graph = match(graph a, graph b, string a_attr, string b_attr, int min_match, int revcomp, int in_graph)
  a, b: graphs whose nodes are compared; in-graph comparision if a==b
  a_attr: the node attribe name in a that contains sequence data
  b_attr: the node attribe name in b that contains sequence data
  min_match: minimal match length to produce a match link in output
  revcomp: for DNA, 1 finds revese-complement matches; 0 otherwise
  in_graph: 1 or when a==b allows in-graph matches; 0 otherwise
```

**node**

compound data type declaration, necessary for defining the graph type. 

node(string name, int count, ...) nodetype;

```
node(string name) nt;
node(string id) nt;
node(string id, int age) nt;
```

**pause**

Pauses a few miliseconds.Useful when used inside animation loops. If delay has value of 0, pause for user input.

```
pause(1000);   // 1000 milisecond pause
pause(0);      // pause for user
```

**pow**

Raises a number to a power.

```
print pow(4,2);  // returns 16, or 4^2 
```
 
**print**

only scalar expressions can be given to the print command

```
print "The number of nodes in graph A is ", nodes(A);
print "Sum of nodes in graph A and B is ", nodes(A)+nodes(B);
```

**r_mat**

```
help r_mat;
graph = r_mat(int nodes, int degree, int loop, int seed, float a, float b, float c, float d)
  nodes: number of nodes in the random graph
  degree: average connectivity degree of nodes
  loop: 0 no loop back to the same node; 1 otherwise
  seed: seed to random number generator; 0 automatic
  a, b, c, d: probabilities of falling into each quadrant
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

**substr**

for substring function

```
string s = "hello world";
s = substr(s,0,5); /* s="hello"*/ 
```

**tan**

trigonometric tan function given the angle in radians

```
double v = tan(315.5);
```

**time**

The time out value when waiting for a loop to finish.

```
time;      /* check what the current time out value is */
time 2000; /* set to 2000 ms */
```

**tocamel**

Converts strings to camel case.
```
string s = tocamel("hello world"); /* s="Hello World" */
```

**tolower**

Converts strings to lower case.
```
string s = tolower("Hello World"); /* s = "hello world" */
```

**toupper**

Converts strings to upper case.

```
string s = tolower("Hello World"); /* s = "HELLO WORLD" */
```

**trim**

Drops spaces at the beginning and end of the string.

```
string s = trim(" hello world "); /* s ="hello world" */

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

**while**

Gel has looping constructs

```
int i=10;
while(i<10) i++;
```
