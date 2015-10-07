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

Next we are going to randomly color the airports and bleed those colors down the links. This will emphasize flights from highly connected airports to less highly connected airports.

```
foreach node in airports where (in+out)>0 set _r=rand(0,1), _g=rand(0,1),_b=rand(0,1);
foreach link in airports where in._z>out._z set _r=in._r,_g=in._g,_b=in._b;
foreach link in airports where in._z<=out._z set _r=out._r,_g=out._g,_b=out._b;
```

In a "foreach link" statement, the special terms "in" and "out" represent the in node and out node of a link. In an undirected graph, the assignments have no further meaning. In a directed graph, the link is directed from the in node to the out node.

We can use this layout to try to set a threshold. For example, we might want to emphasize airports that are highly connected but don't know what threshold value to set. Try the following commands and see how the visualization changes.

```
foreach node in airports where (in+out)>1 set _text=airport;
foreach node in airports where (in+out)>1 set _text=city;
foreach node in airports where (in+out)>1 set _text=city."_".(in+out);
```

In this case, let's choose 40. Any airport with a connectivity above 40 will have a larger radius and be labeled by city name.

```
foreach node in airports where (in+out)>1 set _text="";
foreach node in airports where (in+out)>40 set _text=city, _radius=1;
foreach node in airports where (in+out)>0 set _z=0;
```

##Combine airports by state

Sometimes you may want to group or combine nodes. This is a one way modification so we'll create a duplicate graph called states.

```
graph(nt,lt) states=select node from airports where (in+out)>0;
foreach node in states set _radius=0.2;
foreach node in states set _text=state;
```

We can use the map command to change the node ids. This map command can either use a node attribute or a new map graph. Type **help map;** for more information.

```
states=map(states,"state");
```

The first argument is the graph name. The second argument is the node attribute for the new  node id.

In this example, we've lost the background image. Let's create a new background graph and add it to states.
```
graph(nt,lt) background=select node from airports where (in+out)<1;
states.+=background;
foreach node in background set _r=0.8,_g=0.8,_b=0.8;
```


