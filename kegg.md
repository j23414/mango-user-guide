# KEGG

Open **Mango** and click on **Databases/KEGG** in the menu.

<center>
![](img32.png)

A dialog window will pop and attempt to connect to KEGG database. It will take around a minute for a list of organisms to be shown in the first list. 

<center>
<div style="width:300px">
![](img33.png)


Select an organism from the list so it's highlighted and then click the **Fetch Pathway List** button. 

![](img34.png)

Select one pathway (click) or multiple pathways (ctrl+click, or shift+click) and hit the **Fetch Pathway Networks** button.

![](img36.png)

Each will be KEGG pathway will be loaded as a separate network.

![](img35.png)

Double click the pathway and notice how it retains the original xy coordinates from KEGG.

![](http://rest.kegg.jp/get/hsa00010/image)

Open the KEGG dialog window again, and this time check the box next to **Merge Fetched Pathways** and hit the **Fetch Pathway Networks** button. 

![](img37.png)

All selected pathways are merged into one network where each pathway has a different _z value.

![](img38.png)

