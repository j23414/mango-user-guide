Floats and Doubles
---

Floats are numeric values that can have decimal precision such as 2.3, 4.55, and -204.808. Doubles have twice the decimal precision than floats. Floats and doubles are defined with the **float** and **double** keywords respectively.

```
float f;
float weight;

double d;
double milligrams;

f=2.3;
d=3.3/4.4;
```

During assignment, values must have at least one number to the left of the decimal place.

```
/* does not work */
float f = .1;
double d = .5; 

/* must use */
float f = 0.1;
double d = 0.5;
```

When assigning mathematical expressions to a float or a double, rounding might occur. This happens if none of the numbers have at least one number to the right of the decimal place.

```
float f = 4/3;   /* f = 1.000 */
float f = 4.0/3; /* f = 1.333... */ 

double d = 4/3;   /* d = 1.000 */
double d = 4.0/3; /* d = 1.333... */ 
```

**Integers** can be assigned to a float or double variable with no real change. 
```
float f = 3;   /* f = 3.0000 */
double d = 4;  /* d = 4.0000 */
```

Gel will attempt to convert **strings** if assigned to a float or double. If conversion is not possible, then the assigned value is 0.

```
float f = "3.4";   /* f = 3.4 */
float f = "hello"; /* f = 0.0 */
```

If the string contains a number as a prefix, the number will be stored while the rest of the string will be ignored. The same is NOT true if the number is at the end of the string.
```
float f = "3 pigs"; /* f = 3.0 */
float f = "3.5 pigs"; /* f = 3.5 */
float f = "run 4";  /* f = 0   */
```