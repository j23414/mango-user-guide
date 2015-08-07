Basics Walk-Through Tutorial
================
This tutorial will walk you through creating a gel file and some basic network files from scratch. All you will need is a downloaded version of Mango.

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

Network files can be imported as csv or other delimited text files. These can be exported from excel. The network files usually include a list of nodes, a hypen on it's own line, and a list of edges. Copy and paste the following text blocks into your net.txt and gel.txt files.
**In net.txt**
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

