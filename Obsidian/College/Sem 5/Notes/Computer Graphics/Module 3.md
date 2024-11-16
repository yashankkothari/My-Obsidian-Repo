## 3.1 Clipping: clipping window, normalization and viewport transformations, clipping algorithms,2D point clipping, 2D line clipping algorithms: cohen-sutherland line clipping only - polygon fill area clipping: Sutherland-Hodgeman polygon clipping algorithm only.

### Clipping points and Lines

#### Point Clipping
- **Definition**: Point clipping evaluates whether a point lies within a defined clipping window.
- **Clipping Window Boundaries**: 
  -  Xmin,  Xmax,  Ymin, and Ymax define the clipping window.
- **Inequalities**: A point \( (x, y) \) is considered inside the clipping window if the following inequalities are true:
![[{51E10881-FF21-41C8-AD78-F4687C9DFE38}.png]]

#### Clipping Lines
- **Definition**: Clipping lines in an OpenGL environment involves the automatic removal of parts of lines that fall outside the defined world window.
- **Result**: Only the portions of the lines that lie within the clipping window are rendered, ensuring efficient graphics processing and display.
- **Automatic Clipping**: OpenGL uses specific algorithms to clip each object to the world window boundaries.

#### Clipping a Line using Cohen Sutherland Line Clipping Algorithm

- In the algorithm, first of all, it is detected whether the line lies inside the screen or it is outside the screen. All lines come under any one of the following categories:
  - **Visible**: 
    - If a line lies within the window, i.e., both endpoints of the line lie within the window. A line is visible and will be displayed as it is.
  - **Not Visible**: 
    - If a line lies outside the window, it will be invisible and rejected. Such lines will not display. If any one of the following inequalities is satisfied, then the line is considered invisible:
    - Example:
      - Let  A(x1, y1) and B(x2, y2) be endpoints of the line.
      -  x_min, x_max are coordinates of the window.
      -  y_min, y_max are also coordinates of the window.
      - The conditions for not visible are:
        - \( x_1 > x_{max} \)
        - \( x_2 > x_{max} \)
        - \( y_1 > y_{max} \)
        - \( y_2 > y_{max} \)
        - \( x_1 < x_{min} \)
        - \( x_2 < x_{min} \)
        - \( y_1 < y_{min} \)
        - \( y_2 < y_{min} \)
  - **Clipping Case**: 
    - If the line is neither in the visible case nor in the invisible case, it is considered to be in the clipped case.
    - The category of a line is found based on nine regions given below. All nine regions are assigned codes. Each code is of 4 bits. If both endpoints of the line have end bits zero, then the line is considered to be visible.
![[{97CC4ECF-30DB-4021-9774-349782CB75C9}.png]]

• The center area is having the code, 0000, i.e., region 5 is considered a rectangle window. 
   • Line AB is the visible case
   • Line OP is an invisible case 
   • Line PQ is an invisible line
   • Line IJ are clipping candidates
   • Line MN are clipping candidate 
   • Line CD are clipping candidate
   
![[{09E52248-2C81-482E-A102-5C1BB7063688}.png]]

##### Advantage of Cohen Sutherland Line Clipping
- It calculates endpoints very quickly and can reject or accept lines efficiently.
- It can clip pictures much larger than the screen size.

##### Algorithm of Cohen Sutherland Line Clipping

![[{55F63A88-A4D9-4B30-80B8-10E3D26DEE3D}.png]]
![[{6A6CA45B-D601-4255-9770-3EBB876E62EE}.png]]

##### Example of Cohen-Sutherland Line Clipping Algorithm
![[{5C202124-11E6-4792-9465-CD4A8FBE4362}.png]]
![[{580DE5DB-6653-49E6-9C1D-06754A86A442}.png]]
![[{E11DF315-F3DC-4FA9-897F-1B9217869A8B}.png]]
![[{488815F0-0455-46F8-869B-A48D08FFE921}.png]]

## 3.2 3DGeometric Transformations: 3D translation, rotation, scaling, composite 3D transformations, other 3D transformations, affine transformations, OpenGL geometric transformations functions.

## 3.3  Color Models: Properties of light, color models, RGB and CMY color models. Illumination Models: Light sources, basic illumination models-Ambient light, diffuse reflection, specular and phong model, Corresponding openGL functions.

