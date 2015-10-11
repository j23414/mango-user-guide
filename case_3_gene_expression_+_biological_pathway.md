# Case 3: Gene Expression + Biological Pathway


Fetch the demo files and gel script from the following git hub site.

https://github.com/j23414/Mango_Workshop

Load in the example microarray data and visualize it. 
```
node(string id, string name, float c1, float cn1, float cs1, float hs1, float n1, float pH1, float sd1, float description) nt;
link[] lt;
graph(nt,lt) eco_expr=import("eco_expr.tsv","\t");
layout(eco_expr,"cube");

```