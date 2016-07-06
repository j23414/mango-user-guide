#Building graphs that resemble geometry objects using the lattice function and Gel commands

* **Will be available in version after Mango 1.23**

##The lattice function introduction

The new lattice() function takes a seed graph and tries to replicate the seed graph repetitively to obtain a lattice graph. The lattice graph size is controlled by both the maximum number of nodes that can be added and a maximum bounding box size; both are specified by the users:

```
help lattice;
graph = lattice(graph seed, int max_nodes, float w, float h, float d)
  seed: the seed graph that will be tiled to form the lattice graph;
        _x, _y, _z values in seed graph nodes must be set correctly.
        one node must be named 'anchor' to anchor to tiling nodes.
        one or more nodes must be named with the prefix 'tile...'
        to replicate the seed graph during the tiling process.
  max_nodes: maximum nodes that can be added to the lattice graph.
  w, h, d: width, height & depth of a bounding box that also limit
        the lattice graph; no nodes will be created outside the box.
  If any of the w, h or d values is negative, it defines a circular
        warping around the next axis, e.g, if w is -40, x-axis values
        will fall within a circle around the y-axis with circumference
        40; y-axis warps around z-axis and z-axis warps around x-axis.
```

One of the bounding box size parameter can be negative, which defines a circular warping along that dimension. It’s best to illustrate the warping effect with the following examples, so stay tuned.

The seed graph is the most important parameter to the lattice function. Since nodes in the seed graph will be replicated repetitively according to their relative positions to each other, it is important to set seed graph node positions (i.e., their _x, _y and _z values) correctly before given the seed graph to the lattice function, otherwise the lattice graph constructed by the lattice function may not be what you wanted. In most of the following examples, graph g is a seed graph given as argument and graph r is the returned lattice graph, so pay attention to how the g graph is defined and how the r graph is constructed from it; this will help you understand the usage of the lattice function better.

In all the following examples we make use of the same basic node and link type defined as follows:

```
// delcare basic node and link types; nothing fancy
node (string id) nt;
link [] lt;
```

Obviously, additional node and link attributes can be defined for the seed graph, and the resulted lattice graph will carry the same attributes. However, for efficiency, we use minimal attributes on the seed graph. Any additional graph attributes can be easily added to the lattice graph using Gel attribute promotion methods.

##Simple lattice replications

1-, 2- and 3-dimensional seed graphs will produce 1-, 2- and 3-dimensional lattice graphs, respectively:

| g graph | r graph |
| -- | -- |
|![](imgs/Picture1.png)|![](imgs/Picture2.png)|

```
// linear tiling along y-axis
graph(nt, lt) g = { ("anchor", 0, 0)[]("tile1", 0, 1) };
graph(nt, lt) r = lattice(g, 200, 10, 10, 10);
```

-----

| g graph | r graph |
| -- | -- |
|![](imgs/Picture3.png)|![](imgs/Picture4.png)|

```
// 2-D tiling along x-y plane
graph(nt, lt) g = { ("anchor", 0, 0)[]("tile1", 0, 1), "anchor"[]("tile2", 1, 0) };
graph(nt, lt) r = lattice(g, 200, 10, 10, 10);
```

-----

| g graph | r graph |
| -- | -- |
|![](imgs/Picture5.png)|![](imgs/Picture6.png)|

```
// 3-D tiling along all three axes
graph(nt, lt) g = { ("anchor", 0, 0)[]("tile1", 0, 1), "anchor"[]("tile2", 1, 0), "anchor"[]("tile3", 0, 0, 1)};
graph(nt, lt) r = lattice(g, 2000, 9.5, 9.5, 9.5);
```

We can get a box graph out of the cube graph above by using the Gel select command based on node degrees, because interior nodes of the cube will have higher link degrees than outside nodes.

-----

| g graph | r graph |
| -- | -- |
|![](imgs/Picture5.png)|![](imgs/Picture7.png)|

```
// to carve out the interior of the cube do a select based on node degrees
auto s = select node from r where in+out<6;
```

##Dimension warping

As mentioned earlier, one of the bounding box size limit given to the lattice function can be negative. In that case, it specifies a circular warping along that dimension with the circumference of the circle being the absolute value of the negative size. Lattice growth can simultaneously go on the other two non-warping dimensions, creating cylinders or ripples depending on how they were combined with the warping dimension:

| g graph | r graph |
| -- | -- |
|![](imgs/Picture8.png)|![](imgs/Picture9.png)|

