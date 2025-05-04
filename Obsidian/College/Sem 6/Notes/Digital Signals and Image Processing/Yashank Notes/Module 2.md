
# Chapter 2: Fundamentals of Digital Image and Spatial Domain Enhancement

## Chapter Outline

### 2.1 Digital Image Fundamentals

- Digital image Representation
- Elements of digital image processing systems
- Sampling and quantization
- Basic relationships between pixels
- Mathematical operations on images

### 2.2 Spatial Domain Enhancement Techniques

- Point processing
- Neighborhood processing
- Spatial domain filtering
- Zooming

### 2.3 Spatial Enhancement: Global Processing

- Histogram Equalization

### Self-Learning Topic

- Histogram specification

---

## 2.1 Digital Image Fundamentals

### What is Digital Image Processing (DIP)?

*[Insert Image: What is Digital Image Processing text - From Page 2]*

- **Digital Image Processing (DIP)** is a field that focuses on using computers to manipulate and analyze digital images.
- **Two Major Tasks:**
    1.  **Improvement of pictorial information for human interpretation:** Making images clearer, enhancing features, or removing noise so humans can understand them better.
        - *Example:* Enhancing contrast in an X-ray image to help a radiologist spot anomalies.
    2.  **Processing of image data for storage, transmission, and representation for autonomous machine perception:** Preparing images for efficient handling or for use by automated systems like robots or AI.
        - *Example:* Compressing an image to send it over the internet, or segmenting an image to allow a self-driving car to identify obstacles.
- **Relationship to Other Fields:** DIP is closely related to, and sometimes overlaps with, fields like **Image Analysis** (extracting measurements and quantitative information from images) and **Computer Vision** (building systems that can "see" and interpret images like humans). There's often debate about the exact boundaries.

### Light and Image Formation

*[Insert Image: Light properties and formula - From Page 3]*

- Images are typically formed by sensing electromagnetic radiation, most commonly **visible light**.
- **Nature of Light:**
    - Light consists of particles called **photons**.
    - Light also behaves as **waves**.
- **Fundamental Properties of Light Waves:**
    - **Amplitude:** Related to the intensity or brightness of the light.
    - **Wavelength ($\lambda$):** The distance between successive crests of the wave. Determines the perceived color (for visible light) or type of electromagnetic radiation.
    - **Frequency ($f$):** The number of waves passing a point per unit time. It is the inverse of the wavelength.
- **Relationship:** Wavelength and frequency are related by the speed of light ($c$):
  $$
  \lambda = \frac{c}{f}
  $$
  Where $c$ = speed of light $\approx 299,792,458$ m/s in a vacuum.

### Key Stages in Digital Image Processing

*[Insert Image: Key Stages Diagram (overview) - From Page 4]*

- **Concept Diagram:** Digital Image Processing often involves a sequence of steps, although not all steps are required for every application. The diagram shows typical stages and their relationships.
- **Visualization:** Imagine a pipeline where an image potentially goes through these stages:
    1.  **Problem Domain:** What is the source of the data? (e.g., satellite, microscope, camera).
    2.  **Image Acquisition:** Capturing the image using a sensor (like a camera) and digitizing it. This is the first step in any DIP workflow.
        *[Insert Image: Image Acquisition Illustration - From Page 5]*
    3.  **Image Enhancement:** *Subjective* process. Manipulating an image to make it visually more appealing or suitable for analysis by humans or machines. Doesn't necessarily remove errors, might just highlight features. (e.g., increasing contrast).
        *[Insert Image: Image Enhancement Example (grains) - From Page 6]*
    4.  **Image Restoration:** *Objective* process. Attempting to improve an image by removing or reducing known degradations (like blur, noise) using mathematical models of the degradation.
        *[Insert Image: Image Restoration Example (moon landing) - From Page 7]*
    5.  **Morphological Processing:** Deals with tools for extracting image components that are useful in the representation and description of shape. Often used for pre-processing or post-processing (e.g., boundary extraction, noise removal, skeletonization).
        *[Insert Image: Morphological Processing Example (fingerprint) - From Page 8]*
    6.  **Segmentation:** Partitioning an image into its constituent parts or objects. Finding regions of interest. This is a critical and often challenging step before object recognition.
        *[Insert Image: Segmentation Example (characters) - From Page 9]*
    7.  **Object Recognition:** Assigning a label (e.g., "car", "person", "tumor") to an object based on its descriptors obtained from the representation stage.
        *[Insert Image: Object Recognition Example (iris data) - From Page 10]*
    8.  **Representation & Description:** Following segmentation, converting the segmented regions (e.g., pixels belonging to an object) into a form suitable for computer processing.
        - **Representation:** How the data is organized (e.g., boundary points, region).
        - **Description:** Extracting features that result in quantitative information (e.g., size, shape, texture).
        *[Insert Image: Representation & Description Example (boundary) - From Page 11]*
    9.  **Image Compression:** Reducing the amount of data required to store or transmit an image. Essential for applications like web browsing, medical imaging archives, etc.
        *[Insert Image: Image Compression Example (WinZip showing file sizes) - From Page 12]*
    10. **Colour Image Processing:** Techniques specifically for dealing with color images (e.g., color modeling, pseudo-coloring).
        *[Insert Image: Colour Image Processing Example - From Page 13]*

- **Interconnections:** The output of one stage is generally the input to the next, but feedback loops and skipping stages are common. Colour Processing and Compression can often be considered parallel or supporting processes.

### Digital Image Representation

- A digital image is represented as a 2D array (matrix) of numbers, where each number represents the intensity or color at a specific location (pixel).
- **Digitization Process:** Converting a continuous real-world scene into a digital image involves two main steps:
    1.  **Sampling:** Discretizing the spatial coordinates (x, y). Determines the **spatial resolution** (number of pixels).
    2.  **Quantization:** Discretizing the intensity/amplitude values. Determines the **intensity resolution** or **bit depth** (number of distinct colors/gray levels).

#### Digital Image Types

1.  **Intensity Image (Monochrome / Grayscale):**
    - Each pixel corresponds to a single value representing light intensity (brightness).
    - Normally represented in grayscale (levels of gray from black to white).
    - *Example:* Standard black and white photographs, medical X-rays.
    *[Insert Image: Intensity Image Example (bacteria with zoomed grid) - From Page 14]*

2.  **RGB Image (Color):**
    - Each pixel contains a vector of values, typically representing **Red**, **Green**, and **Blue** components.
    - Combining these three primary colors allows for representation of a wide spectrum of colors.
    - *Example:* Color photographs from digital cameras.
    *[Insert Image: RGB Image Example (tree with zoomed grid) - From Page 15]*

3.  **Binary Image (Black and White):**
    - Each pixel contains only one bit.
    - Typically, `1` represents white (or foreground) and `0` represents black (or background).
    - Often the result of thresholding.
    - *Example:* Scanned documents, silhouette outlines.
    *[Insert Image: Binary Image Example (circuit with zoomed grid) - From Page 16]*

#### Effect of Quantization Levels (Intensity Resolution)

- The number of discrete levels used to represent intensity significantly impacts image appearance. This is determined by the **bit depth** ($k$). The number of levels is $L = 2^k$.
- Common bit depth is 8 bits/pixel ($L = 2^8 = 256$ gray levels).
- Reducing the number of quantization levels:
    - Decreases the file size.
    - Can lead to **false contouring**: visible artificial edges or bands appearing in areas of smooth intensity transition, as different intensities are forced into the same quantization level.
    *[Insert Image: Quantization Levels 256, 128, 64, 32 - From Page 17]*
    *[Insert Image: Quantization Levels 16, 8, 4, 2 (showing false contouring) - From Page 18]*
