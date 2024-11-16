## 1.1 Basics of computer graphics, Application of Computer Graphics, Video Display Devices: Random Scan and Raster Scan displays 

### Basics of computer graphics

#### Need of computer graphics
- **Dynamic Display**: Enables a **computer to visually represent** data and change it over time.
- **Display Technologies**: Can use various technologies like **CRT, LED, or E-Ink**, with the essential factor being the **dynamic** nature of the display.
- **Real-Time Visualization**: Provides **real-time feedback**, allowing users to interact with **changing visual information**.

#### Importance of Dynamic Display
- **Memory Updates**: Visual representation is essential as **memory contents change over time**.
- **Document Revisions**: Documents and other content often undergo **multiple revisions** that need to be reflected visually.
- **State Changes**: Machines **respond to events** by **changing states** repeatedly, and a dynamic display helps in visualizing these changes.

#### Motivation
- **Expanding Art and Entertainment**: **Computer graphics** has broadened the **scope of art and entertainment**, allowing for more creative and imaginative content.
- **Movies**: Films like **Jurassic Park** utilize computer graphics to **push the boundaries of imagination**.
- **Virtual Reality**: Offers a **synthetic reality** created within the computer, providing immersive experiences.
- **Training Simulators**: **Flight simulators** train pilots for extreme conditions, and **surgical simulators** help novice surgeons practice without risk to patients.
- **Engineering Applications**: In fields like **automotive and aerospace**, computer graphics allow for the **quick visualization of newly designed shapes** for faster development.

### Application of Computer Graphics
- **Computer Art**: The use of **computer graphics to create digital artwork**.
- **Computer-Aided Drawing**: Utilizes **software tools** to aid in **technical drawing** and design, often for engineering or architecture.
- **Presentation Graphics**: Enhances **presentations** by creating **visual representations** of data and ideas.
- **Entertainment**: Powers the **visual effects** and **animations** in movies, games, and other media.
- **Education**: Provides **interactive visual aids** and simulations to enhance **learning experiences**.
- **Training**: Simulators and virtual environments for **skill development** without real-world risks.
- **Visualization**: Enables the **graphic representation** of data or concepts to simplify understanding.
- **Image Processing**: Involves the **manipulation and analysis of images** through computational techniques.
- **Machine Drawing**: **Technical drawings** generated through computer software for **mechanical components**.
- **Graphical User Interface (GUI)**: The **visual elements** of an interface that allow users to interact with computers intuitively.
- **Printing Technology**: Leverages computer graphics to **enhance the quality** of printed materials.

### Computer Graphics
- **Computer Graphics** deals with all aspects of **creating images with a computer**.
- It encompasses **Hardware**, which includes the **physical components** like **monitors, graphic cards, and input devices**.
- It involves **Software**, which refers to **graphics programs** and **algorithms** used to **generate and manipulate images**.
- **Applications** of computer graphics extend to various fields like **art, design, simulations, games, and data visualization**.

### Basic Graphics System

![[{EECB62A8-D1D7-404B-8D34-2660CD32CE4D}.png]]

### History of Computer Graphics
#### Computer Graphics: 1950-1960

##### CRT
![[{DC37D297-22ED-4297-8C85-9AEF10B69B71}.png]]
- **CRT (Cathode Ray Tube)** could be used as either a **line-drawing device (calligraphic)** or to **display contents of frame buffer (raster mode)**.

- **Early Development**: Computer graphics date back to the **earliest days of computing** with basic tools such as:
    - **Strip charts**
    - **Pen plotters**
    - **Simple displays** using A/D converters to connect computers to **calligraphic CRTs**.
- **Challenges**:
    - The **cost of refresh** for CRT displays was **too high**.
    - **Computers** were **slow, expensive, and unreliable** during this period.

#### Computer Graphics: 1950-1960
- **Wireframe Graphics**: **Draw only lines** to represent objects, without shading or filling.
- **Sketchpad**: An early computer graphics system allowing **direct interaction** with drawings on a screen, developed by Ivan Sutherland.
- **Display Processors**: Specialized **hardware** designed to handle the rendering of graphics, freeing up the CPU.
- **Storage Tube**: A **non-refresh display** technology where the image remains on the screen until cleared, used in early computer graphics systems.

##### Sketchpad
- **Sketchpad**: **Ivan Sutherland's PhD thesis at MIT**, revolutionizing computer graphics.
- **Recognized the potential** of **man-machine interaction**, allowing users to directly interact with the display.
- **Loop Process**:
    - **Display something** on the screen.
    - **User moves light pen**, interacting with the display.
    - **Computer generates a new display** based on the interaction.
- **Sutherland** also developed many of the **common algorithms** used in modern computer graphics.