```
// linear warping along z-axix (around x-axis)
graph(nt, lt) g = { ("anchor", 0, 0, 0)[]("tile1", 0, 0, 1) };
graph(nt, lt) r = lattice(g, 200, 10, 10, -10);
```

<hr />

| g graph | r graph |
| -- | -- |
|![](imgs/Picture10.png)|![](imgs/Picture11.png)|

```
// 2-D cylinder centered on x-axis (warp on z-axis and tile along x-axis)
graph(nt, lt) g = { ("anchor", 0, 0, 0)[]("tile1", 0, 0, 1), "anchor"[]("tile2", 1, 0, 0) };
graph(nt, lt) r = lattice(g, 200, 10, 10, -10);
```

<hr />

| g graph | r graph |
| -- | -- |
|![](imgs/Picture12.png)|![](imgs/Picture13.png)|

```
// ripples of circles (warp on x-axis while tiling on z-axis)
graph(nt, lt) g = { ("anchor", 0, 0, 0)[]("tile1", 0, 0, 1), "anchor"[]("tile2", 1, 0, 0) };
graph(nt, lt) r = lattice(g, 2000, -20, 10, 20);
```

##Build a pyramid

The pyramid slope degree along each of its four sides is 51.8539761° from the base according to the following website information, thus we first build a seed graph with one anchor node and 4 tile nodes one level down from the anchor at the right angle. After the seed graph is correctly defined, the lattice function easily creates a pyramid:

http://www.handylore.com/a/math-facts-about-the-great-pyramid 

| g graph | r graph |
| -- | -- |
|![](imgs/Picture14.png)|![](imgs/Picture15.png)|

```
float offset = cos(3.1415926535897932384626433*2/360*51.8539761);
graph(nt, lt) g = { ("anchor", 0, 10, 0)[]("tile1", offset, 9, -offset), "anchor"[]("tile2", offset, 9, offset), "anchor"[]("tile3", -offset, 9, offset), "anchor"[]("tile4", -offset, 9, -offset), "tile1"[]"tile2"[]"tile3"[]"tile4"[]"tile1" };
graph(nt, lt) r = lattice(g, 1000, 100, 10, 100);
```

Building an inverted pyramid is equally easy, with the seed graph now upside down.

| g graph | r graph |
| -- | -- |
|![](imgs/Picture16.png)|![](imgs/Picture17.png)|

```
float offset = cos(3.1415926535897932384626433*2/360*51.8539761);
graph(nt, lt) g = { ("anchor", 0, -10, 0)[]("tile1", offset, -9, -offset), "anchor"[]("tile2", offset, -9, offset), "anchor"[]("tile3", -offset, -9, offset), "anchor"[]("tile4", -offset, -9, -offset), "tile1"[]"tile2"[]"tile3"[]"tile4"[]"tile1" };
graph(nt, lt) s = lattice(g, 1000, 100, 10, 100);
```

The two pyramids can now be combined to form an octahedron. To do this, note that the lattice function have named each node in each pyramid in the same location with the same name, albeit the nodes are inverted along the y-axis. Realizing that, we can use simple Gel commands to rename nodes to some other names other than those in the base with a y-axis value of zero, so they become distinct. After that, a simple Gel add graph command easily combines the two pyramids to form an octahedron:

| r graph |
| -- |
|![](imgs/Picture18.png)|

```
// to merge the two pyramids to form an octahedron
// first rename all nodes other than the connecting nodes
foreach node in r where _y>0.0 set id="upper".id;
foreach node in s where _y<0.0 set id="lower".id;
// then just add the two parts together
graph(nt, lt) c = r.+s;
```

Finally, we can carve out the interior of the octahedron with a select command based on node degree:

| r graph |
| -- |
|![](imgs/Picture19.png)|

```
// carve out the interior of the octahedron with a select command
graph(nt, lt) b = select node from c where in+out<10;
```

##Build a torus graph

To build a torus graph, we must use some Gel calculations in addition to using the lattice function, as currently the lattice function allows warping only along one dimension while a torus graph needs warping along a primary axis and another warping along a secondary axis. To begin with, let’s build a cylinder with the lattice function:


```
// build a torus graph
graph(nt, lt) g = { ("anchor", 0, 0, 0)[]("tile1", 0, 0, 1), "anchor"[]("tile2", 1, 0, 0), "anchor"[]("tile3", 1, 0, 1), "tile1"[]"tile2" };
// first create a cylinder along the x-axis that will form the torus
graph(nt, lt) r = lattice(g, 2000, 40, 100, -40);
```

![](imgs/Picture20.png)