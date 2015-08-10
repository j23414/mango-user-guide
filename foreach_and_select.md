foreach and select
===

GEL's method of propagating values through a network relies on foreach and select. These are simple but powerful methods for mapping data attributes to visual attributes, for updating attributes, and for propagating computation through a network. Therefore it is best to have a solid foundation on what these two statements are.

foreach 
---
The general form of the foreach statement is as follows

**foreach** *node* | *link* **in** *graphname* **where** *condition* **set** *expression* **;**


select 
---