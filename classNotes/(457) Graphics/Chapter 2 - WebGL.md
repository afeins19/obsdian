we first begin by defining an html file. We must include a reference to a javascript file containing a script that contains the webgl code.
```html
<script src="index.js"></script>
```
webgl code may be written either separately in a .js file or inline with html in a `<body></body>` tag. 

# Drawing a 2D Diagram 

1. retrieve a `<canvas>` element from the html file and import it to the javascript 
2. request he rendering *context* for the 2D graphics from the element
	- the context supports the acutal drawing features
	- the variabble **ctx** stores the results of the function call
```javascript

function main() {
	// retireve and perform additional validation 
	var canvas = document.getElementById('gl-canvas');

	var ctx = canvas.getContext('2d');

	// Draw a blue rectangle 
	// (R,G,B,A (opacity))
	ctx.fillStyle= 'rgba(0, 0, 255, 1.0)'; // sets the color 
	ctx.fillRect(120, 10, 150, 150); // fill a rectangle with this color 
}

```

# Coordinate System
webpage coordinates have the origin at the top left corner and +x & +y are all left and down from this point respectively 
![[Screen Shot 2024-08-28 at 1.49.39 PM.png]]

without webgl, we define the left and top most point of the figure (120,10) and then the dimensions (150) and (150)

# Creating a Blank Canvas 
WebGL represents color values from 0.0-1.0 for (R,G,B,A)
![[Screen Shot 2024-08-28 at 1.57.39 PM.png]]
- clearColor is the default background color of the canvas 

# Buffers
after we define a color, we need to load it from the buffer via the `COLOR_BBUFFER_BIT`. This loads the data for a clear canvas from memory. 

# Drawing a Dot
say we want to draw a red point using 10 pixels at (0.0,0.0,0.0). WebGL is a 3D graphics engine so we have (x,y,z) axis. To do this we require the following information:
- position
- color
- size

# Shaders
(fragment = pixel)
there are 2 types of shader:
- vertex shader: programs that describbe the traits (position, colors, etc.) of a vertex. The vertex is a point in space such as the corner or intersection of 2D/3D shape
- Fragment Shader: program that deals with prefragment processing such as lighting. (essentially a pixel color)

# Homogenous Coordinate System

![[Screen Shot 2024-08-28 at 2.10.06 PM.png]]
- we have an additional coordinate in the vec4() object since we are using homogeouns coordinates. This allows us to only use matrix multiplication to perform translations, rotations and other transforms.

# Initializing Shaders ![[Screen Shot 2024-08-28 at 2.12.36 PM.png]]

# Drawing the Object
![[Screen Shot 2024-08-28 at 2.12.45 PM.png]]
`gl.drawArrays(g1.POINTS, 0, 1);` 

# Homogenous Coordinates 
the benefit of this coordinate system is it allows us to easily determine whether or not an object is in the line of sight of another object (if an object blocks another object). More Importantly, this coordinate system makes it easier to perform transformations on matrices. 

Scaling, Mirroring, and Rotations are all easily achievable with only using matrix multiplication. However, if we want to move a series of points (translation), we must employ the use of addition operations. Homogenous coordinates allow us to perform transformations only using matrix multiplication.

![[Screen Shot 2024-09-04 at 1.38.51 PM.png]]