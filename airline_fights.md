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
airports += flights;
foreach link in airports set _width=0.1;
```