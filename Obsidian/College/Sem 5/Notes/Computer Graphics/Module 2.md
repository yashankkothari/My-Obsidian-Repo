## 2.1 Fill area Primitives: Polygon fill-areas, OpenGL polygon fill area functions, fill area attributes, general scan line polygon fill algorithm, OpenGL fill-area attribute functions 

### Fill area Primitives
- **Area Filling**: A technique to fill or color a defined area, object, or image.
- **Polygon Filling**: Involves filling or highlighting all pixels inside a polygon's boundaries with a chosen color.
- **Two Primary Algorithms**:
    1. **Seed Fill Algorithm**: Fills an area by starting from a seed point inside the polygon and spreading outward.
    2. **Scan Line Algorithm**: Fills polygons by scanning across each line, determining which parts of the polygon to fill on each scan line.

These methods ensure that all pixels within the polygon are distinct from the background.

![[{5CB15BC8-C465-49F3-BB0E-316FD0954B13}.png]]

##### Fill Area Methods
- **Four-Connected Approach**:
    - Tests and fills pixels that are **directly adjacent** to the current pixel (left, right, above, below).
- **Eight-Connected Approach**:
    - Tests and fills pixels that are **adjacent and diagonal** (left, right, above, below, and four diagonal directions).


#### Seed Fill Algorithm
In this seed fill algorithm, we select a starting point called seed inside the boundary of the polygon. The seed algorithm can be further classified into two algorithms: Flood Fill and Boundary filled.

![[{5B5765D6-501D-4FBB-91A1-35ED68AA9C5F}.png]]

##### Flood-fill Algorithm
• **Flood-Fill Algorithm**: Defines a region starting from a point in a multi-dimensional array.  
• **Comparison**: Similar to the **bucket tool** in paint programs.  
• **Implementation**: Uses a **stack-based recursive function** to replace connected pixels with the fill color.  
• **Replacement**: Replaces pixels of a specific **interior color**, not boundary color.

###### Algorithm of Flood-fill
• **Parameters**: Takes coordinates (x, y), a fill color, and the old color as inputs.  
• **Condition**: If the pixel at (x, y) matches the old color, it gets replaced by the fill color.  
• **Recursion**: The procedure recursively calls itself for the pixels to the **right (x+1)**, **left (x-1)**, **above (y+1)**, and **below (y-1)** until all relevant pixels are filled.

Here's the algorithm written in a code block:
```c
void floodfill(int x, int y, int fill_color, int old_color) {
    if (getpixel(x, y) == old_color) {
        setpixel(x, y, fill_color);
        floodfill(x + 1, y, fill_color, old_color);  // Fill right
        floodfill(x - 1, y, fill_color, old_color);  // Fill left
        floodfill(x, y + 1, fill_color, old_color);  // Fill above
        floodfill(x, y - 1, fill_color, old_color);  // Fill below
    }
}
```
![[{278C8E1A-7DA5-4C0D-8D4C-62901C7D3699}.png]]

###### Advantages of Flood-fill Algorithm

• Provides an easy way to fill color in graphics.  
• Colors the entire area by filling interconnected pixels with a single color.  
• Effectively fills the same color inside defined boundaries.

###### Disadvantages of Flood-fill Algorithm

• **Very slow** compared to other algorithms.  
• **May fail** when handling large polygons.  
• Initial pixel requires **more knowledge** about the surrounding pixels.

##### Boundary-fill Algorithm
• Also known as the "Edge-fill algorithm."  
• Used for **area filling** in graphics.  
• Helps in **creating attractive paintings** by filling enclosed areas.  
• The algorithm **travels each pixel** until it reaches the specified boundary if the object has a single-colored boundary.
![[{5E66FCE6-0DD2-48B9-A792-DB8BBBCE8D18}.png]]

###### 4-connected and 8-connected methods
![[{AAD1B919-1405-4907-927C-8CF026EE371E}.png]]

