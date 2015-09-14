# KEGG

Open **Mango** and click on **Databases/KEGG** in the menu.

<!--<center> -->
![](img32.png)

A dialog window will pop and attempt to connect to KEGG database. A list of the current organisms on KEGG will be fetched. This may take up to a minute depending on your internet speed. 

<div style="width:400px">
![](img33.png)


Select an organism from the list so it's highlighted and then click the **Fetch Pathway List** button. 

You may also type into the search box and press **Enter/Return** to search for a particular organism. Pressing **Enter** multiple times will search for the next match. Clicking on the header will sort the list by column. 

<div style="width:400px">
![](img34.png)

Select one pathway (click) or multiple pathways (ctrl+click, or shift+click) and hit the **Fetch Pathway Networks** button.

<div style="width:500px">
![](img36.png)

Each will be KEGG pathway will be loaded as a separate network.

<div style="width:500px">
![](img35.png)

Double click the pathway and notice how it retains the original xy coordinates from KEGG.

<div style="width:400px">
![](http://rest.kegg.jp/get/hsa00010/image)

Open the KEGG dialog window again, and this time check the box next to **Merge Fetched Pathways** and hit the **Fetch Pathway Networks** button. 

<div style="width:500px">
![](img37.png)

All selected pathways are merged into one network where each pathway has a different _z value.

<div style="width:500px">
![](img38.png)

