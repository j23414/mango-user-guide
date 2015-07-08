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
node(stringname,float_x)nt; //Will throw a syntax error
```
