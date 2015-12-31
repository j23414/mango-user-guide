# Export Graphs

You may want to export your new networks to another program, either for statistical analysis in R or a graph visualization program of your choice. Mango provides the **export** function for this purpose.

```
/* example graph */
node(string name) nt;
link[] lt;
graph(nt,lt) ran=random(20);

/* export as a csv */
export("ran.csv","csv",ran);
```

Graphs can be exported in csv, tsv, or dot formats. The csv and tsv formats first list the node (with node attributes), a hyphen, then the list of links (with link attributes).

```
a
b
c
d
-
a,b
a,c
c,d
```

##Separate the exported graph file into node list and link list files.
Anything above the single - is the node list. You can either copy and paste the items above it into a new file or use the following perl script to generate the node list.
```perl
#! /opt/local/bin/perl

use strict;
use warnings;

my $p=1;
while(<>){
    chomp;
    if(/^-$/){
        $p=0;
    }
    if($p==1){
        if(/#graph/){
            # do nothing
        }elsif(/#(.+)/){
            print "$1\n";
        }else{
            print "$_\n";
        }
    }
}
```

```
perl export2nodelist.pl ran.csv > ran_nodes.csv
```

The following perl script generates the link list.

```perl
#! /opt/local/bin/perl

use strict;
use warnings;

my $p=0;
while(<>){
    chomp;
    if($p==1){
        if(/#(.+)/){
            print "$1\n";
        }else{
            print "$_\n";
        }
    }
    if(/^-$/){
        $p=1;
    }
}
```

```
perl export2linklist.pl ran.csv > ran_edges.csv
```