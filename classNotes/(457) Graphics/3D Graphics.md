q# Rotation 
we can use the standard rotation matrices to rotate our 3d objects like 2D. However, now we introduce this notion of a **viewpoint**. When rotating the object, we must rotate it in such a way that the viewpoint for that object receives an accurate display of the object. This depends on the following factors:
$$
(x,y,z, e_x,e_y,e_z)
$$where $e_{x,y,z}$ are the positions from the viewpoint. 

### Viewpoint Transform
we take the vertex coordinates form the object and then apply a transformation with the rotation matrix. We then must apply another transform to transform this product of 2 matrices with another matrix - the viewpoint matrix. 

# Box-Shaped Viewing
initially, we will just consider a box where all vertices contained within are visible and those outside are not (3 triangles in box example from powerpoint).
![[Screen Shot 2024-10-16 at 1.38.00 PM.png]]

![[Screen Shot 2024-10-16 at 1.38.22 PM.png]]

### Lack of Depth
the issue with this space is that there is no notion of depth in the box. The distances between triangles will not affect how large they appear with respect to each other as distance changes. 
### Clipping 
as soon as an object protrudes out of the box, the section that protrudes out is clipped. To avoid the issue of clipping we can **increase the volume of the box**. This can be done with: 
```js 
setOrtho() // sets the viewing volume 
```

# Quadrangular Pyramid 
to overcome the issue of depth, we can use a **quadrangular pyramid** viewing shape instead of the box. This will allow you to give a sense of depth
![[Screen Shot 2024-10-16 at 2.00.54 PM.png]]
distance between objects is now related proportionally to the size in which they appear to the viewer 
### View Design

![[Screen Shot 2024-10-16 at 2.01.22 PM.png]]

### Field of View (FoV)
with a really wide angle FOV, you lose a lot of depth information because you have a large amount of objects in the immediate vicinity. The way this is really defined is the ratio of the area of the rectangular near clipping area and the far clipping pane

### Aspect Ratio
the ratio of width to height - this is specifically with regards to the **near clipping plane** 

### Summary
so the only 3 things we need to simulate depth are:
- Field of View 
- Aspect Ratio
- Clipping Planes 