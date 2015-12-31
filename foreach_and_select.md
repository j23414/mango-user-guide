Changing graph attributes and Thresholding
===

GEL's method of propagating values through a network relies on foreach and select. These are simple but powerful methods for mapping data attributes to visual attributes, for updating attributes, and for propagating computation through a network. Therefore it is best to have a solid foundation on what these two statements are.

foreach 
---
The general form of the foreach statement is as follows:

**foreach** *node* | *link* **in** *graph* **where** *condition* **set** *expression* **;**

```
foreach node in airports set _x=long,_y=lat;
foreach link in flights set _r=rand();
foreach node in airports where (in+out)>10 set _text=name;
```

select 
---

The general form of the select statement is as follows:

**select** *node* | *link* **from** *graph* **where** *condition* ;

```
auto hubs = select node from airports where (in+out)>10;
auto thresh = select node from gene_net where weight>0.5;
```