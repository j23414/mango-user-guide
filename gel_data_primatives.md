# GEL Data Primatives

Open **Mango** and you should be presented with the following screen. The window is divided into four sections. 

* Data: displays a list of all data objects in Mango 
* Canvas: displays the
* Console:
* Editor

There are **4 data primatives** in GEL: **integers**, **doubles**, **floats**, and **strings**. Type the following commands (ignoring comments between ```/* ...*/```

```
int i = 0; 
float f = 1.1;
double d = 2.2 / 3.3;
string s = "Hello World";
```

Use the **print** and **desc** commands to display the values of data objects in the **Console** panel. Their behaviors are subtly different.

```
/* print displays strings and data objects */
print i;
print "I have 3 apples";
print "var: i=",i, " f=", f, " d=", d, " s=", s;

/* desc only displays data objects */
desc f;
desc i,f,d,s;
desc "hi";     /* this will throw an error */
desc;          /* this will print all data objects */
```

Go under the Data pane, and expand some of the objects
