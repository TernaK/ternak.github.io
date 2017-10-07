## 3D Geometry and perspective transformation

### Deconstructing the intrinsic matrix

[fx |  0  | cx ]
[0  |  fy | cy ]
[0  |  0  |  1 ]

- fx, fy
  
  Camera focal lengths expressed in pixels. Think of fx amd fy as the dimensions in pixels of a square parrallel to the image plane 1m away from the optical center of the camera.
  
- (cx, cy), **P** or principal point

  Coordinates of the optical center of the camera expressed in the camera frame. This is where the optical axis passed through the image.

Effectively the intrinsic matrix is used to calculate the displacement of the point in space from the optical axis expressed in the image frame in pixels.

### Deconstructing the extrinsic matrix

`rx`  |  `ry` |  `rz` |  `T`
----|-----|-----|----
r11 | r12 | r13 | tx
r21 | r22 | r23 | ty
r31 | r32 | r33 | tz

- rx, ry, rz

  x,y,z-axis basis of the camera fre

- R = [rx ry rz]

  Inverse of the camera rotation matrix relative to the world frame

- T = [tx ty tz]' 

  Position of the world origin offset form the camera

- X = [R | T] * x

  **X** is a point at **x**, which is in world coordinates, expressed in the camera frame coordinates   

#### A brief example
Suppose there is a point `p` (2,2,0) in the world frame. Assume the camera is postioned at the world origin, then `p` will be at (2,2,0) in the camera frame. Now suppose the camera translates by (2,0,0) without rotation **R** = **I** (identity), then `p` must now be at (0,2,0) in the camera frame. Therefore **T** = (-2,0,0) which indicates the offset of the origin from the new camera position.
