# UI components in Unity
Getting started with developing UI components for 2D and 3D environments

[UI Documentation](https://docs.unity3d.com/Manual/UISystem.html)
# Components
## Canvas :
* A canvas is a group of of Ui elements which decides on how these elements are to be rendered together.
* It itself is a GameObject. 
* All UI elements should be placed inside the Canvas
* One scen can have more than one canvas
* If new UI element is created without a Canvas it will be automatically be added to a newly generated Canvas

Canvas has 3 possible render modes
1. Screen Space overlay (SSO - default)

    * All UI elements and the canvas will be rendered over the scene
    * The canvas will fill the screen automatically and resize on screen size change as well
    * It automatically adds a Rect Transform component which will be uneditable.
    * Pixel perfect - Renders UI pixels perfectly to sharpen the look
2. Screen space camera (SSC)
    * Rendered by specific camera in the scene allowing camera specific settings to be applied on the UI like applying a perspective camera to give a feeling of depth
    * Canvas will fill the viewport and resize automatically
    * Rect Transform is treated same as in Screen space overlay
    * It includes pixel Perfect option as well as an option for a Render Camera and Plane Distance.
    * If Render Camera is null the render mode will switch to SSO
    * Plane Distance dictates the distance of the canvas from the camera bu should be within camera's clipping plane
    * The UI elements will be adjusted to the Camera's frustrum allowing them to render relative to GameObjects
3. World Space
    
    *  It renders UI elements in the Scene volume
    * These are generally mobile elements like speech bubble or static objects
    * It does not set the Rect Transform component which allows the canvas to be placed wherever desired. Thus when creating mutliple canvases in the same scene generally world space rendering is used.
    * It has an EventCamera property to specify the camera which will detect events and other attribute Recieve Events dictates whetther the canvas will actually recieve any events.
    * Sorting layer and ordering layer determines the rendering order of the canvas as compared to other elements in the scene

Elements in a canvas are rendered in a top down order.
## Rect Transform
Rect Transform represents the transform parameters of a 2D rectangle of certain width set over a pivotal point which allows rendering in the scene volume as a flat 3D object   

Anchoring in UI allows an UI component to be attached to a parent element if it also happens to have a Rect Transform component and transform on the basis of the parent UI

To manipulate the rect transform component we use the rect tool using the shortcut T. With shift key pressed down the UI component resizes proportionally

Rotation takes place relative to the pivot point which can also be shifted as needed even if outside the UI element

Position fields in the rect transform shows distance in pixels from the anchor point to the pivot

The anchor points represents the 4 corners of the parent element. Thier min and max values are percentages of the parent dimensions.

If the dimensions of parent element are changes, the anchor and the UI element with it will adjust to a relative position.

If all the anchor points are joined together the UI element will remain same and not stretch as that entirely depends on the distance of its corner to the anchor points which in this case remains constant. But if the anchor points are seperated then the UI element wil resize along with the parent relative to the anchors.

* If the anchor points are set to the childs corner it will stretch similarly to the parent.
* Positioning the anchors to the corners of the parent will fix the borders of the child
* if the anchors are set on an edge of the parent then the UI element will stretch only across that edge. It will snap back to 

Scaling of UI element leads to full resize and should be primarily used for animations alone 

There two edit modes for the Rect Transform :
1. Blueprint mode : Treats the RT as if it is not rotates or scaled. Also changing the anchor and pivot values in this mode will let the UI at the same positions
2. Raw mode: Changing the RT pivot or anchors actually changes the UI element position

If the elements are goruped under layouts there RT will be controlled by those Layouts and thus be inaccessible directly

## Button
Create a button just use Create > UI > Button

It requires two scripts:
1. Button Script
    
    * Interactable : Whether the button will respond to press.
    * Button has three transitions : Normal, highlighted and pressed
    * All these transitions are represented by color tint, sprites or animations
    * The target image refers automatically to the Image component of the button if added. 
    * Animated transitions wiill require Animators which can be assigned or automatically generated.
2. Image Script  
    
    * This is used to set the image target to be displaye over the button

They also contain an optional Text element to display text overlayed on the button

Events such as button clicks are handled by the EventSystem generated automatically on creation of first UI element

Ecah button has a OnClick field which invokes a list of funcitons on button click. The first arg is the GameObject. OnClick can then call any function associated with the components of this gameobject. For a functipon to be eligible for invoing it has to have a public access specifier, void return type and take no args or float, int, Object, string, bool
## Images
Other than being stand alone graphics they are also used as backgrounds for other UI elements

Components
1. Source Image : The sprite to be displayed
2. Color Multiplier : USed for tinting or fading of color
3. Optional Material to use shadows. textures are ignored. To create an UI material, create a simple material then set shader to uGUI element
4. Image type :
    
    1. Simple 
      
        * Preserve Aspect : Image will be as large as it can be while maintaining aspect ratio

        * Set Native Size : Set to original size
    2. Slice
        * Display the image as a 9Slice sprite which is seprated in 9 sectioned grid pattern. 
        * Only the center grid section stretches allowing scaling without distortion of edges
        * Fill center determines whether the center section of such a sprite will be shown or not. 
    3. Tiled
        * Tiles (repeats) the images
    4. Filled
        * Using Fill Amount determine what portion of the image is to be shown (1 : Fully shown, 0 : not shown)
        * Fill Method and Fill Origin determine which point represents Fill amount as zero and in which direction the image will fill as it increases
        * Fill Methods can be Horizontal/Vertical/Radial. For Radial methods we can define the radial angle to start fill from. Also we can determine if fill be clockwise or not.
## Text
Text component is used to render Text on the UI layout  
Components :

Text : Holds the textual info to be displayed on the UI

Other components includeFont alignment, style, Line spacing, color, material.

Oversized text wont be displayed until horizontal/vertical overflow are set to overflow. Truncate will cut overflowing text

Best Fit ignores these settings making it as large as required

Min and max size refer to limits on font size

Text Markups let us the usage of markup language like HTML