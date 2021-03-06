# Graph Layouts

Each node in a graph has the following system variables for xyz coordinates.

```
_x
_y
_z
```

Therefore you can directly modify these node attributes to create customized layouts.

## Create a Random Network

```
foreach node in graph set _x=rand(-10,10),_y=(-5,5), _z=rand(-2,2);
```

![](imgs/rand.png)

## Default Layouts

```
layout(graphname, "circle");
layout(graphname, "random");
layout(graphname, "cube");
```

![](imgs/cube.png)

![](imgs/circle.png)

## Hive Plot Example

![](imgs/hive2D.png)

```
/* hive plot, 5 groups */
int i;
float f;
foreach node in flights set i=log(in+out),f=rand(1,10), _y=sin(2*3.14/5*i)*f, _x=cos(2*3.14/5*i)*f;
foreach node in flights set i=(log(in+out)),f=rand(1,10), _y=sin(2*3.14/5*i)*10*(log(in+out)-i+0.8), _x=cos(2*3.14/5*i)*10*(log(in+out)-i+0.8);

/* coloring */
foreach node in flights where log(in+out)<2.49 || log(in+out)>4.51 set _r=1;
foreach node in flights where log(in+out)>=1.49 && log(in+out)<3.50 set _g=1,_b=0;
foreach node in flights where log(in+out)>=3.50 && log(in+out)<5.50 set _b=1;
foreach link in flights set _r=(in._r+out._r)/2.0,_g=(in._g+out._g)/2.0,_b=(in._b+out._b)/2.0; 

```

## Crown Plot Example

![](imgs/crown.png)
```c
layout(graphname, "circle");
foreach node in graphname set _z=(in+out)/5.0;

/* coloring */
foreach node in graphname set _r=rand(0,1),_g=rand(0,1),_b=rand(0,1);
foreach link in graphname where in._z>out._z set _r=in._r,_g=in._g, _b=in._b;
foreach link in graphname where in._z<out._z set _r=out._r,_g=out._g, _b=out._b;
```

## Direct Map Example

![](imgs/flights01.png)

```
foreach node in airports set _x=long, _y=lat, _z=0;
center(airports,"DEN");
```

## Bipartite Graph Example

![](imgs/bipartite.png)

```
/* bipartite layout */
foreach node in bipartite where group==1 set _x=-10, _y=rand(-12,12),_z=0;
foreach node in bipartite where group==0 set _x=10, _y=rand(-12,12),_z=0;

/* coloring */
foreach node in bipartite where group==1 set _r=rand(),_g=rand(),_b=rand();
foreach link in bipartite where in._x<0 set _r=in._r, _g=in._g, _b=in._b;
foreach link in bipartite where out._x<0 set _r=out._r, _g=out._g, _b=out._b;
foreach link in bipartite where in._x>0 set in._r+=_r,in._g+=_g,in._b+=_b;
foreach link in bipartite where out._x>0 set out._r+=_r,out._g+=_g,out._b+=_b;
foreach node in bipartite where group==0 set _r=_r/(in+out),_g=_g/(in+out),_b=_b/(in+out);

```

