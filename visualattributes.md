# Visual_Attributes

Nodes and links have a set of system-defined attributes. These are related to the visual representation of the graph. Listed below are all the system-defined attributes and their descriptions.

**Node System Attributes **

| Attr |Description |
| -- | -- |
|_x | x position of the node in 3D space. Center of screen x=0. Negative values go to the left and positive values go to the right. |
|_y | y position of the node in 3D space. Center of screen y=0. Negative values go to the bottom and positive values go to the top. |
|_z | z position of the node in 3D space. Center of screen z=0. Negative values go into the screen. Positive values go toward the camera and can even go behind the camera. |
|_r | Red color of the node, can be a floating point value between 0 and 1. |
|_g | Green color of the node, can be a floating point value between 0 and 1. |
|_b | Blue color of the node, can be a floating point value between 0 and 1. |
|_radius | Radius of the node. If the radius is set to 0 or negative, the node will not be shown.|
|_text | Label of the node. Can be any string value. If _text is set to "" (empty string) then no label is shown |


**Link System Attributes **

| Attr |Description |
| -- | -- |
| _r | Red color of the link, can be a floating point value between 0 and 1 |
| _g | Green color of the link, can be a floating point value between 0 and 1 |
| _b | Blue color of the link, can be a floating point value between 0 and 1 |
| _width | Width of the link. If width is set to 0 or negative, the links will not be shown.|
| _text | Label of the link. Will be located at the halfway point of the link. No current way to move the position.|