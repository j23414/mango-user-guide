Strings
---
Strings are any type of text that contain letters, numbers and symbols. For example "c", "4 sale", and "Hello World"; Strings are defined using the keyword **string** and the variable name.

```
string s = "hello world";
string name = "Bob";
```

Strings must be surrounded by double quotation marks. Gel does not recognize single quotes. 

```
/* will not work */
string s = 'hello world';

/* will work */
string s = "hello world";
```

##String functions

**substr**

```
string s="hello world";
print substr(s,0,5); // prints first 5 characters "hello"
```

**tolower**


```
print tolower("Hello World");    // prints "hello world"
```

**toupper**

```
print toupper("Hello World");    // prints "HELLO WORLD"
```

**tocamel**

```
print tocamel("hello world");    // prints "Hello World"
```

**len**
```
print len("Hello World!");       // returns 12, length of the string
```
