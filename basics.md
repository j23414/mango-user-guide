Walking Through the Mango Grove
================
This tutorial will walk you through creating a gel file and some basic network files from scratch. All you need is a running version of Mango since all code and text-based data will be in this tutorial.

Create a Gel File and the 4 Data Primitives
----
Open **Mango** and go to **File/New** or hit **Ctrl+N** to create a gel script. Create a new folder on your Desktop called **Basic** and name the new gel script "gel.txt". 

![](img03.png)

A new file should show up in the editor pane with a tab labeled "gel.txt". Type the following four lines into the gel.txt. 

```
int i=1;
float f=2.2;
double d=3.3;
string s="Hello World";
```

These are the four basic data types in Gel. 

When you start editing gel.txt, an asterisk symbol appears next the to the name in the tab. This means you have unsaved changes. Hit **Ctrl+S** to save file and notice how the asterisk goes away. 

![](img04.png)

Click inside of the gel.txt and place the cursor on the first line. Then press **Ctrl+Enter** and notice how it shows up under **Values** in the **Data** pane, listing data type and contents. 

![](img05.png)

You can either continue to press **Ctrl+Enter** to load the other data types or you can type the following command into the **Console** to run the entire file.

```
run "gel.txt";
```
![](img06.png)

Create a Network File and Load it
----
Go to **File/New** and create "net.txt". This file will store a small network. 

![](img07.png)

Network files can be imported as csv or other delimited text files. These can be exported from excel. The network files usually include a list of nodes, a hypen on it's own line, and a list of edges. Copy and paste the following text blocks into your net.txt and gel.txt files. In
**net.txt**
```
a
b
c
d
-
a,b
a,c
c,d
a,d
```
![](img08.png)

```
node(string name) nt;
link[] lt;
graph(nt,lt) net=import("net.txt");
```

Run the gel script and the object "net" shows up under Graphs in the Data panel. The "4|4" means net has 4 nodes and 4 links. Two other objects are created: nt, and lt. Click and expand the two.

![](img11.png)

Notice **nt** has string name with a bunch of other things listed with an underscore prefix. The prefixed attributes are called **system-defined attributes**. These are usually associated with the 3D layout or visualization of the network. Expand **lt** and take a look at the attributes. 

Double click "net" and a new tab shows up in the Graph Canvases area.

![](img09.png)

You only see one node because by default, all xyz coordinates are set to zero. Before we change them, run the following command five times:

```
print rand();
```
This will give a random float from 0 to 1. You can give two arguments for min and max values.

```
print rand(-5,5);
```

Type and run the following command.

```
layout(net,"circle");
foreach node in net set _r=0, _g=0.9, _b=1;
foreach link in net set _r=0, _g=0.9, _b=1;
foreach node in net set _text=name;
```

![](img10.png)

The **layout** function has a few preset xyz coordinate calculations for each of the nodes. Type "help layout;" to find out more. 