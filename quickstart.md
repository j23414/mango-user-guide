## Quick Start Demo

You will need a running version of Mango and the **DemoFiles** folder that came with Mango installation. This section demonstrates loading networks, merging some those networks through graph mathematics, and exporting the new graphs. The purpose of this section is to give a quick example. For a more complete walk-through with explanations see Slow Start. 

**Outline** 

* Load 4 graphs
* 3D interactive visualization
* Merge graphs
* Export/Save resulting merged graphs

### Load 4 graphs

Open **Mango** and you should be presented with the following screen. The window is divided into four sections. 

* **Data**: displays a list of all data objects in Mango 
* **Canvas**: displays the graph visualizations
* **Editor**: area to edit gel scripts and run them line by line
* **Console**: accepts gel commands and runs them in real time

![](imgs/sum01.png)

Go to **File/Open** and open the "gel\_sum.txt" file inside of the **DemoFiles/sum\_demo** folder that came with Mango installation.

![](imgs/sum02.png)

![](imgs/sum03.png)

"gel\_sum.txt" contains GEL commands. **GEL** stands for **Graph Exploration Language**. GEL allows reproducible multi-graph analysis. It's a flexible powerful language that will continue to be developed. Functions are designed to address graph analysis.

The script should be loaded into the **Editor** panel. Since this is a quick start, we are going to avoid explaining the meaning of each line. Instead we will show you how to run commands line by line.

Click on the first line in "gel\_sum.txt" to place the cursor. If you are on Windows or Linux, press **Ctrl+Enter**. If you are on Mac, press **Cmd+Return**. Press this key combination multiple times. Each time, Mango will execute the line. 

Repeat this until all four graphs have been loaded into Mango or when you see a comment that says "PAUSE HERE FOR QUICK START TUTORIAL". Loaded graphs will be listed in the **Data** panel. 

```
/* define node and link type */
node(string name) nt;
link[int n1id, int n2id, string n1ex, string n2ex, float neighborhood, float fusion, float cooccurence, float homology, float coexpression, float experimental, float knowledge, float textmining, float combined_score] lt;

/* import 4 graph files */
graph(nt,lt) aldo = import("aldo.csv");
graph(nt,lt) cpn = import("cpn.csv");
graph(nt,lt) frh = import("frh.csv");
graph(nt,lt) hif = import("hif.csv");

/* PAUSE HERE FOR QUICK START TUTORIAL */
```

In the **Data** panel (left), four graph objects are listed inside **Graph**. 

Double click on their names and visualizations of the selected graphs will appear in the Graph Canvas (right center) on separate tabs. Tabs are labeled with the graph names, you can drag and rearrange the tabs or show multiple graphs at once.

![](imgs/sum04.png)

### 3D interactive visualization

Execute the following layout commands using **Ctrl-Enter** (Windows/Linux)or **Cmd-Return** (Mac). 

```
/* layout the four graph */
foreach node in aldo set _x=0,_y=rand(-5,5),_z=rand(-5,5);
foreach node in frh set _x=2,_y=rand(-5,5),_z=rand(-5,5);
foreach node in hif set _x=-2,_y=rand(-5,5),_z=rand(-5,5);
foreach node in cpn set _x=-4,_y=rand(-5,5),_z=rand(-5,5);

/* color nodes and links in each graph */
foreach node in aldo set _r=rand(0.5,1),_g=0,_b=0;
foreach link in aldo set _r=rand(0.5,1),_g=0,_b=0;
foreach node in cpn set _r=rand(0.5,1),_g=rand(0.5,1),_b=rand(0.5,1);
foreach link in cpn set _r=rand(0.5,1),_g=rand(0.5,1),_b=rand(0.5,1);
foreach node in frh set _r=0,_g=rand(0.5,1),_b=0;
foreach link in frh set _r=0,_g=rand(0.5,1),_b=0;
foreach node in hif set _r=0,_g=0,_b=rand(0.5,1);
foreach link in hif set _r=0,_g=0,_b=rand(0.5,1);
```

![](imgs/sum05.png)

The **Graph Canvas** (right center) area responds to mouse and keyboard events. **Left click and drag** across the graph. This will rotate the graph visualization. 

Use the **Roller Ball** on your mouse (or two finger swipe on a trackpad) to zoom in and out of the graph. 

Making sure one of the graphs is selected (the tab label will be bolded) use the **arrow keys** on your keyboard to move the graph left, right, up and down. 

Next, **Right click** on one of the displayed graphs. The graph should start to move where connected nodes moving closer together and disconnected nodes moving farther apart. This is the **force-directed layout** algorithm proposed by Eades. Right click again to stop the animating layout.

To explore some other graph layouts, close all tabs except graph **cpn** and type the following GEL commands into the **Console** (bottom right). Capitalization matters so "layout(cpn, "Circle");" will not work. Try rotating, zooming, and running the force-directed layout after each command.

```
layout(cpn, "circle");
layout(cpn, "cube");
layout(cpn, "random");
```

![](imgs/sum06.png)![](imgs/sum07.png)

Run the following command:

```
layout(cpn, "cube");
```
![](imgs/img26.png)

Right click to start the force-directed layout. Notice that the background will dim. Right click again to stop the force-directed layout and the background will revert to normal.

![](imgs/sum08.png)

Turn on node labels by typing the following:

```
foreach node in cpn set _text=name; /* turns on labels */
foreach node in cpn set _text="";   /* turns off labels */
```

![](imgs/sum09.png)

### Merge graphs

Rerun the layout section in "gel_sum.txt".

```
/* layout the four graph */
foreach node in aldo set _x=0,_y=rand(-5,5),_z=rand(-5,5);
foreach node in frh set _x=2,_y=rand(-5,5),_z=rand(-5,5);
foreach node in hif set _x=-2,_y=rand(-5,5),_z=rand(-5,5);
foreach node in cpn set _x=-4,_y=rand(-5,5),_z=rand(-5,5);
```

Execute the following commands in the "gel_sum.txt" script. Double click on the **sum** network. 
```
graph(nt,lt) sum = aldo;
sum .+=cpn;
sum .+=frh;
sum .+=hif;
```

![](imgs/sum10.png)

Notice how graphs are added together. When you rotate the graph, you should notice that **cpn** is not connected to the other networks. Therefore we're going to remove **cpn** using the following command.

```
sum.-=cpn;
```

![](imgs/sum11.png)

Right click and run the force-directed layout to spread out the graph.

![](imgs/sum12.png)

### Export/Save resulting merged graph

There are multiple ways to store the new graph. One command is **save**. Run the following:

```
save "sum.txt", sum; /* save the sum graph */
clear();             /* clears all data objects from Mango */
run "sum.txt";       /* reload the sum graph */
```

![](imgs/sum13.png)

Another option is to export the graph as a tab delimited file. This file can be read by Excell, or sent to R and Matlab.

```
export("sum.tsv","tsv",sum);
```

