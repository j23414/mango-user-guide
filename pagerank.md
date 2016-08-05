# PageRank

The PageRank algorithm outputs a probability distribution used to represent a likelihood that a person randomly clicking on links will arrive at any particular page. The algorithm requires several iterations, where all nodes start at an equal probability. One function for computing the pagerank of a particular node V at one iteration is given below, although there are certainly others:

$$
PR(v_i) = \sum(PR(v_j)I_{ij})
$$

Where $$I_{ij}$$ is an indicator variable equal to 1 if $$v_i$$ and $$v_j$$ are connected and 0 otherwise.

The following gel code computes pagerank on an undirected graph. A pagerank computation on a directed graph (more likely scenario) will be added later...

**Gel Code**

```
// Initializes graph
node(string name, float rank, float delta, int deg) nt;
link[] lt;
int n=10;
graph(nt,lt) ran=random(n);

float start=1.0/n;
foreach node in ran set rank=start, delta=0, deg=(in+out);

// Run the following two lines each iteration. 
foreach link in ran set in.delta+=out.rank/out.deg, out.delta+=in.rank/in.deg;
foreach node in ran set rank=delta, delta=0, _text=rank;
```