###### Algorithm of Boundary-fill
```c
Procedure boundary_fill(p, q, fill_color, boundary) {
    // Step 1: Initialize the boundary of the region.
    
    // Step 2: Get the interior pixel (p, q).
    // Now, define an Integer called current pixel and assign it to (p, q).
    int current_pixel = getpixel(p, q);
    
    // Step 3: Check if the current pixel is neither the boundary nor the fill color.
    if (current_pixel != boundary && current_pixel != fill_color) {
        // Set the pixel to the fill color.
        setpixel(p, q, fill_color);
        
        // Recursive calls to check neighboring pixels.
        boundary_fill(p+1, q, fill_color, boundary);  // Right
        boundary_fill(p-1, q, fill_color, boundary);  // Left
        boundary_fill(p, q+1, fill_color, boundary);  // Up
        boundary_fill(p, q-1, fill_color, boundary);  // Down
    }
    
    // Step 4: End.
}
```

###### Problems with Boundary-fill algorithm
- **Incomplete Filling**: Sometimes, it may not fill all regions of the object.
- **4-Connected Method Limitation**: It fails to fill corner pixels, as it only checks the adjacent positions of the current pixel.

##### Scan-Line Algorithm
- **Definition**: The Scan-Line Algorithm is an area filling algorithm used for polygons.
- **Method**: It fills polygons using horizontal lines (scan lines).
- **Process**: The scan line intersects the edges of the polygon, filling the interior pixels between pairs of intersections.
- **Purpose**: Its primary goal is to fill color in the interior of the polygon effectively.

###### Special Cases of Polygon Vertices
- **Case 1**: If both lines intersecting at a vertex lie on the same side of the scan line, they are treated as **two distinct points**.
- **Case 2**: If both lines intersecting at a vertex lie on the opposite side of the scan line, they are treated as **a single point**.
![[{265665BA-E2B7-4BBE-AC9E-88776E99851A}.png|500]]

###### Algorithm of Scan line polygon-fill
- **Find Intersections**: Identify the intersection points of the scan line with the polygon edges.
- **Sort Points**: Sort the intersection points by their x-coordinates in increasing order (from left to right).
- **Pair Points**: Pair the sorted intersection points and fill the color inside the pixel pairs.

Cons
- **Staircase or Jagged Appearance**: The algorithm can produce a staircase-like appearance when converting lines or circles, leading to a visually unappealing output.
- **Unequal Intensity**: There can be inconsistent brightness across different lines, with inclined lines often appearing less bright compared to horizontal and vertical lines.
![[{CFAF0865-5701-4CD5-A73F-B340987B2336}.png]]





## 2.2 2DGeometric Transformations: Basic 2D Geometric Transformations, matrix representations and homogeneous coordinates. Inverse transformations, 2DComposite transformations, other 2D transformations, raster methods for geometric transformations, OpenGL raster tran

### 2 D transformations

#### Linear transformation gallery

**2x2 matrices have simple geometric interpretations** 
**– uniform scale**
**– non-uniform scale**
**– rotation** 
**– shear** 
**– reflection**

##### Scaling
![[{60B10363-A036-4F39-8ABF-84202E1754C6}.png]]
![[{9FFDFA78-B800-4018-8AAD-45CEF2684FA6}.png]]

##### Uniform Scale
![[Pasted image 20240925132800.png]]

![[{BB8C71D1-7E1B-41F1-9D42-4E53EBC67A05}.png]]


##### Non-Uniform Scale
![[{3B8CA9A7-9B76-4F82-A25D-0A74FCCFF28D}.png]]

![[{D370FA15-EB2F-4BD6-9D46-D3A7F273AA47}.png]]

##### Rotation
![[{E17D5E75-E470-47E9-A9B4-C900983E9DAD}.png]]

![[{5B241F28-211A-449E-9363-D003DCAA39CB}.png]]

![[{7A842FEC-2005-4DF0-80FE-E9A351237676}.png]]

###### Rotation in 2D
![[{55A30902-1581-4B85-9069-83B0F1204E10}.png]]