- **Observation:** False contouring becomes noticeable around 16 levels and is very prominent at 4 or 2 levels.

#### Selecting Suitable Size and Pixel Depth

*[Insert Image: Subjectivity of Image Detail (Lena, Cameraman, Crowd) - From Page 19]*

- The definition of a "suitable" image size (spatial resolution) and pixel depth (intensity resolution) is **subjective** and depends heavily on the application and the "subject" matter of the image.
- **General Guidelines:**
    1.  For images of the same physical size, a low-detail image may need **more** pixel depth (gray levels) to appear smooth and satisfy human perception.
    2.  As the image size (number of pixels) increases, **fewer** gray levels might be needed to achieve a visually pleasing result, as the spatial detail compensates.
- **Trade-offs:** Higher resolution (both spatial and intensity) leads to larger file sizes and increased processing time.

### Basic Relationships Between Pixels

- Understanding how pixels relate to their neighbors is fundamental for many spatial domain operations.
- **Coordinate System:** Typically, images use matrix coordinates $(row, column)$ or Cartesian coordinates $(x, y)$, often with the origin $(0,0)$ at the top-left corner.
  *[Insert Image: Pixel Coordinate System Diagram - From Page 20]*

#### Neighbors of a Pixel

- **Neighborhood relations** define adjacency between pixels, crucial for analyzing regions and applying spatial filters. Let $p$ be a pixel at coordinates $(x, y)$.
1.  **4-neighbors ($N_4(p)$):** The set of pixels directly adjacent horizontally or vertically.
    - Coordinates: $(x-1, y), (x+1, y), (x, y-1), (x, y+1)$
    - Considers only vertical and horizontal neighbors.
    *[Insert Image: 4-Neighbors Diagram and Formula - From Page 21]*
    - Note: If $q \in N_4(p)$, then $p \in N_4(q)$.

2.  **8-neighbors ($N_8(p)$):** The set of all pixels directly surrounding pixel $p$ (horizontal, vertical, and diagonal).
    - Coordinates: $(x-1, y-1), (x, y-1), (x+1, y-1), (x-1, y), (x+1, y), (x-1, y+1), (x, y+1), (x+1, y+1)$
    - Considers all adjacent neighbor pixels.
    *[Insert Image: 8-Neighbors Diagram and Formula - From Page 22]*

3.  **Diagonal neighbors ($N_D(p)$):** The set of pixels directly adjacent diagonally.
    - Coordinates: $(x-1, y-1), (x+1, y-1), (x-1, y+1), (x+1, y+1)$
    - Considers only diagonal neighbor pixels.
    *[Insert Image: Diagonal Neighbors Diagram and Formula - From Page 23]*
- **Relationship:** $N_8(p) = N_4(p) \cup N_D(p)$.

### Mathematical Operations on Images

- Basic arithmetic operations can be performed on images pixel-by-pixel. Images usually need to be the same size.

#### 1. Image Addition

- **Formula:** $g(x, y) = f_1(x, y) + f_2(x, y)$
- **MATLAB Example Code:**
  ```matlab
  a1 = imread('D:\Matlab\bin\cameraman.jpg'); % Read image 1
  a2 = imread('D:\Matlab\bin\lena.jpg');      % Read image 2
  % Ensure same size (e.g., resize)
  a1_resized = imresize(a1, [255, 255]);
  a2_resized = imresize(a2, [255, 255]);
  % Add images (use imadd for handling data types and clipping)
  g = imadd(a1_resized, a2_resized, 'uint8');
  figure(1);
  subplot(1,3,1), imshow(a1_resized), title('Original Image');
  subplot(1,3,2), imshow(a2_resized), title('Image 2');
  subplot(1,3,3), imshow(g), title('Added Image');
  ```
  *[Insert Image: Image Addition Code Snippet - From Page 24]*
  *[Insert Image: Image Addition Result Visual - From Page 25]*
- **Applications:**
    - **Noise Reduction:** Averaging multiple images of the same scene reduces random noise.
    - **Image Blending/Morphing:** Creating special effects by combining images.

#### 2. Image Subtraction

- **Formula:** $g(x, y) = f_1(x, y) - f_2(x, y)$
- **MATLAB Example Code:**
  ```matlab
  a1 = imread('D:\Matlab\bin\cameraman.jpg');
  a2 = imread('D:\Matlab\bin\lena.jpg');
  a1_resized = imresize(a1, [255, 255]);
  a2_resized = imresize(a2, [255, 255]);
  % Subtract images (use imsubtract)
  g = imsubtract(a1_resized, a2_resized); % Order matters!
  figure(1);
  subplot(1,3,1), imshow(a1_resized), title('Original Image');
  subplot(1,3,2), imshow(a2_resized), title('Image 2');
  subplot(1,3,3), imshow(g), title('Subtracted Image');
  % Example 2 (Subtracting background?) - Code seems incomplete/duplicated
  a3 = imread('D:\Matlab\bin\cameraman.jpg');
  a4 = imread('D:\Matlab\bin\lena.jpg'); % Reads lena again?
  a3_resized = imresize(a3, [255, 255]);
  a4_resized = imresize(a4, [255, 255]);
  figure(2);
  subplot(1,3,1), imshow(a3_resized), title('Original Image');
  subplot(1,3,2), imshow(a4_resized), title('Image 2');
  % subplot(1,3,3), imshow(z); % z is not defined
  ```
  *[Insert Image: Image Subtraction Code Snippet - From Page 26]*
  *[Insert Image: Image Subtraction Result Visual - From Page 27 - Note: Image shown might be incorrect in source slides]*
- **Applications:**
    - **Change Detection:** Subtracting two images of the same scene taken at different times highlights differences.
    - **Background Removal:** Subtracting a known background image from a scene.
    - **Medical Imaging:** Digital Subtraction Angiography (DSA) enhances blood vessel visibility.

#### 3. Image Multiplication & Division

*[Insert Image: Multiplication/Division Formulas - From Page 28]*

- **Image Multiplication:**
  - **Formula:** $G(x, y) = f_1(x, y) \times f_2(x, y)$
  - **Applications:** Applying a **mask** to an image (where the mask image has values 0 or 1) to isolate regions of interest. Correcting shading (multiplying by an inverse shading pattern).
- **Image Division:**
  - **Formula:** $G(x, y) = f_1(x, y) / f_2(x, y)$
  - **Applications:** Correcting for non-uniform illumination (dividing by an estimated illumination field), calculating ratios between images. (Careful with division by zero!).

---

## 2.2 Spatial Domain Enhancement Techniques

### Image Enhancement Overview

*[Insert Image: Image Enhancement Definition - From Page 29]*

- **Objective:** To process an image so that the result is more suitable than the original image for a specific application or for human viewers. It aims to improve the **interpretability** of the information present.
- **Methods:** Enhancement algorithms achieve this by:
    - **Suppressing noise:** Reducing unwanted variations.
    - **Increasing image contrast:** Making features more distinct.
- **Subjectivity:** What constitutes "better" often depends on the specific goal and can be subjective.

### Spatial vs. Transform Domain Methods

*[Insert Image: Spatial vs Transform Domain Methods - From Page 30]*

Image enhancement techniques fall into two broad categories:

1.  **Spatial Domain Methods:**
    - Operate **directly** on the image pixels (the raw data $f(x,y)$).
    - Involves manipulating pixel values based on their original intensity or the intensity of their neighbors.
    - Examples: Contrast stretching, histogram equalization, spatial filtering (mean, median).
    - **Focus of this chapter section.**

