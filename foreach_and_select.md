Changing graph attributes and Thresholding
===

GEL's method of propagating values through a network relies on foreach and select. These are simple but powerful methods for mapping data attributes to visual attributes, for updating attributes, and for propagating computation through a network. Therefore it is best to have a solid foundation on what these two statements are.

foreach 
---
Use **foreach** to query and map node and link attributes. The general form of the foreach statement is as follows:

**foreach** *node* | *link* **in** *graph* **where** *condition* **set** *expression* **;**

```
foreach node in airports set _x=long,_y=lat;
foreach link in flights set _r=rand();
foreach node in airports where (in+out)>10 set _text=name;
```

select 
---
Use **select** to pull out a subgraph. The general form of the select statement is as follows:

**select** *node* | *link* **from** *graph* **where** *condition* ;

```
auto hubs = select node from airports where (in+out)>10;
auto thresh = select node from gene_net where weight>0.5;
```

## Special case of in/out for nodes vs links

When you use **foreach node**, the terms **in** and **out** refer to in-degree (number of links going into a node) and out-degree (number of links going out of a node). Therefore the sum of **in** and **out** is the total degree of the node. 

```
foreach node in g set _text=(in+out);      /* label the nodes by degree */
foreach node in g set _radius=log(in+out); /* size of node directly related to degree */
```

When you use **foreach link**, the terms **in** and **out** refer to in-node and out-node. Since **in** and **out** represent the two connected nodes, they can be used to access, process and propagate node attributes. As an example, we can color the link by the average color of two connected nodes. 

```
/* color link the average color of the two connected nodes */
foreach link in g set _r=(in._r+out._r)/2, _g=(in._g+out._g)/2, _b=(in._b+out._b)/2;  
```

Or if you had a directed graph, the value of the in-node could be passed to the out-node.
```
node(string id) nt;
link<> lt;  /* directed graph */
graph(nt,lt) g=random(10);

layout(g,"random");

int i=0; /* used to convert random float to integer */
foreach node in g set _b=1, i=rand(0,10),_text=i;

/* propagate values */
foreach link in g set out._text=in._text;

```

