# Airline Flights Example

http://blog.revolutionanalytics.com/2011/05/mapping-airline-flight-networks-with-r.html

This is the propagate example from Mango using the flights data from the blog.
![](fromDSM.png)

* Put github link here.
* Folder should contain processed flights and airlines network. 
* User opens gel.txt. Runs line by line and explore the network.
* 

## Load airports and flights data
```
node(string iata, string airport, string city, string state, string country, 
float lat, float long) nt;
link[int cnt, string airline] lt;

graph(nt,lt) airports=import("airports.net");
graph(nt,lt) flights=import("flights.net");
```

Since airports contains longitude and latitude values, map them to xy coordinates and center the graph on Denver Airport.
```
/* layout */
foreach node in airports set _x=long, _y=lat, _z=0;
center(airports,"DEN");
```

Add in the flights data:
```
airports += flights;
foreach link in airports set _width=0.1;
```

If you zoom in on the graph, some of the airports are unconnected. Flights only contains major airlines. We could delete unconnected nodes by typing the following: Do not run this code yet.

```
airports=select node from airports where (in+out)>0;
```
But since we want to keep the shape of the United States, we are going to use those  unconnected nodes as a background, moving them back 3 units and setting their color to grey.

```
foreach node in airports where (in+out)<1 set _z=-3,_r=0.8,_g=0.8,_b=0.8;
```

You can click on the graph and drag to tilt the visualization. Since this is already a 3D graph, we can make further use of the z dimension. For example, we can map connectivity of the airports to height.

```
foreach node in airports where (in+out)>1 set _z=(in+out)/7.0;
```

In a "foreach node" statement, the special terms "in" and "out" represent the number of in degrees for a node and out degrees for a node. I've scaled connectivity by 7.0, so it doesn't jump too far out of the screen. Feel free to adjust as you need.

```
foreach node in airports where (in+out)>0 set _r=rand(0,1), _g=rand(0,1),_b=rand(0,1);
foreach link in airports where in._z>out._z set _r=in._r,_g=in._g,_b=in._b;
foreach link in airports where in._z<=out._z set _r=out._r,_g=out._g,_b=out._b;
```

In a "foreach link" statement, the special terms "in" and "out" represent the in node and out node of a link. In an undirected graph, the assignments have no further meaning. In a directed graph, the link is directed from the in node to the out node.

