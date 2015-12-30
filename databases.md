# Connecting to external databases

Currently Mango provides methods to connect to the following network databases. Any added databases will be under the **Databases** Menu.
<center>
![](img32.png)

##KEGG

Since it was motivated by bioligical research, we created a method to fetch biological pathways data from KEGG. KEGG contains biological pathways data manual curated and integrated in a way to compare across organisms. KEGG stands for Kyoto Encyclopedia of Genes and Genomes.


#Other sources of network data
The number of size of online databases continue to grow. This is a listing of some public network repositories to get you started.


SNAP
--
SNAP or Standford Large Network data set collection contain publicly available social networks, networks with ground-truth communities, communication networks, citation networks, collaboration networks, web graphs, amazon networks, internet networks, road networks, autonomous systems, signed networks, wikipedia networks, twitter and other online communities. The data is available from https://snap.stanford.edu/data. 

WGCNA
---
Weighted Gene Correlation Network Analysis can help generate gene to gene correlation networks. It computes the Pearson Correlation Coefficient between all pairs of genes and then applies a soft threshhold function to create a network that follows the power law of connectivity. This is because biological networks are usually scale-free which connectivity follows a power law.