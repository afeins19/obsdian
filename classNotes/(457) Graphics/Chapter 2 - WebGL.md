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

to translate the point given by vector <x,y> by some distance dx and dy, increase the size of the matrix (nxm) to ((n+1) x (m+1)). Note we can also do the standard matrix operations in tandem with the the translation:

![[Screen Shot 2024-09-04 at 1.41.56 PM.png]]
this applies a rotation to the vector this matrix is being multiplied by as well as a translation by dx and dy. 

# The WebGL Coordinate System 
this coordinate system is different from the html coordinate system:
	- the center position of the `<canvas>`: (0.0, 0.0, 0.0)
	- the range of the x axis is (-1.0,0,0) to (1.0,0,0)
	- the range of the y axis is (0.0,-1.0,0.0) to (0.0, 1.0, 0.0)
	- the Z axis "protrudes" towards you (0.0,0.0, -1.0 to (0.0,0.0,1.0)

# Passing data between JavaScript and the Shaders 
we need to define global variables that have acces to both shader variables and js variables 
1. prepare the attribute variable for the vertex position in the vertex shader 
```WebGL		 
'attribute vec4 a_Position'; 
```
2. assign the attribute variable to the gl_position variable (this is set dynamically from the javascript rather than statically)
3. pass the data to the attribute variable 
4. assign a value to an attribute variable 

what this does is allows us to specify a position variable locally in the javascript and then send it to the shader program when its ready to be plotted. This lets us dynamically control the location where an object will be on the canvas. 

# Converting Between WebGL and HTML Coordinates 

```javascript 
var x = ev.ClientX; // x coordinate
var y = ev.ClientY; // y coordinate 

var rect = ev.target.getBoundingClient

// getting difference between your screen's boundary and the canvas boundary (if one exists)
x = ((x-rect.left) - (canvas.width/2) / (canvas.width/2))
y = ((y-canvas.top)/2 - (y - rect.top/2)) / (canvas.height/2)
```

### Points are stored in an array as a flat arrangement
```
g_points = [x_1, y_1, x_2, y_2, ...]
```
- each point is represented by 2 values in thiis array 

to iterate over these points we use:
```javascript 
for (var i = 0; i < len; i+=2)
	// do stuff 
```

# Changing the Point Color (ChangingPoints.JS)
we must pass the data to a fragment shader as fragment shaders handle colors 
1. prepare the uniform variable for the color in the fragment shader
2. assign the uniform variable to the gl_FragColor variable 
3. pass the color data to the unifrom variable from the JS program

# Shader Code
```
var FSHADER_SOURCE +
	'precision mediump float;' + 
	'uniform vec4 u_FracColor;' +
	...
```

# Uniform variables 
used to pass static information to the fragment shader 
(things like `u_FragColor`)

### Assigning a Value to a uniform Variable
```
// logic to determine which quadrant was clicked
```
