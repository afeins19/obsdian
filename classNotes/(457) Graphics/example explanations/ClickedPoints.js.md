### Event Handler
this is used to register clicks that the user performs on the mouse asynchronously. The coordinates of the mouse click are recorded to setup an event we must setup a function that performs some task 
```
canvas.onmousedown = function(ev) { click(Ev, gl, canvasl, a_position };
```
note that this is an anonymous function. This function stores the mouse click information in an event() object. This is then passed to the browser. 

### How WebGL Plots
every time something new is plotted to the canvas, WebGL **CLEARS** the entire canvas and then replots all previous points including the new one(s)