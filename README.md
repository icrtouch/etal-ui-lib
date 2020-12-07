# etal-ui-lib
ETAL User interface library 

This repository is an unofficial project by an ICRTouch developer, and as such comes with no warranty or support.
Use at your own risk. Please be aware that sales records and program data could be affected.

To use this library
put the GUI folder in this location 
`/ICRTouch/etal/lib/`

Dependencies 
 - TimerControl Library, add into `/ICRTouch/etal/lib/`
 - StateManagement Library, add into `/ICRTouch/etal/lib/`
 

Example of UI library
put `/example` into
 `ICRTouch/etal/`


 # UI Class
 The UI Class's role is to manage and control all the display objects.
 
 UI object methods
  - **createWindow(String XMLFile)**
  -- This will tell the UI library which window it should be rendering on.
  - **enableWindow()**
  -- Enables the window to be drawn on touchpoint
  - **disableWindow()**
  -- Disables the window to be drawn on touchpoint
  - **redraw()**
  -- forces the screen to redraw, you can call this after changes a display objects properties to see the change.
  - **addObject(DisplayObject object)**
  --  Add a object to the ui object, on the root level. (this in reality only needs to be done once)
  - **findObject(String identifier)**
  -- if you have given an object an identifier, you can find this object by using this function, it will return the object.
  - **removeDisplayObject(INT ID)**
  -- remove the display object from the UI instance, this is by integer ID only.
 
 # Display Objects


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
 

DisplayObject Methods
 - **addChildObject(DisplayObject object)**
 -- This function will add any other display object as a child of the current object, this can be called on any display object, even if they are themselves a child.
 - **removeAllChildObjects()**
 -- deletes all childObjects of the current object, even children of children.
 - **getParent()**
 -- This function will, if it exists, get the parent object.
 - **setPosition(x,y)**
 -- sets the objects position property
 - **setSize(x,y)**
 -- sets the objects size property

    

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
 - fontName - (String) - font name/type that the text will use.
 - text - (String) - The text that will shoe from a textObject


 # Constraint Controllers
 Constraint controllers are the backbone of the GUI library, it allows easy and dynamic capabilities with very minimal code
 for example, setting the width of a box to a percentage, or even centering the box on the x or y or both axis. 
 
 An example of a constraint controller being centered would be as follows
 ```moc
	 local MyBox = BoxObject(UI, {
			identifier="CenterME",
			zDepth=1,
			clickable=false,
			size={x=50,y=50},
			color=0xff0000,
		});
	local cc = ConstraintController()
	cc.setX(CenterConstraint())
	cc.setY(CenterConstraint())
	myBox.setConstraintController(cc)
 ```
As you can see, with very little code you can center a box perfectly.
Note how we did not need to provide a position for the box, as the constraint controller now "Controls" those properties

The constraintController itself has 4 methods they are as follows, each method take in a Constraint type Object
 - setX(Controller)
 - setY(Controller)
 - setWidth(Controller)
 - setHeight(Controller)

At current there are two types of constraint controllers
CenterConstraint() & PercentConstraint

Here I will list what properties each can control

**CenterConstraint()**
 - X position
 - Y position

**PercentConstraint()**
 - X position
 - Y position
 - Width
 - Height
