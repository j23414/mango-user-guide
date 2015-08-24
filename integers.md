Integers
--
Integers are whole numbers such as ...-4,-3,-2,-1,0,1,2,3,4... In Gel, integers are defined with the **int** keyword and name of the variable.

```
int i;
int count;
i = 1;
i = 1 + 2;
```

Floating point numbers such as **floats** and **doubles** are rounded (up or down) to the nearest integer when assigned to an int.

```
int i = 2.3;  /* i = 2 */
int i = 2.5;  /* i = 3 */
int i = 2.8;  /* i = 3 */
```
When assigned to an integer variable, Gel will attempt to convert **strings** to a numeric value. If the string is a number such as "30", the number 30 will be stored as an int. If the string cannot be converted into a number, then zero will be stored in the int. 

```
int i = "30";     /* i = 30 */
int i = "hello";  /* i = 0 */
```
The same rounding rules apply from **floats** and **doubles**.
```
int i = "3.3";    /* i = 3 */
int i = "3.8";    /* i = 4, due to rounding up */
```
If the string contains a number as a prefix, the number will be stored as an int while the rest of the string will be ignored. The same is not true if the number is at the end of the string.
```
int i = "3 pigs"; /* i = 3 */
int i = "run 4";  /* i = 0 */
```