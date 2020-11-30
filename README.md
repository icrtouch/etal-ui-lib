# etal-ui-lib
ETAL User interface library 

This repository is an unofficial project by an ICRTouch developer, and as such comes with no warranty or support.
Use at your own risk. Please be aware that sales records and program data could be affected.

To use this library
put the GUI folder in this location 
`/ICRTouch/etal/lib/`

Dependencies 
 - TimerControl Library, add into `/ICRTouch/etal/lib/`
 

Example of UI library
put `/example` into
 `ICRTouch/etal/`
 
 ## GENERAL INFORMATION
 ### DisplayObject
DisplayObject is the base class to which all other objects that will be rendered is derived from, this creates a flexable system, whereby you can create your own components and the render pipeline will manage all the annoying bits like click handling, z-depth control, constraints and heiarchy management.

Every display object follows this layout
`ObjectType (GUI UI, Table {})`

Here is an example of a object.
```moc
local MyBox = BoxObject(UI, {
			identifier="Wrapper",
			zDepth=1,
			clickable=false,
			position={x=0,y=0},
			size={x=50,y=50},
			color=0x000000,
		});
```
this will create a box that is 50 by 50 pixels in size.
as you can see, the positional and size properties are themselves objects that consist of
`{x:20,y:20}`

Here is a list of all the posible properties, some may not be applicaple, depending on the object.
 - identifier - (string) identifies the object, like html id
 - visible - (bool) shows or hides the object
 - clickable - (bool) enables or disables this specific object for clicking
 - position - (table {x:0,y:0}) - relative position
 - size - (table {x:0, y:0}) - size, height and width of object
 - zDepth - (int) relative z-depth of all objects on the same heiarchy level
 - color - (0xf2f2f2) - Background colour of a box derived object.
 - borderRadius - (int) - adds a curved edge to any boxObject
 - fontSize - (int) - font size of any textObject
 - fontColor - (0xf2f2f2) - colour of the font of any textObject
 - text - (String) - The text that will shoe from a textObject
 - onClick - (callback function) - when object is clicked the callback will be called.
 

### BoxObject
 ```moc
        local MyBox = BoxObject(UI, {
			identifier="Wrapper",
			zDepth=1,
			clickable=false,
			position={x=10,y=10},
			size={x=50,y=50},
			color=0xff0000,
		});
 ```
Here is a list of all the properties that are specific to boxObjects
 - identifier - (string) identifies the object, like html id
 - visible - (bool) shows or hides the object
 - clickable - (bool) enables or disables this specific object for clicking
 - position - (table {x:0,y:0}) - relative position
 - size - (table {x:0, y:0}) - size, height and width of object
 - zDepth - (int) relative z-depth of all objects on the same heiarchy level
 - color - (0xf2f2f2) - Background colour of a box derived object.
 - borderRadius - (int) - adds a curved edge to any boxObject
 - onClick - (callback function) - when object is clicked the callback will be called.

### TextObject
 ```moc
        local textObjectSample = TextObject(UI,{
			text="Sample Text Object ",
			fontSize=27,
			fontColor=Color().lightgray,
			position={x=50,y=100},
		});
 ```
Here is a list of all the properties that are specific to boxObjects
 - identifier - (string) identifies the object, like html id
 - visible - (bool) shows or hides the object
 - position - (table {x:0,y:0}) - relative position
 - zDepth - (int) relative z-depth of all objects on the same heiarchy level
 - fontSize - (int) - font size of any textObject
 - fontColor - (0xf2f2f2) - colour of the font of any textObject
 - text - (String) - The text that will shoe from a textObject
