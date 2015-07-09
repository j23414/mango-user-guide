## Install Mango

Install **Mango** by going to http://www.complex.iastate.edu/download/Mango and registering a free account. You will receive an email shortly with your new password. Use your email and new password to log into the download area and select the installation file for your operating system. 

## Quick Start Demo
Open **Mango** and you should be presented with the following screen.

![](start.png)

The **Console** (bottom right) is where you can type and execute GEL commands. All GEL commands end with a semi-colon symbol. Type the following into the **Console** and press **Enter/Return**:

```
setwd();
```

**setwd** pops a window to allow you to select the current working directory. This directory may contain your graph or GEL script files. Navigate and select the **DemoFiles** folder that came with Mango installation.

![](setwd.png)

Now we're going to load 4 graph files. Go to **File/Open** and select "loadnet.txt". The file should be loaded into the **Editor** panel.

![](loadnet.png)

Click within the loadnet.txt, and place the cursor at the first line. Then press Alt-Enter if you're on Mac or Ctrl-Enter if you're on Windows or Linux to execute one line. Repeat this until all four graphs have been loaded into Mango. They will be listed in the **Data** panel. 