###### Rotating in 2D, matrix notation
![[{076E759E-4AD3-4407-8212-6769B7E27C00}.png]]


##### Shear
![[{5599767C-6CB4-4139-9CC2-DC5A47FD6198}.png]]

![[{C440CD59-168B-4048-813A-6063D3FC07CF}.png]]

##### Reflection
![[{C1873819-FD5B-40CF-ADE6-3DBFEFE7CEFF}.png]]

##### Summary
![[{A6716C3A-1BA8-4AFF-9841-C5F6EE137CA2}.png]]

##### Translation
![[{9C981623-39C7-4F66-A0AA-F79D64FF4043}.png]]

## 2.3  2D viewing: 2D viewing pipeline, OpenGL 2D viewing functions

### World Windows and Viewports
![[{A8775D73-F1AD-43DC-9198-069A4C59DB34}.png]]
- **Definition**: The window and viewport are aligned rectangles defined by the programmer.
- **World Coordinates**: The window represents a section in world coordinates.
- **Viewport**: The viewport is a specific area of the screen where the window's content is displayed.
- **Functionality**: Content within the world window is scaled and shifted to fit the viewport; anything outside this area is clipped and not shown.

#### The mapping from the window to the viewport
![[{B974A794-28A1-43F1-86D1-E2C1B0120651}.png]]
![[{74E8ACC2-9536-4D4D-9164-7ACA4E802CAF}.png]]
#### The Mapping from the Window to the Viewport
- **Distortion**: The figure in the window may need to be stretched to fit the viewport, leading to potential distortion.
- **Mapping Transformation**: This process is known as window-to-viewport mapping or transformation.
- **OpenGL Functionality**: OpenGL simplifies this mapping by automatically transforming each vertex passed via `glVertex2*()` commands, ensuring proper mapping.
- **Clipping**: OpenGL also automatically clips parts of objects that lie outside the world window.
- **Setup**: Proper setup of transformations is all that's needed, as OpenGL handles the rest.
- **2D Drawing**:
  - **World Window**: Set using `gluOrtho2D()`, defined as:
    ```c
    void gluOrtho2D(GLdouble left, GLdouble right, GLdouble bottom, GLdouble top);
    ```
    This sets the window with the lower left corner at `(left, bottom)` and the upper right corner at `(right, top)`.
  - **Viewport**: Set using `glViewport()`, defined as:
    ```c
    void glViewport(GLint x, GLint y, GLint width, GLint height);
    ```
    This sets the viewport with the lower left corner at `(x, y)` and the upper right corner at `(x + width, y + height)`.

#### Zooming and Roaming
- **Zooming In**: Reducing the window size is akin to zooming in on the object with a camera. This causes the contents of the window to be enlarged to fit within the fixed viewport.
- **Zooming Out**: Conversely, increasing the window size resembles zooming out from the object, allowing more of the scene to be displayed at a smaller scale.
- **Effect**: As the window changes size, the portion of the scene within it is scaled accordingly, resulting in a more detailed or broader view of the object, depending on the zoom level.
![[{1E2A2D44-BAE1-4D25-89AF-B758BE3ED81A}.png]]

**The aspect ratio of an image is the ratio of its width to its height.**

#### Automatic setting of the viewport to Preserve Aspect Ratio
![[{2309A917-3236-451F-9815-1239BD7B2F1C}.png]]

##### Example 1
![[{ED5468D7-4639-4AF8-A233-278E0C4222E0}.png]]

##### Example 2
![[{FD94195E-3E80-432E-B587-EAD9006E4A5B}.png]]

##### Resizing the screen window, and the resize event.

- **Function Definition**: `glutReshape(myReshape);`
  - This line specifies the function `myReshape` to be called when a resize event occurs in the OpenGL window.
- **Purpose**: The `myReshape` function handles updates to the viewport and any necessary transformations to adjust the rendering based on the new window dimensions.

# Made By Yashank