2.  **Transform Domain Methods:**
    - Operate on a **transform** of the image (e.g., Fourier Transform $F(u,v)$).
    - Modify the transform coefficients and then perform the inverse transform to get the enhanced image.
    - Examples: Frequency domain filtering (low-pass, high-pass), homomorphic filtering.
    - **(Covered in Chapter 3 notes).**

### Spatial Domain: Point Processing

- Simplest spatial domain techniques.
- The output value $g(x, y)$ at a specific coordinate depends **only** on the input value $f(x, y)$ at the **same coordinate**.
- Transformation function: $s = T(r)$, where $r$ is the input pixel intensity and $s$ is the output pixel intensity.

#### 1) Image Negative (Digital Negative)

*[Insert Image: Image Negative Definition - From Page 31]*
*[Insert Image: Image Negative Formula & Application - From Page 32]*

- **Concept:** Inverts the intensity levels of an image. Dark areas become light, and light areas become dark.
- **Context:** Assumes grayscale image $f(m, n)$ with intensity values from $0$ (black) to $L-1$ (white). For 8-bit images, $L=256$, so levels are 0-255.
- **Transformation Formula:**
  $$
  g(m, n) = (L - 1) - f(m, n)
  $$
  For 8-bit images:
  $$
  g(m, n) = 255 - f(m, n)
  $$
  Where $g(m,n)$ is the negative image and $f(m,n)$ is the original image.
- **Application:** Useful for enhancing white or gray detail embedded in dark regions, especially in medical images like X-rays.
- **MATLAB Example Code:**
  ```matlab
  clear all;
  close all;
  a=imread("D:\Matlab\bin\cameraman.jpg");
  z=255-a; % Apply negative transformation
  figure(1);
  imshow(a); % Show original
  figure(2);
  imshow(z); % Show negative
  ```
  *[Insert Image: Image Negative Code Snippet - From Page 33]*
  *[Insert Image: Image Negative Result Visual - From Page 34]*

#### 2) Contrast Stretching (Contrast Adjustment)

*[Insert Image: Contrast Stretching Definition - From Page 35]*
*[Insert Image: Contrast Stretching Formulas & Effects - From Page 36]*

- **Problem:** Images acquired under poor illumination or with limited sensor dynamic range may have low contrast, making details hard to see.
- **Goal:** Increase the dynamic range of the gray levels in the image. Makes dark portions darker and bright portions brighter.
- **Simple Method (Contrast Adjustment):** Scaling all pixel values by a constant factor $k$.
  $$
  g[m, n] = f[m, n] \times k
  $$
- **Effect of $k$:**
    - $k > 1$: Increases contrast (stretches the range). Bright samples get brighter, dark samples get darker (relative to mid-gray).
    - $k < 1$: Decreases contrast (compresses the range).
- **Note:** This simple scaling can cause clipping if $f \times k$ exceeds the maximum possible value (e.g., 255). More sophisticated contrast stretching often involves mapping the input range $[r_{min}, r_{max}]$ to the full output range $[0, L-1]$ (see Linear Stretching under Histogram section).
- **MATLAB Example Code:**
  ```matlab
  clear all
  close all
  b=imread("D:\Matlab\bin\butterfly.jpg");
  % Assumes b is grayscale or converted:
  % b_gray = rgb2gray(b);
  z = b * 0.4; % Decrease contrast (k=0.4)
  k = b * 40;  % Increase contrast (k=40 - likely causes clipping!)
  figure(1);
  imshow(b); % Original
  figure(2);
  imshow(z); % Decreased Contrast
  figure(3);
  imshow(k); % Increased Contrast
  ```
  *[Insert Image: Contrast Adjustment Code Snippet - From Page 37]*
  *[Insert Image: Contrast Adjustment Result Visual - From Page 38]* (Shows original, decreased, increased contrast)

#### 3) Thresholding

*[Insert Image: Thresholding Definition & Formulas - From Page 39]*

- **Concept:** An extreme form of contrast stretching that produces a **binary** image.
- **Process:** A threshold value $T$ (or $a$ in the notes) is chosen. Pixels with intensity $r$ above or equal to the threshold are set to a high value (e.g., 255, white), and pixels below the threshold are set to a low value (e.g., 0, black).
- **Transformation Formula:**
  $$
  s = \begin{cases} L-1 & \text{if } r \ge T \\ 0 & \text{if } r < T \end{cases}
  $$
  Using notation from slide ($L-1=255$, threshold $a$, input $r$, output $S$):
  $$
  S = 255 \quad \text{if } r(\text{pixel intensity value}) \ge a(\text{threshold value})
  $$
  $$
  S = 0 \quad \text{if } r(\text{pixel intensity value}) < a(\text{threshold value})
  $$
- **Application:** Simple form of image **segmentation** – separating objects from the background based on intensity.
- **MATLAB Example Code:**
  ```matlab
  clear all;
  close all;
  a=imread("D:\Matlab\bin\tumor.jpg");
  a_gray=rgb2gray(a); % Convert to grayscale if needed
  p=a_gray; % Keep original for display
  [r c]=size(a_gray); % Get image dimensions
  T=input('Enter the value of Threshold '); % Get threshold from user
  for i=1:1:r
      for j=1:1:c
          if(p(i,j)<T) % Check pixel against threshold
              a_gray(i,j)=0; % Below threshold -> black
          else
              a_gray(i,j)=255; % At or above threshold -> white
          end
      end
  end
  figure(1);
  imshow(a_gray); % Show thresholded image
  figure(2);
  imshow(p); % Show original grayscale image
  ```
  *[Insert Image: Thresholding Code Snippet - From Page 40]*
  *[Insert Image: Thresholding Result Visual (tumor example) - From Page 41]*

#### 4) Gray Level Slicing (Intensity Slicing)

*[Insert Image: Gray Level Slicing Definition - From Page 42]*
*[Insert Image: Gray Level Slicing Methods & Formulas - From Page 43]*

- **Concept:** Similar to thresholding, but highlights a specific **range** or "slice" of gray levels. Useful for enhancing features within a certain intensity band (e.g., water bodies in satellite images, specific tissues in medical scans).
- **Process:** Select a range of interest $[a, b]$. Pixels within this range are highlighted (e.g., set to white), while others are either suppressed (set to black) or left unchanged.
- **Two Main Methods:**
    1.  **Without Background:** Highlight the range of interest and set everything else to a constant low value (e.g., black).
        - Formula (Input $r$, Output $S$, range $[a, b]$):
          $$
          S = \begin{cases} L-1 & \text{if } a \le r \le b \\ 0 & \text{otherwise} \end{cases}
          $$
        - *Slide Notation:* S=255 if a <= r <= b; S=0 otherwise.
        - *Effect:* Displays high value for the range, low value for others.
        - *MATLAB Code Example:*
          ```matlab
          % ... (read image 'a', convert to gray 'p', get size [r c]) ...
          T1=input('Enter the value of Threshold T1 '); % Lower bound 'a'
          T2=input('Enter the value of Threshold T2 '); % Upper bound 'b'
          a_processed = zeros(r,c,'uint8'); % Initialize output as black
          for i=1:1:r
              for j=1:1:c
                  if(p(i,j)>=T1 && p(i,j)<=T2) % Check if pixel is in range
                      a_processed(i,j)=255; % In range -> white
                  % else: remains 0 (black)
                  end
              end
          end
          % ... (display original 'p' and processed 'a_processed') ...
          ```
         *[Insert Image: Gray Level Slicing Code (Without Background) - From Page 44]*
         *[Insert Image: Gray Level Slicing Result (Without Background - Skull) - From Page 45]*

    2.  **With Background:** Highlight the range of interest but preserve the original gray levels for pixels outside the range.
        - Formula (Input $r$, Output $S$, range $[a, b]$):
          $$
          S = \begin{cases} L-1 & \text{if } a \le r \le b \\ r & \text{otherwise} \end{cases}
          $$
        - *Slide Notation:* S=255 if a <= r <= b; S=r otherwise.
        - *Effect:* Brightens the desired range, leaves other gray levels unchanged.
        - *MATLAB Code Example:*
          ```matlab
          % ... (read image 'a', convert to gray 'p', get size [r c]) ...
          T1=input('Enter the value of Threshold T1 '); % Lower bound 'a'
          T2=input('Enter the value of Threshold T2 '); % Upper bound 'b'
          a_processed = p; % Initialize output as the original image
          for i=1:1:r
              for j=1:1:c
                  if(p(i,j)>=T1 && p(i,j)<=T2) % Check if pixel is in range
                      a_processed(i,j)=255; % In range -> white
                  % else: remains p(i,j) (original value)
                  end
              end
          end
          % ... (display original 'p' and processed 'a_processed') ...
          ```
         *[Insert Image: Gray Level Slicing Code (With Background) - From Page 46]*
         *[Insert Image: Gray Level Slicing Result (With Background - Skull) - From Page 47]*