##### Display Processor
- **Display Processor (DPU)**: **Special-purpose computer** designed to handle display refresh, reducing load on the host computer.
- **Graphics stored** in a **display list (display file)**, which is maintained by the DPU.
- **Host compiles** the **display list** and sends it to the **DPU** for rendering, allowing more efficient graphics handling.
![[{CFB610FD-ABC6-465B-A80F-4FE4F2563905}.png|500]]

##### Direct View Storage Tube
- **Direct View Storage Tube**: Developed by **Tektronix**, this technology eliminated the need for constant refresh of the display.
- **Standard Interface**: Provided a consistent connection to computers, enabling compatibility with various systems.
- **Standard Software**: Facilitated the use of common software applications, such as **Plot3D** in **Fortran**.
- **Cost-Effective**: Relatively inexpensive compared to other display technologies, making it accessible.
- **Impact on CAD Community**: Paved the way for the use of computer graphics in **Computer-Aided Design (CAD)** applications.

#### Computer Graphics: 1970-1980
- **Raster Graphics**: Emergence of raster graphics as a dominant form of image representation.
- **Beginning of Graphics Standards**: The establishment of standards for graphics, leading to improved interoperability.
- **IFIPS**: International Federation for Information Processing Standards contributed to the development of graphics standards.
- **GKS**: A European initiative that became the ISO **2D standard**, enhancing consistency in graphics programming.
- **Core**: A North American effort focused on **3D graphics** but ultimately failed to become an ISO standard.
- **Workstations and PCs**: The growth of workstations and personal computers facilitated more widespread use of computer graphics.

##### Raster Graphics
- **Image Production**: Raster graphics produce images as an array (the raster) of picture elements (pixels) stored in the frame buffer.
![[{73827A45-D4E6-43F5-86E0-6D4A372E9676}.png]]


- **Transition to Filled Polygons**: This technology allows for the transition from simple lines and wireframe images to complex, filled polygons.
![[{15DDADA0-2FB9-4E2A-8669-619C4765A2D7}.png]]

- **Definition of Raster Graphics**: Raster graphics represent images using a grid of pixels, where each pixel corresponds to a specific color or shade, creating a complete image when viewed as a whole.
- **Pixel Density**: The quality of a raster image is determined by its resolution, measured in pixels per inch (PPI) or dots per inch (DPI), affecting the level of detail and clarity.
- **Common Formats**: Common raster image formats include JPEG, PNG, BMP, and GIF, each serving different purposes in terms of compression, transparency, and color depth.
- **Advantages**: Raster graphics excel in representing complex images like photographs with rich detail and color gradients, making them ideal for digital photography and detailed artwork.
- **Limitations**: Raster images can lose quality when scaled up, leading to pixelation, as enlarging a raster image stretches the existing pixels rather than generating new detail.

##### PCs and Workstations
- **Historical Context**: Workstations and PCs originated from different technological foundations, with workstations being designed for professional and technical applications, while PCs were primarily intended for personal use.
- **Networked Connection**: Early workstations were typically connected in a networked environment, utilizing a client-server model to facilitate resource sharing and collaboration among users.
- **High-Level Interactivity**: Workstations offered a higher degree of interactivity, allowing users to engage with graphics-intensive applications and perform complex computations in real time.
- **Frame Buffer Integration**: Early PCs incorporated a frame buffer into user memory, enabling direct manipulation of graphics data and simplifying the process of image creation and modification.
- **User-Friendly Graphics**: The ability to easily change contents within the frame buffer allowed users to create and modify images dynamically, paving the way for the development of graphic design and multimedia applications.

