# Rotation 
we can use the standard rotation matrices to rotate our 3d objects like 2D. However, now we introduce this notion of a **viewpoint**. When rotating the object, we must rotate it in such a way that the viewpoint for that object receives an accurate display of the object. This depends on the following factors:
$$
(x,y,z, e_x,e_y,e_z)
$$where $e_{x,y,z}$ are the positions from the viewpoint. 

### Viewpoint Transform
we take the vertex coordinates form the object and then apply a transformation with the rotation matrix. We then must apply another transform to transform this product of 2 matrices with another matrix - the viewpoint matrix. 

Let 