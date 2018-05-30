## 3D Geometry and perspective transformation

### Deconstructing the intrinsic matrix

fx |  0  | cx 
0  |  fy | cy 
0  |  0  |  1 


- `fx`, `fy`
  
  The shift in pixels in the x and y directions per meter displacement of a point from the optical axis at a depth of 1m.
  
- (`cx`, `cy`)

  The mid-point of the image plane.

Effectively the intrinsic matrix is used to calculate the displacement of a point in space from the optical axis expressed in the image frame in pixels.

### Deconstructing the extrinsic matrix

`rx`  |  `ry` |  `rz` |  `T`
----|-----|-----|----
r11 | r12 | r13 | tx
r21 | r22 | r23 | ty
r31 | r32 | r33 | tz

- `R` = [`rx` `ry` `rz`]

  Inverse of the camera rotation matrix relative to the world frame.

- `T` = [`tx` `ty` `tz`]' 

  Position of the world origin offset from the camera.

- `X_c` = [`R` `T`] * `x`

  `X_c` is the location of a point in the camera frame and `x` is it's location in the world frame.

#### A brief example
Suppose there is a point `p` (2,2,0) in the world frame. Assume the camera is postioned at the world origin, then `p` will be at (2,2,0) in the camera frame. Now suppose the camera translates by (2,0,0) without rotation `R` = `I` (identity), then `p` must now be at (0,2,0) in the camera frame. Therefore `T` = (-2,0,0) which indicates the offset of the origin from the new camera position.
