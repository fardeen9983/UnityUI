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