#### 5) Bit Plane Slicing

*[Insert Image: Bit Plane Slicing Definition - From Page 48]*
*[Insert Image: Bit Plane Diagram (Fig 3.12) - From Page 49]*
*[Insert Image: Bit Plane Diagram (Annotated) - From Page 50]*
*[Insert Image: Bit Plane Slicing Information Content - From Page 51]*

- **Concept:** Decomposes a grayscale image into a series of binary images, one for each bit of the pixel representation. Instead of highlighting intensity ranges, it highlights the contribution of each specific bit to the overall image.
- **Process:** For an 8-bit grayscale image (values 0-255), each pixel value can be represented by 8 bits. Bit-plane slicing creates 8 binary images (planes):
    - Plane 0 (Least Significant Bit - LSB): Contains the 0-th bit of every pixel.
    - Plane 1: Contains the 1st bit of every pixel.
    - ...
    - Plane 7 (Most Significant Bit - MSB): Contains the 7th bit of every pixel.
- **Information Content:**
    - **Higher-order bits** (closer to MSB, e.g., planes 7, 6, 5) usually contain the most significant visual information, representing the coarse structure and large intensity variations.
    - **Lower-order bits** (closer to LSB, e.g., planes 0, 1, 2) contain subtle details and often a significant amount of random noise.
- **Applications:**
    - **Image Compression:** Lower-order bit planes might be discarded with little visual impact, achieving compression (though modern methods are far more efficient).
    - **Steganography:** Hiding information within the lower-order bit planes, which are less visually significant.
    - **Image Analysis:** Understanding the contribution of different bit levels to the image content.
- **Example (3x3 Image):**
    *[Insert Image: Bit Plane Example (3x3 matrix calculation) - From Page 52]*
    - Shows a 3x3 image with max value 7 (needs 3 bits: 000 to 111).
    - Decomposes each pixel value (e.g., 4 is 100, 7 is 111) into its bits.
    - Forms three bit planes: LSB plane (bit 0), Middle bit plane (bit 1), MSB plane (bit 2).
- **MATLAB Example Code:**
  ```matlab
  clear all;
  close all;
  clc;
  a=imread('D:\Matlab\bin\lena.jpg'); % Assuming grayscale or converted
  % Initialize matrices for each bit plane (e.g., 256x256 for Lena)
  [rows cols] = size(a);
  b1=zeros(rows,cols); b2=zeros(rows,cols); % ... up to b8

  for m=1:rows
      for n=1:cols
          % Convert pixel value to 8-bit binary string
          t=de2bi(a(m,n),8,'left-msb'); % 'left-msb' makes t(1)=MSB, t(8)=LSB
          % Assign each bit to its corresponding plane matrix
          b8(m,n)=t(1); % MSB Plane (Bit 7)
          b7(m,n)=t(2); % Bit 6 Plane
          b6(m,n)=t(3); % Bit 5 Plane
          b5(m,n)=t(4); % Bit 4 Plane
          b4(m,n)=t(5); % Bit 3 Plane
          b3(m,n)=t(6); % Bit 2 Plane
          b2(m,n)=t(7); % Bit 1 Plane
          b1(m,n)=t(8); % LSB Plane (Bit 0)
      end
  end

  % Display results
  subplot(3,3,1); imshow(a); title('Image of cameramen'); % Title mismatch? Should be Lena
  subplot(3,3,2); imshow(b8); title('image of bit-7'); % MSB
  subplot(3,3,3); imshow(b7); title('image of bit-6');
  subplot(3,3,4); imshow(b6); title('image of bit-5');
  subplot(3,3,5); imshow(b5); title('image of bit-4');
  subplot(3,3,6); imshow(b4); title('image of bit-3');
  subplot(3,3,7); imshow(b3); title('image of bit-2');
  subplot(3,3,8); imshow(b2); title('image of bit-1');
  % Missing subplot for LSB (b1)? Code seems to show bits 7 down to 1.
  ```
  *[Insert Image: Bit Plane Slicing Code Pt1 - From Page 53]*
  *[Insert Image: Bit Plane Slicing Code Pt2 (Display) - From Page 54]*
  *[Insert Image: Bit Plane Slicing Result Visual - From Page 55]* (Shows original and bit planes 7 down to 0, confirming 8 planes).

#### 6) Dynamic Range Compression (Log Transformation)

*[Insert Image: Dynamic Range Compression Problem - From Page 56]*
*[Insert Image: Log Transformation Formula & Concept - From Page 57]*

