# Looping structures

Gel currently contains while, do while, and for loops.

*while loop*
```
int i=0;
while(i<10){
  i++;
}
```

*for loop*
```
int i=0;
int j=0;
for(i=0; i<20; i++){
  j+=i*5;
}
```
## Loops that wait for the user input

The following code iterates a variable *i* until the user presses the ESC key. Try it. You should see the i variable update within the data panel. You may need to make sure the cursor is in the console. If the graph canvas has the focus, the ESC key will be ignored. Click on the Console or Editor an then click ESC to stop. 

```
int i=0;
string stop="no";
while(stop!="yes"){
  i++;
  stop=pause(1);
}
```

# Graph Animation

This allows animation of the graphs. The following code generates a random graph and then randomly assigns colors ever 500 milliseconds.

```
node(string id, float value, float temp) nt;
link<> lt;
graph(nt,dlt) dg=random(50);

layout(g,"random");
foreach link in g set _width=0.5;
/* double click on g in Data Panel to show in graph canvas */

string stop="no";
while(stop!="yes"){
  foreach node in g set _r=rand(),_g=rand(),_b=rand();
  stop=pause(500);
}
```

![](imgs/ranloop.gif)

Remember to click on the Editor or Console and press ESC key to stop the animation. 

# Graph Simulation
Then you can do more complicated stuff like propagation of values.

```
node(string id, float value,float temp) nt;
link<> dlt;
graph(nt,dlt) dg=random(50);

/* double click on dg in data panel to show in graph canvas */

layout(dg,"random");
foreach link in dg set _width=0.1;
foreach node in dg set _r=rand(),_g=rand(),_b=rand();

/* assign random values to each node from 0.5 to 10.0*/
foreach node in dg set value=rand(0.5,10.0);
foreach node in dg set _text=value;

string stop;
while(stop!="yes"){
  foreach node in dg set temp=0,value=value/(in+out);
  foreach link in dg set out.temp+=in.value;
  foreach node in dg set value=temp, _text=value;
  stop=pause(500);
}
```

![](imgs/proploop.gif)