#### Computer Graphics: 1980-1990
**Realism comes to computer graphics**
- **Special Purpose Hardware**: Development of dedicated hardware designed specifically for rendering graphics, enabling faster and more complex visual representations.
- **Silicon Graphics Geometry Engine**: Introduction of advanced graphics systems, such as Silicon Graphics' geometry engine, which facilitated high-performance rendering of 3D graphics.
- **VLSI Implementation**: Utilization of Very Large Scale Integration (VLSI) technology to create efficient graphics pipelines, enhancing the speed and quality of image rendering.
- **Industry-Based Standards**: Establishment of standards like PHIGS (Programmer's Hierarchical Interactive Graphics System) to ensure compatibility and interoperability among different graphics systems.
- **RenderMan**: Introduction of RenderMan, a powerful rendering software developed by Pixar, which allowed for high-quality photorealistic image generation and set new benchmarks in the industry.
- **Networked Graphics**: The advent of networked graphics systems like the X Window System, enabling remote graphical interfaces and collaborative applications across multiple machines.
- **Human-Computer Interface (HCI)**: Advancements in HCI design, improving user interaction with computer graphics through intuitive interfaces and interactive applications, enhancing the overall user experience.

#### Computer Graphics: 1990-2000
- **OpenGL API**: Development of the Open Graphics Library (OpenGL) as a standard API for rendering 2D and 3D graphics, facilitating cross-platform compatibility and widespread adoption in various applications.
- **Feature-Length Movies**: Achievements in completely computer-generated feature-length films, exemplified by Pixar's _Toy Story_, which marked a significant milestone in the animation industry and showcased the potential of computer graphics.
- **New Hardware Capabilities**: Advancements in hardware technology allowed for more sophisticated graphics processing, including enhanced rendering speeds and the ability to handle complex scenes.
- **Texture Mapping**: Introduction of texture mapping techniques, allowing for the application of images onto 3D surfaces to create realistic textures and details in computer graphics.
- **Blending**: Development of blending techniques that enable the combination of multiple image layers, improving realism in graphics by simulating effects like transparency and light diffusion.
- **Accumulation Buffers**: Utilization of accumulation buffers in rendering processes, allowing for the accumulation of multiple frames to achieve effects such as motion blur and depth of field.
- **Stencil Buffers**: Implementation of stencil buffers, enabling more complex image compositions and masking effects, enhancing the visual fidelity of rendered scenes.

#### Computer Graphics: 2000-2010
- **Photorealism**: Advancements in rendering techniques that enabled the creation of images indistinguishable from real-life photographs, pushing the boundaries of visual fidelity in computer graphics.
- **Graphics Cards (GPU)**: The dominance of dedicated graphics processing units (GPUs) in PCs, with companies like Nvidia and ATI leading the market, significantly improving graphics rendering capabilities and performance.
- **Game Consoles**: The influence of gaming consoles (e.g., Wii, Kinect) on the computer graphics market, shaping trends and driving innovations in graphics technology to enhance user experience and gameplay.
- **Industry Software**: Widespread adoption of specialized graphics software in the movie industry, such as Maya and Lightwave, which became industry standards for 3D modeling, animation, and visual effects production.
- **Programmable Pipelines**: Introduction of programmable graphics pipelines, allowing developers to write custom shaders and effects, leading to greater flexibility and creativity in graphics programming and rendering techniques.

#### Computer Graphics: 2010-
- **Mobile Computing**: The rise of mobile devices, especially smartphones like the iPhone, revolutionized the way graphics are rendered and displayed, making high-quality graphics accessible on handheld devices.
- **Cloud Computing**: Platforms like Amazon Web Services (AWS) provided scalable resources for graphics processing, enabling complex graphic applications to run in the cloud, facilitating collaboration and accessibility.
- **Virtual Reality (VR)**: The emergence of VR technologies, such as Oculus Rift, pushed advancements in graphics to create immersive environments that simulate real-world experiences for gaming, training, and education.
- **Artificial Intelligence (AI)**: Integration of AI in computer graphics for improved rendering techniques, automated asset generation, and enhanced realism in simulations and animations.
- **Big Data/Deep Learning**: Utilization of big data and deep learning algorithms to analyze and generate graphics, leading to breakthroughs in procedural content generation and more realistic visual effects.
- **Autonomous Vehicles**: Development of computer graphics in the context of self-driving technology, exemplified by innovations like Google Car, which relies on sophisticated graphics processing for navigation and obstacle detection.


### Graphics Pipeline
![[{070B57A1-2C44-45FA-A743-41ACDECD61BF}.png]]

#### Modeling
- **Polygons**: Fundamental building blocks in 3D graphics, typically defined by vertices, edges, and faces. They serve as the primary representation for 3D objects in various graphics applications.
- **Constructive Solid Geometry (CSG)**: A modeling technique that combines simple solids using Boolean operations such as **union**, **intersection**, and **difference** to create complex shapes. CSG is useful for CAD applications and object modeling.
- **Parametric Surfaces**: Represented mathematically by functions like f(u)=x(u,v),y(u,v),z(u,v)f(u) = x(u,v), y(u,v), z(u,v)f(u)=x(u,v),y(u,v),z(u,v), allowing for the creation of complex shapes defined by parameters. This technique is widely used in computer-aided design and animation.
- **Implicit Surfaces**: Defined by the locus of solutions of equations like f(x,y,z)=0f(x,y,z) = 0f(x,y,z)=0. These surfaces are useful in modeling organic shapes and can create smooth, continuous surfaces without explicit polygonal representation.
- **Subdivision Surfaces**: A technique for creating smooth surfaces by recursively refining polygonal meshes. This method is popular in animation and film, as it allows for high-quality surface representations from coarse initial models.
- **Particle Systems**: Used to simulate fuzzy phenomena such as fire, smoke, and explosions. Each particle can represent a small part of a complex effect, allowing for realistic motion and behavior in animations.
- **Volumes**: Representation of 3D space filled with matter, allowing for the modeling of complex structures in fields such as medical imaging and scientific visualization. Volume rendering techniques can visualize data in ways that traditional polygonal representations cannot.

#### Animation
- **Scripted**: Animation created using programming or scripting languages to control movements and behaviors dynamically.
- **Key-frame Interpolation**: Technique where key frames are defined at significant points in time, and intermediate frames are generated through interpolation to create smooth motion.
- **Inverse Kinematics**: A method for calculating the joint movements needed to achieve a desired position of an object (like a character's limb); essential for realistic character animation.
- **Dynamics**: Simulation of forces and physical interactions to create realistic movements and behaviors in animations, often used for objects responding to gravity, collisions, and other forces.

#### Rendering
- **Definition**: Rendering, or image synthesis, is the process of generating a photorealistic image from a 2D or 3D model using computer programs.
- **Techniques**: Includes various techniques such as rasterization, ray tracing, and scanline rendering to convert models into images.
- **Lighting Models**: Utilizes different lighting models (e.g., Phong, Blinn-Phong) to simulate how light interacts with surfaces for realistic appearances.
- **Shading**: Involves applying colors and textures to the surfaces of models, determining how they appear under various lighting conditions.
- **Post-processing**: Enhancements like anti-aliasing, depth of field, and motion blur applied after rendering to improve the final image quality.
![[{AFEDF884-9264-4CD9-9B3E-7309A044D27D}.png]]

#### Image-Based Rendering

![[{4C6CFC76-9B58-4EF6-B417-78789FA5F8E1}.png]]

##### Image Based Rendering (IBR) Pros and Cons
- **Pros**:
    - **Modest Computation**: Requires less computational power compared to classical computer graphics methods.
    - **Cost Independence**: Rendering cost does not depend on scene complexity, making it efficient for various applications.
    - **Imagery Flexibility**: Can generate images from both real and virtual scenes, providing versatility in visualization.

- **Cons**:
    - **Static Scene Geometry**: Limited to static geometries, which restricts dynamic scene representation.
    - **Fixed Lighting**: Assumes fixed lighting conditions, which may not accurately reflect changes in real environments.
    - **Fixed Viewpoint**: The look-from or look-at point is fixed, limiting the perspective and interactivity of the viewer.

##### Appearance Modeling
![[{6922E98D-13D2-49F6-9F61-4EF965584B0A}.png]]

-  Appearance models in computer graphics and vision try to answer these questions
- **Sky Color**: Investigates why the sky appears blue, often due to Rayleigh scattering of sunlight.
- **Surface Wetness**: Explores why wet sand appears darker than dry sand, related to changes in light absorption and reflection.
- **Iridescence**: Analyzes why iridescent surfaces (like CD-ROMs and butterfly wings) show different colors from different viewing angles, tied to structural coloration.
- **Aging Effects**: Examines why old and weathered surfaces have distinct appearances compared to new ones, often due to texture changes and material degradation.
- **Rust Appearance**: Studies the differences in appearance between rusted and un-rusted surfaces, which involve changes in color, texture, and reflectivity.

#### Real Time Rendering

- **Definition**: Real-time rendering prioritizes quick image display over photo-realism; techniques that take a long time to render are acceptable for non-interactive applications.
- **Applications**: Common in games, flight simulators, virtual reality, and augmented reality where quick visual feedback is essential.

##### Characteristics of Real-Time Rendering

- **Rendering Speed**: Measured in Frames Per Second (fps); a frame rate of at least 15 fps is considered real-time, with 30 fps being a minimum for a smooth experience.
- **Immersion**: A rate of about 72 fps enhances user immersion and interaction, minimizing distractions.

##### Achieving Real-Time Speeds

- **Pre-Processing**: Simplifying graphics models, using textures instead of polygons, and optimizing data for faster rendering.
- **Hardware Acceleration**: Utilizing dedicated graphics hardware for improved performance.
    - **Graphics Cards**: Innovations by companies like ATI and Nvidia have transformed real-time graphics; the 3Dfx Voodoo 1 was pivotal in this evolution.
    - **Graphics Processing Unit (GPU)**: Offers faster rendering than CPUs and greater programmability, enabling more complex graphics calculations in real time.

### Raster Scan
![[Pasted image 20240925005146.png]]
#### Types of Scanning or travelling of beam in Raster Scan
- **Interlaced Scanning**
    - Each horizontal line of the screen is traced from top to bottom.
    - Results in potential fading of displayed objects as it alternates between odd and even lines, creating a flickering effect.
- **Non-Interlaced Scanning**:
    - Odd-numbered lines are traced first by the electron beam.
    - In the next pass, even-numbered lines are scanned, providing a more stable image without the flicker seen in interlaced scanning.

#### Scan Converting a Point
- Each pixel on a graphics display represents a region, not a single mathematical point.
- This region can theoretically contain an infinite number of points.
- **Scan-Converting a Point**: Involves illuminating the pixel that contains the point, effectively converting the mathematical point into a visual representation on the display.
![[{5060B188-824B-46DF-ABCB-0B4E79151A99}.png]]

#### DDA
-  Digital Differential Analyzer A.K.A. Incremental method
- equation of the straight line :- **y = mx + c** 
-  Here, m is the slope of (x1, y1) and (x2, y2). 
- m = (y2 – y1)/ (x2 – x1)

![[{DC7D4AE6-9861-4ACE-A353-84456BDE67EC}.png]]
![[{D9F981D0-068C-4EE5-966E-679F0288B4F4}.png]]

##### Example: A line has a starting point (1,7) and ending point (11,17). Apply the Digital Differential Analyzer algorithm to plot a line.
![[{939277CB-BC41-46FB-BD25-D04BFD8E84E1}.png]]
![[{7D6C0E26-8886-4659-A12A-1456486FA0DF}.png]]

##### Advantages of Digital Differential Analyzer
- **Simplicity**: The DDA algorithm is straightforward to implement, making it accessible for developers and suitable for various applications in computer graphics.
- **Speed**: It is faster than using the direct line equation, as it relies on incremental calculations rather than computing the line equation for every pixel.
- **Limitations**: The algorithm does not employ multiplication, which can simplify calculations but may also limit precision in certain scenarios.
- **Point Overflow**: DDA effectively manages point overflow, allowing it to track changes in location accurately, ensuring smooth transitions between points in graphical rendering.

##### Disadvantages of Digital Differential Analyzer
- **Time-Consuming Arithmetic**: The floating-point arithmetic used in the DDA can be slow, leading to longer processing times for rendering lines.
- **Round-Off Errors**: The method of rounding off calculations can introduce additional time consumption and may affect the accuracy of the rendered line.
- **Position Accuracy**: There are instances where the computed position of the point may not be accurate, leading to potential visual artifacts in the rendered graphics.


## 1.2 Introduction to Graphics software OpenGL ,coordinate reference frames, specifying two-dimensional world coordinate reference frames in OpenGL, OpenGL point functions, OpenGL line functions, point attributes, line attributes, curve attributes, OpenGL point attribute functions, OpenGL line attribute functions, Line drawing algorithms(DDA, Bresenham’s), circle generation algorithms (Bresenham’s).

### OpenGL
- **Overview**:
    - OpenGL is a **cross-language** and **cross-platform** (platform-independent) API that enables developers to render 2D and 3D vector graphics using polygons to represent images.
- **Hardware-Based Design**:
    - The OpenGL API is primarily designed to operate with hardware, allowing for efficient rendering through the Graphics Processing Unit (GPU).

#### Design
- **Function Set**:
    - OpenGL is defined as a set of functions that can be called by client programs to perform various graphics operations. This modular design allows for flexibility and extensibility in graphics programming.

#### Development
- **Evolving API**:
    - OpenGL is continuously evolving, with the Khronos Group regularly releasing new versions that introduce extended features and improvements over previous versions.
    - GPU vendors may provide additional functionality through extensions, allowing for enhanced performance and capabilities specific to their hardware.

#### Associated Libraries
- **Complexity Management**:
    - OpenGL can be complex to use directly, so various utility libraries have been developed to simplify the process:
        - **OpenGL Utility Toolkit (GLUT)**: Originally provided functionality for window management and handling user input.
        - **FreeGLUT**: An updated version of GLUT that offers additional features and fixes.
        - **GLEE (OpenGL Extension Engine)**: Helps manage OpenGL extensions and simplifies their usage.
        - **GLEW (OpenGL Extension Wrangler Library)**: A cross-platform C/C++ library that manages OpenGL extensions efficiently.
        - **glbinding**: A modern C++ binding for OpenGL that provides a safer and more convenient API.

#### Implementation
- **Mesa 3D**:
    - Mesa 3D is an open-source implementation of OpenGL that supports software rendering and can leverage hardware acceleration on platforms such as BSD and Linux.
    - It provides a platform for testing and developing OpenGL applications without requiring specific hardware.

This structured approach allows developers to harness the full power of graphics rendering while maintaining portability across different platforms and languages.

### OpenGL Rendering Pipeline
#### COLOR
![[{8B12D73D-728F-437B-9E67-95ADF0CE60AA}.png]]

#### The such function calls are formatted.
![[{B8D37E11-9F97-456C-B741-689B0F1A86E6}.png]]

#### Command suffixes and argument data types.
![[{24A622A7-C3DB-4ADF-8C2D-2E3613BF11B9}.png]]

#### The OpenGL “State”

##### OpenGL State Management
- **State Variables**: 
  - OpenGL maintains numerous state variables that affect rendering behavior, including:
    - **Current Point Size**: Determines the size of points drawn.
    - **Current Drawing Color**: The color used for drawing shapes and objects.
    - **Current Background Color**: The color that fills the background of the window.

- **State Persistence**: 
  - The value of each state variable remains active until it is explicitly changed by the programmer.

##### Setting Colors
- **Color Functions**: 
  - Colors in OpenGL can be set using the `glColor3f` function, where the parameters represent the red, green, and blue components of the color. Each component ranges from **0.0** to **1.0**.

  - **Examples**:
    - `glColor3f(1.0, 0.0, 0.0);` // Sets the drawing color to **red**.
    - `glColor3f(0.0, 0.0, 0.0);` // Sets the drawing color to **black**.
    - `glColor3f(1.0, 1.0, 1.0);` // Sets the drawing color to **white**.
    - `glColor3f(1.0, 1.0, 0.0);` // Sets the drawing color to **yellow**.

##### Background Color
- **Setting Background Color**: 
  - The background color can be defined using the `glClearColor` function, which specifies the RGBA (Red, Green, Blue, Alpha) values:
    - `glClearColor(red, green, blue, alpha);`
    - The **alpha** parameter controls transparency:
      - **Fully transparent**: A = 0.0
      - **Fully opaque**: A = 1.0

##### Clearing the Window
- **Clearing the Color Buffer**: 
  - To clear the entire window and fill it with the background color, use:
    - `glClear(GL_COLOR_BUFFER_BIT);`
  - Here, `GL_COLOR_BUFFER_BIT` is a constant predefined in OpenGL, indicating that the color buffer should be cleared.

This state management system allows for flexible and dynamic graphics rendering in OpenGL applications, enabling developers to create visually appealing scenes and effects.

#### Indexed Color

![[{3350CEF0-8553-4178-93D0-C1F1F75F8A4D}.png]]

- **Pixel Representation**: 
  - Each pixel in an indexed color system is represented by an integer value (index) ranging from **0** to **(2^k) - 1**, where **k** indicates the number of bits used for the index.

- **Color Component Precision**: 
  - If each color component (red, green, blue) is defined with a precision of **m bits**, it allows for:
    - **2^m** different shades of red,
    - **2^m** different shades of green,
    - **2^m** different shades of blue.

- **Total Color Combinations**: 
  - This results in a potential total of **2^(3m)** distinct colors that can be represented on the display.

- **Frame Buffer Limitation**: 
  - However, the frame buffer can only specify **2^k** colors from this larger palette, meaning that while many colors may be available, only a limited subset can be utilized at any given time in the display output. 

This method is particularly efficient for applications where a limited color palette is sufficient, such as in certain types of images, animations, or applications requiring reduced memory usage.

#### Setting Point Size in OpenGL

- Use the function:
  
  ```c
  glPointSize(2.0);
  ```

- **Purpose**: This sets the rendered point size to **2 pixels wide**. 

- **Usage**: Useful for enhancing visibility of points in graphics applications.

#### The Orthographic View

- **Definition**: The simplest and default view in OpenGL.
- **Characteristics**:
  - Objects retain their size regardless of their distance from the camera.
  - Parallel lines remain parallel, without convergence.
- **Usage**: Ideal for 2D graphics and technical drawings where scale and dimensions are crucial.

![[{067877BF-899C-49EE-A985-C1ED50AD25B6}.png]]

#### Two-Dimensional Viewing
![[{4ED603A5-9F9C-48C2-A855-0F1B76B34E0A}.png]]

### OpenGL Utility Toolkit (GLUT)

- **Purpose**: A library of functions designed to provide a simple interface between applications and the underlying system.
- **Implementation**: 
  - Abstracts away details specific to the windowing or operating system.
  - Ensures that the complexities of the system are hidden from the user.
- **Benefit**: Simplifies the development process by allowing developers to focus on graphics programming without worrying about system-specific intricacies.

### Establishing the Coordinate System in OpenGL

- **glVertex**: Defines a vertex in 2D or 3D space.
- **glVertex3**: Specifies a vertex using three coordinates (x, y, z).
- **glVertex3f**: Defines a vertex using three coordinates of type `GLfloat` (e.g., `glVertex3f(1.0f, 2.0f, 3.0f)`).
- **glVertex3fv**: Specifies a vertex using three `GLfloat` coordinates contained within a vector (e.g., `GLfloat coords[] = {1.0f, 2.0f, 3.0f}; glVertex3fv(coords);`).
- **Alternative**: `glVertex3fl` allows defining a vertex using a list of arguments instead of a vector.

### Coordinate Reference Frames

- **Coordinate Systems**: OpenGL uses a right-handed coordinate system where:
    - The **X-axis** extends horizontally.
    - The **Y-axis** extends vertically.
    - The **Z-axis** extends out of the screen towards the viewer.
- **World Coordinate Reference Frames**: In OpenGL, world coordinates define the position of objects in a 2D or 3D space. You can specify two-dimensional world coordinate frames by setting the projection and modelview matrices.
### Specifying Two-Dimensional World Coordinate Reference Frames in OpenGL

- **Setting Up the View**: Use functions like `glOrtho()` to create an orthographic projection, or `gluPerspective()` for perspective projections, to define the visible region in world coordinates.
- **Transformations**: Apply translation, rotation, and scaling transformations using `glTranslatef()`, `glRotatef()`, and `glScalef()` to position objects within the world coordinate frame.

### OpenGL Point Functions
- **Point Functions**: OpenGL provides functions like `glBegin(GL_POINTS)` and `glEnd()` to define points in the rendering pipeline. Points can be specified using `glVertex2f(x, y)`.

### OpenGL Line Functions
- **Line Functions**: To draw lines, OpenGL uses `glBegin(GL_LINES)` or `glBegin(GL_LINE_STRIP)` along with vertex specification functions like `glVertex2f(x, y)` to define endpoints of the lines.

### Point Attributes
- **Point Attributes**: Attributes like size and color can be set using functions such as `glPointSize(size)` for point size and `glColor3f(r, g, b)` for color.

### Line Attributes
- **Line Attributes**: Line width can be controlled using `glLineWidth(width)` to define the thickness of the drawn lines.

### Curve Attributes
- **Curve Attributes**: Curves can be represented using various methods, including using a series of line segments. Attributes like color and thickness can be applied similarly to line attributes.

### OpenGL Point Attribute Functions
- **Point Attribute Functions**: Utilize functions such as `glPointSize()` to define the size of points and `glColor3f()` to specify their color.

### OpenGL Line Attribute Functions
- **Line Attribute Functions**: Use `glLineWidth()` to set the width of lines and `glColor3f()` to set their color attributes.

### Line Drawing Algorithms

![[{2611DD85-CF57-4574-8F0C-61196D561818}.png]]


#### Digital Differential Analyzer (DDA)
DDA (Digital Differential Analyzer) is a line drawing algorithm used in computer graphics to generate a line segment between two specified endpoints. It is a simple and efficient algorithm that works by using the incremental difference between the x-coordinates and y-coordinates of the two endpoints to plot the line.

Given the starting and ending coordinates of a line,
DDA Algorithm attempts to generate the points between the starting and ending coordinates.

##### Procedure
Given-
- Starting coordinates = (X0, Y0)
- Ending coordinates = (Xn, Yn)

The points generation using DDA Algorithm involves the following steps-


###### Step 1
![[{8F8E757A-80DD-48BB-A284-6BB4ED4F42F1}.png]]

###### Step 2
![[{5FDE058C-22E9-4212-91DA-948F61B1A389}.png]]

###### Step 3
![[{5FD6E9B9-8ABA-4C9F-8158-57FFC34D1FD4}.png]]

###### Step 4
**Keep repeating Step-03 until the end point is reached or the number of generated new points (including the starting and ending points) equals to the steps count.**

##### Example

**Calculate the points between the starting point (5, 6) and ending point (13, 10).**
![[{00C0BB7F-D1D5-41DA-875E-13B04F85A1DF}.png]]

###### Step 1
![[{6F6FDBA7-6A11-43C7-9BFE-5EE298775ED7}.png]]

###### Step 2
![[{82A97B3C-0D23-445E-B8A6-B498D7A57301}.png]]

###### Step 3
![[{6DBFFFC1-84D9-4053-AAC1-3EC493EEB2E8}.png]]

##### Advantages of DDA Algorithm-

The advantages of DDA Algorithm are-

- It is a simple algorithm.
- It is easy to implement.
- It avoids using the multiplication operation which is costly in terms of time complexity.

##### Disadvantages of DDA Algorithm-

The disadvantages of DDA Algorithm are-

- There is an extra overhead of using round off( ) function.
- Using round off( ) function increases time complexity of the algorithm.
- Resulted lines are not smooth because of round off( ) function.
- The points generated by this algorithm are not accurate.


#### Bresenham's line algorithm
**• It is a line drawing algorithm that determines the points of an n- dimensional raster that should be selected in order to form a close approximation to a straight line between two points.**

##### Procedure
![[{C84CB267-9E4A-4A6C-A5A1-C5F23BDFD860}.png]]

###### Step 1
![[{3B7DD74B-1F25-48CE-ACC2-B2367C72B6E3}.png]]

###### Step 2
![[{3A235D10-8C0C-4C35-888E-4FDB13A88EBD}.png]]

###### Step 3
![[{D2B952F2-A2F1-4D0F-A958-2CFD00C99D1C}.png]]

###### Step 4
**Keep repeating Step-03 until the end point is reached or number of iterations equals to (ΔX-1) times.**

##### Example

**Calculate the points between the starting coordinates (9, 18) and ending coordinates (14, 22).**
![[{0CC0349D-0C95-4ADF-AAD6-8A3FC4394FC3}.png]]

###### Step 1
![[{DFCC9C5F-DF02-4A9C-A752-E0E098B08861}.png]]

###### Step 2
![[{17657649-DD92-4471-B773-D0366413AA64}.png]]

###### Step 3
![[{407D7E36-4406-41DF-A2B7-23EE0F07EEEB}.png]]


##### Advantages of Bresenham Line Drawing Algorithm-

The advantages of Bresenham Line Drawing Algorithm are-
- It is easy to implement.
- It is fast and incremental.
- It executes fast but less faster than DDA Algorithm.
- The points generated by this algorithm are more accurate than DDA Algorithm.
- It uses fixed points only.

##### Disadvantages of Bresenham Line Drawing Algorithm-

The disadvantages of Bresenham Line Drawing Algorithm are-
- Though it improves the accuracy of generated points but still the resulted line is not smooth.
- This algorithm is for the basic line drawing.
- It can not handle diminishing jaggies.


### Circle Generation Algorithms

#### Bresenham Circle Drawing Algorithm
![[{9ED497CD-47EA-4F9E-A410-268E947DBB02}.png]]

##### Procedure
![[{349BE019-2ED4-4F31-A336-AF623EC903D9}.png]]

###### Step 1
![[{36D86301-5FBB-4F2E-A1DF-35D6A5DCE799}.png]]

###### Step 2
![[{E6A114F7-A846-4DA0-B0F6-6219C05CE7CC}.png]]

###### Step 3
![[{03AD65F8-70AA-4BC1-884F-D240C41ACA40}.png]]

###### Step 4
![[{7506EF9A-EA0C-4220-860A-A42E9ADC3015}.png]]

###### Step 5
![[{AD4AABE7-7C3F-4C62-AB88-446D90DD3AF0}.png]]

###### Step 6
![[{15C780E7-B168-4B22-977B-33666C8A1373}.png]]

##### Example
**Given the centre point coordinates (0, 0) and radius as 8, generate all the points to form a circle.**
![[{EC77ED00-7A72-4AF8-BF0D-DC3CE308151E}.png]]

###### Step 1
![[{FB86A916-36CE-47B8-863C-A9984E5B724D}.png]]

###### Step 2
![[{2EA3951A-9CA7-4450-A5C4-36EB5B50272F}.png]]

###### Step 3
![[{DD02AA76-B8FA-494A-8990-EB3FB692FCC7}.png]]

###### Step 4
![[{78E7E366-CB45-4E74-9776-31448F8A4BC4}.png]]

###### Step 5
![[{0463A77C-A12F-47DE-BB90-D9DA730BD6AE}.png]]
![[{14E6CC38-F003-4509-9317-107BCF91AA00}.png]]
![[{3B72A713-CC49-4494-9669-FB8B4B767723}.png]]

##### Advantages of Bresenham Circle Drawing Algorithm

The advantages of Bresenham Circle Drawing Algorithm are-
- The entire algorithm is based on the simple equation of circle X2 + Y2 = R2.
- It is easy to implement.

##### Disadvantages of Bresenham Circle Drawing Algorithm-

The disadvantages of Bresenham Circle Drawing Algorithm are-
- Like Mid Point Algorithm, accuracy of the generating points is an issue in this algorithm.
- This algorithm suffers when used to generate complex and high graphical images.
- There is no significant enhancement with respect to performance.

### Line Drawing using moveto() and lineto()

- **moveto(x, y)**: Sets the current position (CP) to the coordinates (x, y).
- **lineto(x, y)**: Draws a line from the current position (CP) to (x, y), then updates the current position to (x, y).
- **Example**: To draw a line from (x1, y1) to (x2, y2), use:
  ```c
  moveto(x1, y1);
  lineto(x2, y2);
  ```
- **Polyline**: For a series of points  (x0, y0), (x1, y1)... (xn-1}, yn-1}) iterate through the points, using `moveto` and `lineto` for each:
  ```c
  GLintPoint CP; // Global current position
  ```

### Mouse interaction

- **Function Prototype**: Define the mouse event handler with the following prototype:
  ```c
  void myMouse(int button, int state, int x, int y);
  ```
- **Parameters**:
  - **button**: Indicates which mouse button was pressed or released (values can be `GLUT_LEFT_BUTTON`, `GLUT_MIDDLE_BUTTON`, or `GLUT_RIGHT_BUTTON`).
  - **state**: Represents the state of the button (either `GLUT_DOWN` or `GLUT_UP`).
  - **x**: The x-coordinate of the mouse pointer when the event occurred.
  - **y**: The y-coordinate of the mouse pointer when the event occurred.
- **Event Handling**: When a mouse event occurs, the system calls `myMouse()` and provides the respective values for these parameters.

# Made By Yashank