- **Problem:** Sometimes the **dynamic range** (ratio between maximum and minimum intensity values) of an image is very large and exceeds the display capability of a device or human perception. High pixel values can overshadow details in the low pixel value regions. (e.g., Fourier spectra often have very high DC/low-frequency values and much smaller high-frequency values).
- **Goal:** Compress the dynamic range so that both high and low values are visible simultaneously.
- **Method:** Use a **Logarithmic Transformation**. The log function compresses larger values more strongly than smaller values.
- **Transformation Formula:**
  $$
  s = c \times \log(1 + |r|)
  $$
  Where:
    - $r$: Input pixel intensity (absolute value $|r|$ used to handle potential negative values if input isn't standard image). `1+` is added to handle $r=0$ since $\log(0)$ is undefined.
    - $s$: Output pixel intensity.
    - $c$: A scaling constant, used to adjust the output range (e.g., to fit 0-255).
- **Effect:** Expands the range of dark pixel values and compresses the range of bright pixel values.
- **MATLAB Example Code:**
  ```matlab
  a1 = imread('D:\Matlab\bin\saturn.jpg'); % Read image
  % Convert to double and normalize (optional but good practice for log)
  a = double(a1)/256;
  c = 2; % Constant (adjust as needed)
  % Apply Log Transform
  f = c*log(1 + (a)); % Use 'a' directly if already double and non-negative
  figure(1)
  subplot(1,2,1), imshow(a1), title('Original Image'); % Show original uint8
  subplot(1,2,2), imshow(f), title('Log Transformation Image'); % Show processed double
  ```
  *[Insert Image: Log Transform Code Snippet - From Page 58]*
  *[Insert Image: Log Transform Result Visual (c=2) - From Page 59]*
  *[Insert Image: Log Transform Result Visual (c=4) - From Page 60]*
  *[Insert Image: Log Transform Result Visual (c=10) - From Page 61]*
- **Observation:** As `c` increases, the output image becomes brighter. The log transform makes faint details (like the rings/background structure in the Saturn image) more visible.

#### 7) Power Law (Gamma) Transformation

*[Insert Image: Power Law Motivation - From Page 62]*
*[Insert Image: Power Law Formula & Concept - From Page 63]*

- **Motivation:**
    1.  **Human Perception:** Our eyes are more sensitive to changes in dark intensity levels than bright ones.
    2.  **Display Devices:** Devices like CRT monitors and many LCDs have a non-linear relationship between input voltage and output brightness, often approximated by a power function with an exponent (**gamma**, $\gamma$) typically between 1.8 and 2.5. This makes images appear darker than intended if not corrected.
- **Concept (Gamma Correction):** Apply a power-law transformation to the input image signal to counteract the display's gamma, making the perceived image look correct.
- **Transformation Formula:**
  $$
  s = c \times r^\gamma
  $$
  Where:
    - $r$: Input pixel intensity (usually normalized to [0, 1]).
    - $s$: Output pixel intensity.
    - $c$: A scaling constant (often 1 if input/output are [0, 1]).
    - $\gamma$: The exponent (gamma value).
- **Effect:**
    - $\gamma > 1$: Compresses dark values, expands bright values. Makes the image **darker**. (Used to simulate display effect).
    - $\gamma < 1$: Expands dark values, compresses bright values. Makes the image **brighter**. (Used for **gamma correction** - applying $1/\gamma_{display}$ to the image).
    - $\gamma = 1$: Linear mapping (no change).
- **MATLAB Example Code:**
  ```matlab
  a1 = imread('D:\Matlab\bin\cameraman.jpg');
  a = double(a1)/256; % Normalize image to [0, 1]
  gamma=input('Enter the correction factor gamma value: ');
  c=2; % Scaling constant (may need adjustment or set to 1)
  % Apply Power Law Transform
  f = c*a.^gamma; % Element-wise power: .^
  subplot(1,2,1),imshow(a1),title('Original Image');
  subplot(1,2,2),imshow(f),title('Power Law Image');
  ```
  *[Insert Image: Power Law Code Snippet - From Page 64]*
  *[Insert Image: Power Law Result Visual (gamma=0.4 - brighter) - From Page 65]*
  *[Insert Image: Power Law Result Visual (gamma=2.2 - darker) - From Page 66]*

#### Comparison: Power Law vs. Contrast Stretching

*[Insert Image: Power Law vs Contrast Stretching Table - From Page 67]*

| Feature            | Power Law Transformation                       | Contrast Stretching (Linear)                     |
| :----------------- | :--------------------------------------------- | :----------------------------------------------- |
| **Transformation Type** | **Nonlinear** (depends on exponent $\gamma$) | **Linear** (stretches pixel values)            |
| **Effect on Image** | Adjusts **brightness** and **local contrast** | Increases **global contrast**                    |
| **Parameter**      | Gamma ($\gamma$) determines nonlinearity      | Min/Max input/output values determine stretch |
| **Pixel Range**    | May alter distribution, not necessarily range | Expands range to desired output min/max        |
| **Visual Impact**  | Brightens/darkens based on $\gamma$            | Increases overall contrast, makes ends darker/brighter |
| **Use Case**       | Gamma correction, brightness adjustment        | Improving visibility in low contrast images    |

---

### Spatial Domain: Neighborhood Processing (Spatial Filtering)

*[Insert Image: Neighborhood Processing Concept - From Page 68]*

- **Concept:** The output value for a pixel $g(x, y)$ depends on the input pixel values $f$ in a **neighborhood** around $(x, y)$.
- **Mechanism:** Usually involves moving a **filter mask** (also called a kernel, template, or window) across the image. At each position $(x, y)$, the output pixel value is calculated based on the input pixels covered by the mask and the mask's coefficients. This process is typically **convolution** or **correlation**.
- **Neighborhood Size:** Common sizes are 3x3, 5x5, 7x7, etc. Larger neighborhoods generally produce stronger effects.

#### Low Pass Averaging Filter (Box Filter)

*[Insert Image: Low Pass Averaging Filter Concept - From Page 69]*
*[Insert Image: Low Pass Averaging Filter Effect - From Page 70]*
*[Insert Image: Averaging Filter Masks (3x3, 5x5) - From Page 71]*
*[Insert Image: Averaging Filter Properties - From Page 72]*

- **Purpose:** Reduce noise (especially Gaussian noise) and smooth the image by blurring.
- **Mechanism (Mean Filter):** Replaces each pixel's value with the **average** (mean) of all pixel values within its local neighborhood defined by the mask.
- **Mask:** A simple averaging filter uses a mask where all coefficients are equal. To preserve the overall brightness, the sum of the coefficients should equal 1.
    - **3x3 Mask:**
      $$
      h = \frac{1}{9} \begin{bmatrix} 1 & 1 & 1 \\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{bmatrix}
      $$
    - **5x5 Mask:**
      $$
      h = \frac{1}{25} \begin{bmatrix} 1 & 1 & 1 & 1 & 1 \\ \vdots & \vdots & \vdots & \vdots & \vdots \\ 1 & 1 & 1 & 1 & 1 \end{bmatrix}
      $$
- **Properties:**
    - It's a **low-pass** filter because averaging suppresses rapid changes (high frequencies).
    - Preserves smooth regions.
    - Removes sharp variations (edges, noise), leading to a **blurring effect**.
    - **Blurring increases** with the size of the mask (neighborhood).
    - Mask size is usually **odd** (3x3, 5x5) so there's a clear central pixel.
- **Example Calculation:**
    *[Insert Image: Averaging Filter Example Calculation Pt1 - From Page 73]*
    *[Insert Image: Averaging Filter Example Calculation Pt2 - From Page 74]*
    - Shows applying a 3x3 averaging mask to an image with a sharp edge (values 10 and 50).
    - Pixels far from the edge remain unchanged (average of 10s is 10, average of 50s is 50).
    - Pixels near the edge get blurred. E.g., a pixel surrounded by six 10s and three 50s becomes $(6 \times 10 + 3 \times 50)/9 = 210/9 \approx 23.33$.
    - The sharp transition from 10 to 50 is replaced by a smoother transition (e.g., 10 -> 23.33 -> 36.6 -> 50).
    *[Insert Image: Averaging Filter Blurring Effect Description - From Page 75]*
- **Limitations:**
    *[Insert Image: Averaging Filter Limitations Text - From Page 76]*
    1.  **Blurring:** The main drawback is that it blurs sharp edges and fine details along with noise. Affects feature localization.
    2.  **Impulse Noise:** Not very effective against impulse noise (salt-and-pepper noise). It attenuates and diffuses the noise spots but doesn't remove them effectively.
        *[Insert Image: Impulse Noise Visual Example - From Page 77]* (Showing speckled noise)
    3.  **Outlier Sensitivity:** A single pixel with an unrepresentative value (an outlier) within the neighborhood can significantly affect the calculated mean for the center pixel.
- **Visual Result:**
    *[Insert Image: Averaging Filter Visual Result (Rose) - From Page 78]* (Shows original, 3x3 filtered, 5x5 filtered - increasing blur)

#### Weighted Average Filter

*[Insert Image: Weighted Average Mask Example - From Page 79]*
*[Insert Image: Weighted Average Filter Concept - From Page 80]*

- **Concept:** A variation of the averaging filter where pixels in the neighborhood contribute differently to the average, typically based on their distance from the center.
- **Mask:** Coefficients are not all equal. Pixels nearer the center are given higher weights. The sum of weights should still equal 1 for normalization.
    - **Example 3x3 Mask:**
      $$
      h = \frac{1}{16} \begin{bmatrix} 1 & 2 & 1 \\ 2 & 4 & 2 \\ 1 & 2 & 1 \end{bmatrix}
      $$
- **Rationale:** The center pixel is often considered more important, and closer neighbors are more correlated. Assigning higher weights to closer pixels aims to reduce blurring compared to the simple averaging filter while still smoothing noise. This specific mask approximates a Gaussian function.

#### Median Filter

*[Insert Image: Median Filter Concept - From Page 81]*
*[Insert Image: Median Filter Steps - From Page 81]*
*[Insert Image: Median Filter Advantages - From Page 86]*

- **Concept:** A **non-linear** statistical filter. It replaces the center pixel's value with the **median** of the intensity values in its neighborhood.
- **Process:**
    1.  Identify all pixels in the neighborhood of the current pixel (including the center pixel).
    2.  Sort the intensity values of these neighboring pixels in ascending (or descending) order.
    3.  Compute the median (middle value) of the sorted list.
    4.  Replace the original center pixel's value with the computed median.
- **Example 1 (Simple 3x3):**
    *[Insert Image: Median Filter Example 1 (3x3 calculation) - From Page 82]*
    - Neighborhood values: {1, 5, 7, 2, 4, 6, 3, 2, 1}
    - Sorted values: {1, 1, 2, 2, **3**, 4, 5, 6, 7}
    - Median value is 3.
    - The original center pixel (value 4) is replaced by 3.
- **Example 2 (Larger Image):**
    *[Insert Image: Median Filter Example 2 Pt1 - From Page 83]*
    *[Insert Image: Median Filter Example 2 Pt2 - From Page 84]*
    *[Insert Image: Median Filter Example 2 Pt3 (Final Result) - From Page 85]*
    - Shows step-by-step calculation for several pixels in an image using a 3x3 neighborhood.
- **Advantages:**
    - **Excellent for removing impulse noise (salt-and-pepper noise).** Outlier pixel values (very high or very low) tend to end up at the extremes of the sorted list and are ignored when the median is chosen.
    - **Less blurring** of edges compared to the mean filter, especially when noise is impulsive. The median is more robust to outliers.
- **Comparison with Averaging/Box Filter:**
    *[Insert Image: Salt & Pepper Noise Removal (Smoothing Result) - From Page 87]* (Shows averaging filter diffuses noise, blurs image)
    *[Insert Image: Salt & Pepper Noise Removal (Median Result) - From Page 88]* (Shows median filter removes noise effectively, preserves edges better)

#### Comparison Between Filters (Average, Weighted, Median)

*[Insert Image: Filter Comparison Table - From Page 89]*

| Parameters               | Average Filter                                     | Weighted Filter                               | Median Filter                                      |
| :----------------------- | :------------------------------------------------- | :-------------------------------------------- | :------------------------------------------------- |
| **Noise Reduction**    | Reduces Noise but introduces blurring at edges.    | Blurring effect is less than Average filter.  | Blurring effect is less than Average filter.       |
| **Percentage of noise Reduction** | (Implies less effective on some noise types) | (Similar to Average for Gaussian noise)       | Almost 100% noise reduced (especially impulse).    |
| **Size of Filter**       | Increase size: Noise reduces but blurring increases. | Increase size: Noise reduces but blurring increases. | Increase size: Noise reduces but blurring increases at edges. |
| **Mask Example**         | 1/9 * [1,1,1; 1,1,1; 1,1,1]                      | 1/16 * [1,2,1; 2,4,2; 1,2,1]                | Pixel value replaced by median of neighborhood.    |
| **MATLAB Function**      | `filter2(mask, Noisy_img)` or `imfilter`           | `filter2(mask, Noisy_img)` or `imfilter`        | `medfilt2(Noisy_img, [3 3])`                       |

**Simplified Summary:**
- **Average:** Simple, good for Gaussian noise, blurs edges.
- **Weighted Average:** Less blurring than simple average.
- **Median:** Non-linear, great for salt-and-pepper noise, preserves edges better than average filters.

### Spatial Domain: Highpass Filtering (Sharpening)

*[Insert Image: Highpass Filtering Concept - From Page 90]*
*[Insert Image: Highpass Filter Mask Example - From Page 91]*
*[Insert Image: Highpass Filter Zero Sum Property - From Page 92]*

- **Purpose:** Enhance fine details and edges in an image, leading to a "sharpened" appearance.
- **Mechanism:** Eliminates or reduces the low-frequency components (smooth areas, background) while retaining or enhancing the high-frequency components (edges, noise, texture).
- **Result:** High-pass filtered images often have little or no background, emphasizing regions of rapid intensity change.
- **Spatial Mask:** High-pass filter masks typically have positive coefficients near the center and negative coefficients in the outer periphery. A common characteristic is that the **sum of the coefficients is zero**. This ensures that areas of constant intensity (zero frequency) result in zero output, effectively removing the DC component or background.
    - **Example 3x3 Sharpening Mask (Laplacian-like):**
      $$
      h = \frac{1}{9} \begin{bmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{bmatrix} \quad \text{(Note: Normalization factor may vary or be omitted)}
      $$
      (Sum = -1*8 + 8 = 0).
- **Example Calculation:**
    *[Insert Image: Highpass Filter Example Calculation Pt1 - From Page 93]*
    *[Insert Image: Highpass Filter Example Calculation Pt2 (Result) - From Page 94]*
    - Shows applying the high-pass mask. The result emphasizes the edge between the 10 and 100 regions.
    - **Note on Output:** The output values can be negative or exceed the standard range [0, 255]. Often, the result is scaled or clipped, or added back to the original image (see High-boost). Negative values are typically set to zero for display.

### High-boost Filtering

*[Insert Image: High-boost Filtering Concept - From Page 95]*
*[Insert Image: High-boost Filtering Formula - From Page 96]*
*[Insert Image: High-boost Filtering Mask Structure - From Page 97]*

- **Concept:** A technique to sharpen an image while **retaining** some of the low-frequency components (background). Also known as **high-frequency emphasis filtering**. Standard high-pass filtering removes the background entirely.
- **Mechanism:** The input image $f(m, n)$ is multiplied by an amplification factor $A$ ($A \ge 1$), and then a low-pass version of the image is subtracted. Alternatively, it can be seen as adding a high-pass filtered image back to the original image, scaled by $(A-1)$.
- **Formula Derivation:**
    - High-boost = $A \times f - f_{lowpass}$
    - Since $f_{highpass} = f - f_{lowpass}$, we have $f_{lowpass} = f - f_{highpass}$.
    - Substitute: High-boost = $A \times f - (f - f_{highpass})$
    - High-boost = $A \times f - f + f_{highpass}$
    - **High-boost = $(A - 1) \times f + f_{highpass}$**
- **Mask Implementation:** The high-boost filter can often be implemented with a single mask derived from the high-pass mask. If the high-pass mask $h_{hp}$ sums to zero and has center weight $W_c$, the high-boost mask $h_{hb}$ can be constructed by changing the center weight to $W_c + (A-1) \times (\text{Sum of absolute values of mask coeffs, or just A }?)$.
    - Using the example high-pass mask ($1/9$ factor ignored for structure): $[-1, -1, -1; -1, 8, -1; -1, -1, -1]$.
    - The high-boost mask has a center weight adjusted. If A is the amplification factor (often called k in the mask):
      $$
      h_{hbf} = \frac{1}{9} \begin{bmatrix} -1 & -1 & -1 \\ -1 & 9A-1 & -1 \\ -1 & -1 & -1 \end{bmatrix} \quad \text{(Common form, or simply adjust center coeff: } \frac{1}{9} [-1, -1, -1; -1, 9A-1, -1; -1, -1, -1])
      $$
      *Slide notation:* Center weight is $9k-1$ (where $k$ is amplification factor A).
      $$
      w = \frac{1}{9} \begin{bmatrix} -1 & -1 & -1 \\ -1 & 9k-1 & -1 \\ -1 & -1 & -1 \end{bmatrix}
      $$
- **Effect:** Sharpens details like a high-pass filter but keeps the overall background structure visible. Factor $A$ controls the amount of boosting. $A=1$ gives a standard high-pass filter result.

### Zooming

*[Insert Image: Zooming Concept - From Page 98]*
*[Insert Image: Zooming by Pixel Replication Illustration - From Page 99]*
*[Insert Image: Zooming Visual Result - From Page 100]*

- **Purpose:** Increase the spatial resolution of an image (magnify it) to examine fine details. Equivalent to viewing through a magnifying glass.
- **Challenge:** Need to create new pixel locations and assign values to them.
- **Simplest Method: Pixel Replication (Nearest Neighbor Interpolation):**
    - To zoom an image by a factor (e.g., 2), create a larger grid and replicate each original pixel value into the corresponding block of new pixels.
    - *Example:* To zoom 2x, each pixel $f(x,y)$ becomes a 2x2 block of pixels in the zoomed image $g$, all with the value $f(x,y)$.
- **Advantage:** Very simple and fast.
- **Disadvantage:** Can produce a blocky or jagged appearance ("pixelated"). More sophisticated methods like **bilinear** or **bicubic interpolation** produce smoother results by considering multiple neighboring pixels to estimate the new pixel values.

---

## 2.3 Spatial Enhancement: Global Processing - Histogram Methods

- These methods modify pixels based on the **global** intensity distribution of the entire image, as captured by the image **histogram**.

### Histogram Modeling

*[Insert Image: Histogram Definition - From Page 101]*
*[Insert Image: Histogram Plotting Method 1 (Counts) - From Page 102]*
*[Insert Image: Histogram Plotting Method 2 (Normalized) - From Page 103]*
*[Insert Image: Normalized Histogram Advantages - From Page 104]*

- **Histogram:** A function showing the frequency of occurrence of each gray level (intensity value) in an image. It provides a global description of the image's appearance (contrast, brightness).
    - $h(r_k) = n_k$
    Where $r_k$ is the $k$-th gray level and $n_k$ is the number of pixels in the image with that gray level.
- **Plotting Methods:**
    1.  **Method 1:** Plot the number of pixels ($n_k$) for each gray level ($r_k$).
    2.  **Method 2 (Normalized Histogram):** Plot the probability or relative frequency of occurrence for each gray level.
        $$
        p(r_k) = \frac{n_k}{N}
        $$
        Where $N$ is the total number of pixels in the image.
        - The sum of all values in a normalized histogram is 1.
        - Maximum value plotted is $\le 1$.
        - Provides clear information about the image's intensity distribution, independent of image size.

### Histogram (Linear) Stretching

*[Insert Image: Linear Stretching Concept - From Page 105]*
*[Insert Image: Linear Stretching Formula & Variables - From Page 106]*

- **Concept:** A technique to increase the dynamic range (contrast) of an image by linearly mapping the original range of gray levels to a new, wider range (typically the full possible range, e.g., 0 to 255).
- **Process:** Finds the minimum ($r_{min}$) and maximum ($r_{max}$) intensity values present in the input image and maps them to the desired minimum ($s_{min}$) and maximum ($s_{max}$) output values. Values in between are linearly interpolated.
- **Formula:** The transformation $s = T(r)$ is given by:
  $$
  s = \left( \frac{s_{max} - s_{min}}{r_{max} - r_{min}} \right) (r - r_{min}) + s_{min}
  $$
  Where:
    - $r$: Input gray level
    - $s$: Output gray level
    - $r_{min}, r_{max}$: Minimum and maximum gray levels in the input image.
    - $s_{min}, s_{max}$: Minimum and maximum desired gray levels in the output image (e.g., 0 and 255).
- **Effect:** Spreads out the histogram to cover the entire dynamic range without changing its basic shape significantly. Improves contrast in images where the original values occupy only a narrow portion of the possible range. (This is a more formal version of the Contrast Adjustment discussed earlier).

### Histogram Equalization

*[Insert Image: Histogram Equalization Concept - From Page 107]*
*[Insert Image: Histogram Equalization Procedure - From Page 108]*

- **Concept:** A powerful technique that attempts to redistribute the pixel intensity values so that the histogram of the output image is approximately **uniform** (flat).
- **Goal:** Spreads out the gray levels evenly across their range, effectively increasing the global contrast, especially when the image data is represented by close contrast values.
- **Mechanism:** Reassigns brightness values based on the cumulative distribution function (CDF) of the image histogram. Tries to make the output histogram as flat as possible.
- **Advantages:** Often provides more visually pleasing results across a wider range of images compared to linear stretching. Fully automatic (no parameters needed).
- **Procedure:**
    1.  **Compute Histogram:** Find the number of pixels $n_k$ for each gray level $r_k$ in the input image (range 0 to L-1).
    2.  **Compute Cumulative Histogram (CDF):** Calculate the running sum of the histogram values.
        $$
        CDF(r_k) = \sum_{j=0}^{k} n_j
        $$
    3.  **Normalize CDF:** Divide the CDF values by the total number of pixels ($N$). This gives values in the range [0, 1].
        $$
        CDF_{norm}(r_k) = \frac{CDF(r_k)}{N} = \sum_{j=0}^{k} p(r_j)
        $$
    4.  **Transform (Map Gray Levels):** Multiply the normalized CDF values by the maximum gray level value ($L-1$) and round to the nearest integer. This gives the new gray level $s_k$ corresponding to the original gray level $r_k$.
        $$
        s_k = \text{round}((L-1) \times CDF_{norm}(r_k))
        $$
    5.  **Create Output Image:** Replace each pixel with gray level $r_k$ in the original image with the new gray level $s_k$.
- **Example Calculation:**
    - **Input Image & Histogram:**
        *[Insert Image: Histogram Eq Example Image (Matrix) - From Page 109]*
        *[Insert Image: Histogram Eq Example Step 0 (Histogram Table) - From Page 110]*
        - Image size 5x5 = 25 pixels (N=25). Max value 5. Assume 8 levels (L=8, 0-7).
        - Histogram: $n_3=6, n_4=14, n_5=5$. Others are 0.
    - **Step 1: Running Sum (CDF):**
        *[Insert Image: Histogram Eq Example Step 1 (Running Sum Table) - From Page 111]*
        - CDF: 0, 0, 0, 6, 20, 25, 25, 25
    - **Step 2: Normalize CDF (Divide by N=25):**
        *[Insert Image: Histogram Eq Example Step 2 (Normalize Table) - From Page 112]*
        - CDF_norm: 0, 0, 0, 6/25, 20/25, 25/25, 25/25, 25/25
    - **Step 3: Scale & Round (Multiply by L-1 = 7):**
        *[Insert Image: Histogram Eq Example Step 3 (Scale Table) - From Page 113]*
        *[Insert Image: Histogram Eq Example Step 3 (Rounded Table) - From Page 114]*
        - Scaled: 0, 0, 0, 42/25, 140/25, 175/25, 175/25, 175/25
        - Scaled (approx): 0, 0, 0, 1.68, 5.6, 7, 7, 7
        - Rounded ($s_k$): 0, 0, 0, 2, 6, 7, 7, 7
    - **Step 4: Mapping & Result:**
        *[Insert Image: Histogram Eq Example Step 4 (Mapping Table & Result Matrix) - From Page 115]*
        - Mapping: 0->0, 1->0, 2->0, 3->2, 4->6, 5->7, 6->7, 7->7
        - Apply mapping to original image matrix.
- **Visual Example:**
    *[Insert Image: Histogram Eq Visual Example (Baby) - From Page 116]*
    - Shows a dark, low-contrast original image with its histogram clustered at low values.
    - After equalization, the image has much better contrast, and its histogram is spread across the entire range, appearing more uniform.

### Self-Learning Topic: Histogram Specification (Matching)

- While not detailed in these slides, **Histogram Specification** is a related technique where instead of aiming for a flat histogram (like equalization), the goal is to transform the image so that its histogram matches the shape of a *specified* target histogram. This allows for more control over the output image appearance.

---

## Section Summary: Spatial Domain Enhancement

- **Operates directly on pixels.**
- **Point Processing:** Output depends only on one input pixel ($s=T(r)$).
    - *Negative:* Inverts intensities ($s=L-1-r$).
    - *Contrast Stretching:* Linearly scales intensities ($s=k \times r$) or maps input range to output range.
    - *Thresholding:* Creates binary image based on a threshold ($s=0$ or $L-1$).
    - *Gray Level Slicing:* Highlights a specific intensity range.
    - *Bit Plane Slicing:* Decomposes image into binary bit planes.
    - *Log Transform:* Compresses dynamic range ($s=c \log(1+|r|)$).
    - *Power Law (Gamma):* Adjusts brightness non-linearly ($s=cr^\gamma$), used for gamma correction.
- **Neighborhood Processing (Spatial Filtering):** Output depends on neighboring pixels.
    - *Averaging Filter:* Linear, mean of neighbors, smooths noise, blurs edges.
    - *Weighted Average:* Linear, weighted mean, less blurring.
    - *Median Filter:* Non-linear, median of neighbors, good for impulse noise, preserves edges better.
    - *Highpass Filter:* Enhances edges/details, removes background (zero-sum mask).
    - *High-boost Filter:* Sharpens details while retaining background.
- **Zooming:** Increases spatial resolution (e.g., pixel replication).
- **Histogram Processing (Global):** Uses image histogram for enhancement.
    - *Stretching:* Linearly expands histogram range.
    - *Equalization:* Aims for a flat output histogram, automatically enhances contrast using CDF.

---

## Glossary of New Terms (Chapter 2)

- **Digital Image Processing (DIP):** Using computers to manipulate digital images.
- **Image Analysis:** Extracting measurements or quantitative data from images.
- **Computer Vision:** Enabling computers to "see" and interpret images like humans.
- **Photon:** Elementary particle of light.
- **Wavelength ($\lambda$):** Distance between wave crests.
- **Frequency ($f$):** Number of waves per unit time.
- **Image Acquisition:** Capturing and digitizing an image.
- **Image Enhancement:** Subjective improvement of image appearance or interpretability.
- **Image Restoration:** Objective removal of known image degradations.
- **Morphological Processing:** Operations related to shape and structure.
- **Segmentation:** Partitioning an image into regions or objects.
- **Object Recognition:** Assigning labels to detected objects.
- **Representation & Description:** Converting segmented objects into usable features.
- **Image Compression:** Reducing image data size.
- **Sampling:** Discretizing spatial coordinates in image digitization.
- **Quantization:** Discretizing intensity values in image digitization.
- **Spatial Resolution:** Number of pixels in an image (related to sampling).
- **Intensity Resolution (Bit Depth):** Number of bits used per pixel, determining the number of gray levels or colors (related to quantization).
- **False Contouring:** Artificial edges appearing due to insufficient quantization levels.
- **Pixel:** Picture element, the smallest unit of a digital image holding an intensity/color value.
- **Neighbors (4-, 8-, Diagonal):** Sets of pixels adjacent to a given pixel.
- **Adjacency:** Defines which pixels are considered connected based on neighborhood and intensity similarity (not explicitly covered but related).
- **Connectivity:** Defines paths between pixels based on adjacency (not explicitly covered).
- **Image Addition/Subtraction/Multiplication/Division:** Arithmetic operations performed pixel-wise between images.
- **Spatial Domain:** Operations performed directly on image pixel values.
- **Transform Domain:** Operations performed on a transform (e.g., Fourier) of an image.
- **Point Processing:** Spatial operations where output pixel depends only on the corresponding input pixel ($s=T(r)$).
- **Image Negative:** Point process inverting intensity ($s=L-1-r$).
- **Contrast Stretching:** Point process to expand the range of intensity values.
- **Thresholding:** Point process creating a binary image based on a threshold value.
- **Gray Level Slicing:** Point process highlighting a specific range of intensities.
- **Bit Plane Slicing:** Decomposing an image into binary images based on bit positions.
- **LSB (Least Significant Bit):** The lowest-order bit in a binary number.
- **MSB (Most Significant Bit):** The highest-order bit in a binary number.
- **Dynamic Range:** Ratio between maximum and minimum intensity values.
- **Log Transformation:** Point process compressing dynamic range ($s = c \log(1+|r|)$).
- **Power Law (Gamma) Transformation:** Point process for non-linear brightness adjustment ($s=cr^\gamma$).
- **Gamma Correction:** Using power law transform to compensate for display non-linearity.
- **Neighborhood Processing (Spatial Filtering):** Operations where output pixel depends on input pixels in a local neighborhood.
- **Filter Mask (Kernel, Template, Window):** A small array of coefficients used in spatial filtering.
- **Convolution/Correlation:** Mathematical operations used to apply spatial filters.
- **Low Pass Filter (Spatial):** Filter that averages neighbors, causing smoothing/blurring.
- **Averaging (Mean) Filter:** Simple low-pass filter using equal weights.
- **Gaussian Noise:** Random noise following a Gaussian distribution.
- **Impulse Noise (Salt-and-Pepper Noise):** Noise characterized by random occurrences of black and white pixels.
- **Weighted Average Filter:** Low-pass filter using non-equal weights (e.g., Gaussian-like).
- **Median Filter:** Non-linear filter replacing pixel with median of neighbors, effective for impulse noise.
- **Highpass Filter (Spatial):** Filter that enhances edges and details (e.g., using Laplacian-like masks).
- **Sharpening:** Enhancing edges and fine details.
- **High-boost Filtering:** Sharpening technique that retains background information.
- **Zooming:** Increasing the spatial resolution (size) of an image.
- **Pixel Replication (Nearest Neighbor):** Simple zooming method by duplicating pixels.
- **Interpolation (Bilinear, Bicubic):** More advanced methods for zooming/resizing.
- **Histogram:** Plot showing the frequency of each intensity level in an image.
- **Normalized Histogram:** Histogram where values represent probabilities ($p(r_k)=n_k/N$).
- **Histogram Stretching:** Linearly mapping the histogram to cover the full dynamic range.
- **Histogram Equalization:** Processing an image to make its histogram approximately flat, enhancing contrast.
- **CDF (Cumulative Distribution Function):** Running sum of histogram values (used in equalization).
- **Histogram Specification (Matching):** Modifying an image so its histogram matches a target histogram.

---

## Further Learning Resources

- **Digital Image Processing** by Gonzalez and Woods: Chapters 2 and 3 cover these fundamentals extensively.
- **Digital Image Processing Using MATLAB** by Gonzalez, Woods, and Eddins: Provides practical implementations and further examples.
- **Online Courses:** Platforms like Coursera, edX often have courses on DIP fundamentals.
- **Software Documentation:** MATLAB Image Processing Toolbox, Python libraries (OpenCV, Scikit-Image, Pillow) document these functions with examples. Search for functions like `imadjust`, `histeq`, `imfilter`, `medfilt2`, `de2bi`, `imresize`.
