# Export Graphs

You may want to export your new networks to another program, either for statistical analysis in R or a graph visualization program of your choice. Mango provides the **export** function for this purpose.

```cpp
/* example graph */
node(string name) nt;
link[] lt;
graph(nt,lt) ran=random(20);

/* export as a csv */
export("ran.csv","csv",ran);
```

Graphs can be exported in csv, tsv, or dot formats. The csv and tsv formats first list the node (with node attributes), a hyphen, then the list of links (with link attributes).