
# Chapter 10: Image Segmentation

*(Reference: Digital Image Processing, 2nd ed., Gonzalez & Woods)*

## Introduction to Image Segmentation

*[Insert Image: Chapter 10 Title Slide - From Page 1]*
*[Insert Image: Segmentation Definition and Approaches - From Page 2]*

- **Definition:** **Image segmentation** is the process of partitioning or dividing a digital image into multiple **regions** or sets of pixels.
- **Goal:** To simplify or change the representation of an image into something that is more meaningful and easier to analyze. Typically, the goal is to locate and **find individual objects** or boundaries within an image.
- **Criteria for Regions:** Pixels within a region should be:
    - **Connected:** There should be a path between any two pixels within the region, consisting entirely of pixels from that region.
    - **Similar:** Pixels within a region should share some common property or characteristic (e.g., intensity, color, texture).
    - **Different:** Adjacent regions should have some difference in the characteristic property.

### Fundamental Approaches to Segmentation

There are two fundamental approaches based on how pixel properties are analyzed:

1.  **Detecting Discontinuity:** Partitioning an image based on **abrupt changes** in intensity or other properties. This focuses on finding the **boundaries** between regions.
    - Primarily involves detecting:
        - **Points:** Isolated pixels different from their surroundings.
        - **Lines:** Thin structures different from their surroundings.
        - **Edges:** Boundaries between regions of different intensity/color/texture. Sudden changes define edges.
    - *Analogy:* Finding the fences between properties.

2.  **Detecting Similarity:** Grouping pixels based on whether they share common attributes within a region. This focuses on finding the **regions** themselves.
    - Primarily involves techniques like:
        - **Thresholding:** Grouping pixels based on whether their intensity falls within certain ranges.
        - **Region Growing:** Starting from "seed" pixels and adding similar neighboring pixels.
        - **Region Splitting and Merging:** Recursively dividing or merging regions based on similarity criteria.
    - *Analogy:* Finding all the houses that are painted the same color.

*[Insert Image: Segmentation Approaches Diagram - From Page 3]*

---

## Detecting Discontinuities

- Focuses on finding isolated points, lines, and edges based on abrupt intensity changes.
- **Common Method:** Scan a small **mask** (kernel/template) over the image. The mask's coefficients are designed to detect a specific type of discontinuity.
- **Mask Operation:** The response $R$ of the mask at any point is calculated as the sum of products of the mask coefficients ($w_i$) and the corresponding image pixel intensities ($z_i$) under the mask.
  $$
  R = w_1 z_1 + w_2 z_2 + \dots + w_9 z_9 = \sum_{i=1}^{9} w_i z_i \quad \text{(for a 3x3 mask)}
  $$
  *[Insert Image: Mask Operation Formula & 3x3 Mask Coefficients - From Page 4]*

### Point Detection

*[Insert Image: Point Detection Mask and Example - From Page 5]*

- **Goal:** Detect isolated pixels whose intensity is significantly different from their neighbors.
- **Mask:** A typical point detection mask emphasizes the center pixel and de-emphasizes neighbors. Often looks like a Laplacian mask. Example 3x3 mask:
  $$
  \begin{bmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{bmatrix}
  $$
- **Detection:** A point is detected at the location where the mask is centered if the absolute value of the mask's response $|R|$ exceeds a certain non-negative threshold $T$:
  $$
  |R| \ge T
  $$
- **Application Example:** Finding pores or defects in an X-ray image of a turbine blade (Figure 10.2). (a) Mask, (b) X-ray image, (c) Result of applying mask (high response at point defect), (d) Thresholded result showing detected point.

### Line Detection

*[Insert Image: Line Detection Masks (Horizontal, Vertical, +/- 45 deg) - From Page 6]*
*[Insert Image: Line Detection Example (Wire Bond) - From Page 7]*

- **Goal:** Detect lines, typically one pixel wide, in an image. Slightly more common than point detection.
- **Masks:** Different masks are designed to detect lines in specific orientations. For digital images, common orientations are horizontal, vertical, +45°, and -45°. The masks have larger coefficients along the line direction they are designed to detect.
- **Process:** Apply each orientation mask separately to the image. If the response $|R|$ for a specific mask exceeds a threshold $T$ at a certain point, that point is considered likely part of a line in that orientation.
- **Example:** Detecting wire bonds in an electronic component (Figure 10.4). (a) Input image, (b) Response using the -45° detector mask, (c) Thresholded result showing detected -45° lines.

### Edge Detection

*[Insert Image: Edge Models (Ideal vs. Ramp) - From Page 8]*
*[Insert Image: Edge Profile and Derivatives - From Page 9]*

- **Concept:** Edges are significant local changes in image intensity, usually associated with the boundary between two different regions or objects. They are the most common type of discontinuity used for segmentation.
- **Edge Models:**
    - **Ideal Edge (Step Edge):** An instantaneous change in intensity. Represents a perfect, sharp boundary.
    - **Ramp Edge:** A gradual change in intensity over a finite distance. More realistic due to blurring in real images. The slope of the ramp is proportional to the degree of blurring.
- **Detection using Derivatives:** Edges correspond to locations of high intensity change, which can be detected using derivatives.
    - **First Derivative:** The magnitude of the first derivative (gradient) is high at an edge. It produces a peak (or thick edge).
        - Positive at the leading edge of transition.
        - Negative at the trailing edge of transition.
        - Zero in constant intensity areas.
    - **Second Derivative:** The second derivative (Laplacian) has a **zero-crossing** at the midpoint of a ramp edge (or produces a double edge for step edges).
        - Positive on the darker side of the edge.
        - Negative on the lighter side of the edge.
- **Effect of Noise:** Derivatives are very sensitive to noise, as noise introduces many small, rapid intensity changes.
    *[Insert Image: Effect of Noise on Edge Profiles and Derivatives - From Pages 10 & 11]*
    - Noise makes it harder to detect true edges based solely on derivative values. Smoothing is often necessary.

#### Gradient Operators (First-Order Derivatives)

*[Insert Image: Gradient Vector, Magnitude, Direction Formulas - From Page 12]*

- The **gradient** of an image $f(x, y)$ provides information about the magnitude and direction of the maximum intensity change at location $(x, y)$.
- **Gradient Vector:**
  $$
  \nabla f = \begin{bmatrix} G_x \\ G_y \end{bmatrix} = \begin{bmatrix} \frac{\partial f}{\partial x} \\ \frac{\partial f}{\partial y} \end{bmatrix}
  $$
  Where $G_x$ and $G_y$ are the derivatives (approximated digitally) in the x and y directions.
- **Gradient Magnitude (Edge Strength):** Represents the strength of the edge.
  $$
  |\nabla f| = \text{mag}(\nabla f) = \sqrt{G_x^2 + G_y^2}
  $$
  Often approximated for computational efficiency as $|\nabla f| \approx |G_x| + |G_y|$.
- **Gradient Direction (Edge Direction):** The angle of maximum intensity change, perpendicular to the edge itself.
  $$
  \alpha(x, y) = \tan^{-1}\left(\frac{G_y}{G_x}\right)
  $$
  (atan2 function is preferred for correct quadrant).

##### Common Gradient Masks (Digital Approximations)

- These masks approximate the partial derivatives $G_x$ and $G_y$.
- **Roberts Cross-Gradient Operators:** (2x2 masks)
    - $G_x \approx z_9 - z_5$ (using Fig 10.1 numbering) or mask: $[0, 1; -1, 0]$ (approx diagonal diff)
    - $G_y \approx z_8 - z_6$ or mask: $[1, 0; 0, -1]$ (approx other diagonal diff)
    *[Insert Image: Roberts Masks - From Page 13]*
- **Prewitt Operators:** (3x3 masks)
    - Approximates derivative using differences between adjacent rows/columns.
    - $G_x$ (vertical edges): $\begin{bmatrix} -1 & 0 & 1 \\ -1 & 0 & 1 \\ -1 & 0 & 1 \end{bmatrix}$
    - $G_y$ (horizontal edges): $\begin{bmatrix} -1 & -1 & -1 \\ 0 & 0 & 0 \\ 1 & 1 & 1 \end{bmatrix}$
    *[Insert Image: Prewitt Horizontal/Vertical Masks - From Page 13]*
    - Also includes masks for diagonal edges.
    *[Insert Image: Prewitt Diagonal Masks - From Page 14]*
- **Sobel Operators:** (3x3 masks)
    - Similar to Prewitt but gives more weight to the center pixels, providing some smoothing. Generally preferred over Prewitt.
    - $G_x$ (vertical edges): $\begin{bmatrix} -1 & 0 & 1 \\ -2 & 0 & 2 \\ -1 & 0 & 1 \end{bmatrix}$
    - $G_y$ (horizontal edges): $\begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ 1 & 2 & 1 \end{bmatrix}$
    *[Insert Image: Sobel Horizontal/Vertical Masks - From Page 13]*
    - Also includes masks for diagonal edges.
    *[Insert Image: Sobel Diagonal Masks - From Page 14]*

##### Gradient Operator Example

*[Insert Image: Gradient Example (Building) - From Page 15]*
*[Insert Image: Gradient Example (Smoothed Building) - From Page 16]*
*[Insert Image: Diagonal Gradient Example (Building) - From Page 17]*

- Shows an original image (a), the $G_x$ component (b), the $G_y$ component (c), and the gradient magnitude $|\nabla f| \approx |G_x| + |G_y|$ (d).
- Page 16 shows the same process applied after smoothing the original image with a 5x5 averaging filter, reducing noise in the gradient components.
- Page 17 shows results using Sobel diagonal masks.

#### Laplacian Operator (Second-Order Derivative)

*[Insert Image: Laplacian Formula and Masks - From Page 18]*

- The **Laplacian** is a scalar operator defined as the sum of the second partial derivatives.
- **Formula:**
  $$
  \nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2}
  $$
- **Properties:**
    - Rotationally invariant (responds equally to edges in all directions).
    - Produces **zero-crossings** at the center of edges.
    - More sensitive to noise than the gradient.
- **Common Digital Masks:**
    - Mask 1 (4-neighbors): $\begin{bmatrix} 0 & -1 & 0 \\ -1 & 4 & -1 \\ 0 & -1 & 0 \end{bmatrix}$
    - Mask 2 (8-neighbors): $\begin{bmatrix} -1 & -1 & -1 \\ -1 & 8 & -1 \\ -1 & -1 & -1 \end{bmatrix}$ (Often preferred)

#### Laplacian of Gaussian (LoG)

*[Insert Image: Gaussian Function & LoG Formula - From Page 19]*
*[Insert Image: LoG 3D Plot, Cross Section, Mask Approximation - From Page 20]*

- **Concept:** Combines Gaussian smoothing with the Laplacian operator to reduce noise sensitivity while still detecting edges via zero-crossings.
- **Steps:**
    1. Smooth the image $f(x,y)$ with a Gaussian filter $h(x,y)$.
       $$ h(r) = e^{-\frac{r^2}{2\sigma^2}} \quad \text{where } r^2 = x^2 + y^2 $$
    2. Compute the Laplacian of the smoothed image $\nabla^2 (h * f)$.
- **LoG Function (Mexican Hat):** The Laplacian applied directly to the Gaussian function itself:
  $$
  \nabla^2 h(r) = -\left[ \frac{r^2 - \sigma^2}{\sigma^4} \right] e^{-\frac{r^2}{2\sigma^2}}
  $$
  This function looks like an inverted sombrero or "Mexican hat".
- **Mask Approximation:** The LoG operator can be approximated by a single mask, like the 5x5 mask shown on page 20.
- **Edge Detection:** Edges correspond to the **zero-crossings** in the LoG-filtered image.

##### LoG Example

*[Insert Image: LoG Example Comparison (Artery) Pt1 - From Page 21]*
*[Insert Image: LoG Example Comparison (Artery) Pt2 - From Page 22]*

- Shows an original image (a), Sobel gradient (b) for comparison.
- Shows Gaussian smoothing function and Laplacian mask.
- Shows the LoG filtered image (e). Note the gray level represents zero, white is positive, black is negative.
- Shows thresholded LoG (f) - not very useful.
- Shows **zero-crossings** of the LoG image (g), which accurately locate the edges.

---

## Edge Linking and Boundary Detection

- Edge detection algorithms typically output pixels that are *potential* edge points (edge fragments).
- **Edge linking** aims to assemble these fragments into meaningful object boundaries.

### Local Processing Approach

*[Insert Image: Edge Linking Criteria - From Page 23]*

- **Idea:** Examine pixels in a local neighborhood (e.g., 3x3 or 5x5) around a potential edge pixel $(x,y)$. Link $(x,y)$ to a neighboring pixel $(x_0, y_0)$ if they have similar properties.
- **Useful Properties:**
    1.  **Edge Strength (Magnitude):** Link points if their gradient magnitudes are similar.
        $$ |\nabla f(x,y) - \nabla f(x_0, y_0)| \le E $$
        where $E$ is a non-negative threshold.
    2.  **Edge Direction:** Link points if their gradient directions are similar.
        $$ |\alpha(x,y) - \alpha(x_0, y_0)| < A $$
        where $A$ is a non-negative angle threshold.
- **Process:** Start from edge points and connect them to similar neighbors to form edge chains.

#### Local Processing Example

*[Insert Image: Edge Linking Example (Van) - From Page 24]*

- Shows input image (a), Gy component (b), Gx component (c).
- Shows the result of edge linking (d) based on local magnitude and direction similarity. The license plate boundary becomes more clearly defined after linking isolated edge pixels.

### Handling Noise in Edge Detection

*[Insert Image: Noisy Edge Profile & Derivative - From Page 26]*

- As seen before, derivatives are highly sensitive to noise. The derivative of a noisy edge can be very messy, making it difficult to locate the true edge peak.

#### Solution: Smooth First (Derivative Theorem of Convolution)

*[Insert Image: Smoothing First Concept & Plots - From Page 27]*
*[Insert Image: Derivative Theorem of Convolution - From Page 28]*

- **Idea:** Smooth the image *before* taking the derivative.
    - Convolution with a smoothing kernel (e.g., Gaussian $h$) reduces noise.
    - Taking the derivative of the smoothed signal $\frac{\partial}{\partial x}(h * f)$ gives a cleaner peak indicating the edge location.
- **Derivative Theorem of Convolution:** The derivative of a convolution is the convolution of the derivative:
  $$
  \frac{\partial}{\partial x} (h * f) = \left( \frac{\partial h}{\partial x} \right) * f
  $$
- **Advantage:** Instead of smoothing the whole image then taking the derivative (two operations), we can pre-compute the derivative of the smoothing kernel ($\frac{\partial h}{\partial x}$) and convolve the original image with this single kernel. Saves one operation.

#### Laplacian of Gaussian (LoG) Revisited

*[Insert Image: LoG as Derivative of Convolution - From Page 29]*

- Applying the derivative theorem twice leads to the LoG approach:
  $$
  \nabla^2 (h * f) = (\nabla^2 h) * f
  $$
- We convolve the image $f$ with the **Laplacian of Gaussian** kernel ($\nabla^2 h$, the "Mexican Hat").
- Edges are located at the **zero-crossings** of the result $(\nabla^2 h) * f$.

### Canny Edge Detector

*[Insert Image: Canny Steps Formulas - From Page 30]*
*[Insert Image: Non-Maximum Suppression Diagram - From Page 31]*

- A widely used and effective edge detection algorithm that aims to achieve:
    1.  **Good Detection:** Find as many real edges as possible.
    2.  **Good Localization:** Detected edge points should be as close as possible to the center of the true edge.
    3.  **Single Response:** Only one response to a single edge (avoid multiple detections).
- **Steps:**
    1.  **Smooth Image:** Convolve the input image $I$ with a 2D Gaussian filter $G$ to reduce noise. Result: $G * I$.
    2.  **Find Gradient:** Compute the gradient magnitude $|\nabla(G*I)|$ and direction $\alpha = \text{atan2}(G_y, G_x)$ for each pixel, typically using Sobel-like approximations on the smoothed image.
    3.  **Non-Maximum Suppression (NMS):** Thin the wide ridges around edges in the gradient magnitude image down to single-pixel width.
        - For each pixel $q$, check its gradient magnitude against the magnitude of its neighbors in the positive and negative gradient directions ($\vec{n}$).
        - If the magnitude at $q$ is *not* greater than the magnitude at its neighbors along the gradient direction (interpolated values p and r might be needed), suppress (set to zero) the magnitude at $q$.
        - This keeps only the local maxima along the gradient direction.
    4.  **(Hysteresis Thresholding - Not explicitly shown but crucial part of Canny):** Apply two thresholds, $T_{low}$ and $T_{high}$.
        - Pixels with magnitude above $T_{high}$ are strong edge pixels (definitely edges).
        - Pixels with magnitude below $T_{low}$ are suppressed (definitely not edges).
        - Pixels with magnitude between $T_{low}$ and $T_{high}$ are weak edge pixels. Keep a weak edge pixel *only if* it is connected (8-connectivity) to a strong edge pixel. This helps link edges while removing isolated noise responses.
- **Canny Relationship to LoG:** Locating edges by finding zero-crossings along the edge normal direction (step 4 in slide formula) is related to finding zero-crossings of the second derivative in that direction, similar in principle to LoG but applied directionally after NMS.

#### Canny Edge Detector Example (Lena)

*[Insert Image: Canny Example - Original Lena - From Page 32]*
*[Insert Image: Canny Example - Gradient Magnitude - From Page 33]*
*[Insert Image: Canny Example - After Non-Maximum Suppression (and Hysteresis) - From Page 34]*

- Shows the steps visually: Original -> Gradient Magnitude -> Final Edge Map (after NMS and thresholding). The final result shows thin, well-localized edges.

### Global Processing via the Hough Transform

*[Insert Image: Hough Transform Introduction (Canny + Girl) - From Page 35]*
*[Insert Image: Hough Transform y=ax+b Concept - From Page 36]*

- **Purpose:** A global technique for edge linking, particularly effective for finding features with specific shapes (lines, circles, etc.) even if they are broken or noisy. It uses information from all edge points simultaneously.
- **Prerequisite:** Typically applied to an **edge image** (output of an edge detector like Canny) where potential boundary points are marked.
- **Focus:** Finding edge points that lie along a **straight line**.

#### Hough Transform: $y = ax + b$ Representation

- **Idea:** A point $(x_i, y_i)$ in the image space corresponds to a line in the parameter space (Hough space). For the line equation $y = ax + b$, the parameters are slope $a$ and intercept $b$.
- **Mapping:** Rewrite the equation as $b = -x_i a + y_i$. This is the equation of a line in the $ab$-plane (parameter space).
    - Each point $(x_i, y_i)$ in the image maps to a line $b = -x_i a + y_i$ in the $ab$-plane.
- **Collinearity:** Points $(x_i, y_i)$ and $(x_j, y_j)$ that lie on the *same* line $y = a_0 x + b_0$ in the image space will produce lines in the $ab$-plane that *intersect* at the point $(a_0, b_0)$.
- **Process:**
    1. Quantize the parameter space ($ab$-plane) into an **accumulator array**. Initialize all cells to zero.
    2. For each edge point $(x_i, y_i)$ in the image:
        - Generate the line $b = -x_i a + y_i$ in the $ab$-plane.
        - Increment the count in all accumulator cells that this line passes through.
    3. Find accumulator cells with high counts. These "peaks" correspond to lines $(a_k, b_k)$ that pass through many edge points in the image.

#### Example ($y=ax+b$)

*[Insert Image: Hough Example y=ax+b - Points & Equations - From Page 37]*
*[Insert Image: Hough Example y=ax+b - Table for a=0, a=1 - From Page 38]*
*[Insert Image: Hough Example y=ax+b - Plot in ab-plane - From Page 39]*
*[Insert Image: Hough Example y=ax+b - Intersection & Result Line - From Page 40]*

- Given points A(1,4), B(2,3), C(3,1), D(4,1), E(5,0).
- Each point $(x, y)$ defines a line $b = -ax + y$ in the $ab$-plane.
    - A: $b = -a + 4$
    - B: $b = -2a + 3$
    - C: $b = -3a + 1$
    - D: $b = -4a + 1$
    - E: $b = -5a + 0$
- Plotting these lines in the $ab$-plane shows they (mostly) intersect near the point $(-1, 5)$.
- This intersection point corresponds to the parameters $a=-1$ and $b=5$.
- The line equation linking the points is $y = -1x + 5$ or $y = -x + 5$.

#### Flaw of $y=ax+b$ Representation & Normal Form

*[Insert Image: Hough Transform Flaw & Normal Form Intro - From Page 41]*
*[Insert Image: Hough Transform Normal Form Diagram & Explanation - From Page 42]*

- **Flaw:** The slope $a$ becomes infinite for **vertical lines**. This requires infinite memory in the accumulator array.
- **Solution: Normal Parameterization:** Represent the line using its normal vector from the origin.
  $$
  \rho = x \cos(\theta) + y \sin(\theta)
  $$
  Where:
    - $\rho$ (rho): The perpendicular distance from the origin to the line.
    - $\theta$ (theta): The angle of the normal vector with respect to the positive x-axis.
- **Parameter Space:** The Hough space is now the $(\rho, \theta)$ plane.
- **Mapping:** Each edge point $(x_i, y_i)$ in the image transforms into a **sinusoidal curve** in the $(\rho, \theta)$ plane, defined by $\rho = x_i \cos(\theta) + y_i \sin(\theta)$.
- **Collinearity:** Edge points lying on the same line (with parameters $\rho_0, \theta_0$) in the image space will produce sinusoidal curves that **intersect** at the point $(\rho_0, \theta_0)$ in the Hough space.
- **Process:**
    1. Quantize the $(\rho, \theta)$ parameter space into an accumulator array.
    2. For each edge point $(x_i, y_i)$:
        - For each possible value of $\theta$ (e.g., 0° to 180°):
            - Calculate the corresponding $\rho = x_i \cos(\theta) + y_i \sin(\theta)$.
            - Increment the accumulator cell $(\rho, \theta)$.
    3. Find peaks (cells with high counts) in the accumulator array. These peaks $(\rho_k, \theta_k)$ represent the parameters of the dominant lines in the image.

#### Example (Normal Form)

*[Insert Image: Hough Example Normal Form - Input Grid & Equations - From Page 43]*
*[Insert Image: Hough Example Normal Form - Hough Space Plot - From Page 44]*
*[Insert Image: Hough Example Normal Form - Detected Line & Result - From Page 45]*

- Shows an input grid with 5 marked points (pixels): (0,5), (1,4), (3,2), (3,3), (5,0). *(Note: Point (3,3) seems added, others match previous example)*
- For each point $(x,y)$, the equation $\rho = x \cos(\theta) + y \sin(\theta)$ is generated.
- These equations are plotted as curves in the $(\rho, \theta)$ plane (Hough space).
- The curves corresponding to the collinear points (0,5), (1,4), (3,2), (5,0) intersect at a peak, found to be around $\theta' = 45^\circ$ and $\rho' = 3.4$.
- This peak identifies the parameters of the line passing through those points.
- The point (3,3) does not lie on this line, and its curve does not pass through the main intersection point.

---

## Thresholding (Revisited as Similarity-Based Segmentation)

- Thresholding can also be viewed as a basic form of similarity-based segmentation, grouping pixels based on whether their intensity values fall into defined ranges (similarity to predefined thresholds).

*[Insert Image: Thresholding Histograms (Single vs Multiple) - From Page 46]*

- **Basic Assumption:** Objects of interest have intensity levels that are distinct (different range) from the background.
- **Types:**
    - **Single Threshold (Global):** Use one threshold $T$ to separate objects from background. $g(x,y) = 1$ if $f(x,y) > T$, else $0$. Effective when object/background intensities are clearly separated (bimodal histogram).
    - **Multiple Thresholds:** Use multiple thresholds $T_1, T_2, ...$ to partition the image into several classes based on intensity ranges.

### Role of Illumination in Thresholding

*[Insert Image: Role of Illumination - Reflectance Image & Histogram - From Page 47]*
*[Insert Image: Role of Illumination - Reflectance, Illumination, Product Image & Histograms - From Page 48]*

- **Problem:** Non-uniform illumination significantly complicates thresholding.
- **Model:** Image $f(x,y) = i(x,y) \times r(x,y)$, where $i$ is illumination and $r$ is reflectance.
- **Effect:** If illumination $i(x,y)$ varies across the image, the same object reflectance $r(x,y)$ will produce different image intensities $f(x,y)$ in different locations.
- **Histogram Impact:** A simple object/background reflectance histogram (bimodal) can become complex and unimodal (or have merged peaks) when multiplied by varying illumination, making it difficult or impossible to find a single global threshold that works for the entire image.

### Basic Global Thresholding

*[Insert Image: Global Thresholding Example (Characters) - From Page 49]*
*[Insert Image: Global Thresholding Example (Fingerprint) - From Page 50]*

- Apply a single threshold $T$ to the entire image.
- **Choosing T:**
    - **Manual:** Select based on visual inspection or histogram analysis.
    - **Automatic (Iterative):**
        1. Select an initial estimate for $T$ (e.g., midway between min and max intensity).
        2. Segment the image using $T$ into two groups: $G_1$ (pixels > T) and $G_2$ (pixels <= T).
        3. Compute the average intensity values $\mu_1$ and $\mu_2$ for the pixels in $G_1$ and $G_2$.
        4. Compute a new threshold $T = \frac{1}{2}(\mu_1 + \mu_2)$.
        5. Repeat steps 2-4 until $T$ converges (stops changing significantly).
- **Works well when:** Object and background histograms are clearly separated and illumination is relatively uniform.

### Basic Adaptive Thresholding

*[Insert Image: Adaptive Thresholding Problem & Example - From Page 51]*
*[Insert Image: Adaptive Thresholding Problem Detail - From Page 52]*
*[Insert Image: Adaptive Thresholding Solution (Subdivision) - From Page 53]*

- **Need:** Required when illumination varies significantly across the image, causing a single global threshold to fail.
- **Concept:** The threshold value $T$ is varied dynamically over the image based on local characteristics.
- **Approach (Subdivision):**
    1. Divide the image into smaller subimages.
    2. Determine a threshold for each subimage independently (e.g., using histogram analysis or iterative method within the subimage).
    3. Apply the locally determined threshold to segment that subimage.
- **Result:** Can successfully segment objects even under non-uniform illumination where global thresholding fails.

### Optimal Global and Adaptive Thresholding (e.g., Otsu's Method)

*[Insert Image: Optimal Thresholding Concept (PDFs) - From Page 54]*

- **Concept:** Treats pixel intensities as coming from probability density functions (PDFs), one for the object ($p_1(z)$) and one for the background ($p_2(z)$).
- **Goal:** Find the threshold $T$ that **minimizes the probability of misclassifying** pixels.
- **Errors:**
    - Mislabeling an object pixel as background.
    - Mislabeling a background pixel as object.
- **Otsu's Method:** A popular technique that finds the optimal threshold by minimizing the intra-class variance (or maximizing the inter-class variance) between the two groups (object and background) created by the threshold. It's computationally efficient as it only uses the histogram.

### Other Thresholding Approaches

- **Using Boundary Characteristics:** Incorporate edge information (e.g., high gradient magnitude near the boundary) to help select thresholds or refine the thresholded result.
  *[Insert Image: Boundary Characteristics Thresholding Example (Check) - From Page 55]*
- **Thresholds Based on Several Variables:** Use multiple features per pixel for thresholding, especially useful for color images (e.g., thresholding based on R, G, and B values or other color space components).
  *[Insert Image: Multivariate Thresholding Example (Color Image) - From Page 56]*

---

## Region-Based Segmentation

*[Insert Image: Region-Based Segmentation Introduction - From Page 57]*
*[Insert Image: Region Segmentation Example (Grapes) - From Page 58]*
*[Insert Image: Region Segmentation Example (Beach) - From Page 59]*

- **Motivation:** Edge detection and thresholding may not work well if edges are noisy/broken or if intensity levels overlap significantly between regions.
- **Concept:** Group pixels into regions based on **similarity** and **connectivity**.
- **Requirements for Regions:**
    - **Uniformity:** Pixels within a region must be similar according to a predefined **predicate** or **homogeneity criterion** (e.g., similar gray level, color, texture).
    - **Connectivity:** Pixels within a region must be connected.
- **Main Approaches:**
    1.  **Region Growing:** Bottom-up approach. Start small and grow.
    2.  **Region Splitting:** Top-down approach. Start large and divide.
    3.  **Region Splitting and Merging:** Combination of both.

### Basic Formulation

*[Insert Image: Region Segmentation Formal Definition - From Page 60]*

Let $R$ represent the entire image region. Segmentation partitions $R$ into $n$ subregions $R_1, R_2, \dots, R_n$ such that:
(a) $\bigcup_{i=1}^{n} R_i = R$ (Every pixel belongs to a region).
(b) $R_i$ is a connected region, for $i=1, 2, \dots, n$.
(c) $R_i \cap R_j = \phi$ for all $i \neq j$ (Regions are disjoint).
(d) $P(R_i) = \text{TRUE}$ for $i=1, 2, \dots, n$ (Each region satisfies the homogeneity predicate $P$).
(e) $P(R_i \cup R_j) = \text{FALSE}$ for any adjacent regions $R_i$ and $R_j$ (Merging adjacent regions would violate the predicate).

- **Predicate $P(R_k)$:** A logical function determining if region $R_k$ is homogeneous.
    - *Example:* $P(R_k) = \text{TRUE}$ if all pixels in $R_k$ have the same gray level, or if the standard deviation of gray levels in $R_k$ is below a threshold, or if the range (max-min) is below a threshold.

### Region Growing

*[Insert Image: Region Growing Definition - From Page 61]*
*[Insert Image: Region Growing Numerical Example - From Page 62]*
*[Insert Image: Region Growing Step-by-Step Visual - From Page 63]*
*[Insert Image: Region Growing Weld Example (Problem & Histogram) - From Page 64]*
*[Insert Image: Region Growing Weld Example (Results) - From Page 65]*

- **Concept:** A procedure that groups pixels or subregions into larger regions based on predefined criteria. Starts from "seed" points and grows.
- **Simplest Approach: Pixel Aggregation:**
    1. Start with a set of **seed points** (can be chosen manually or automatically).
    2. For each seed, examine its **neighboring pixels**.
    3. Add a neighbor to the region if it satisfies the **similarity predicate** (e.g., gray level difference from the seed or region mean is below a threshold, same color class, etc.).
    4. Newly added pixels become candidates for growing the region further.
    5. Continue until no more pixels can be added to any region.
- **Similarity Criteria:** Based on intensity, gray level, color, texture, shape, etc.
- **Advantages:**
    - Good for segmenting regions with similar properties, especially when boundaries are noisy or weak.
    - Can often perform better than edge-based methods in noisy images.
- **Challenges:** Selecting appropriate seed points and similarity criteria. Order of processing neighbors can affect the result.
- **Example (Numerical):**
    - Seed point: Center pixel with value 60.
    - Threshold: Intensity difference <= 10.
    - The region grows iteratively by adding neighbors whose values are within 10 of a pixel already in the growing region.
- **Example (Weld Defects):**
    - Shows an image where defects are hard to segment by thresholding due to overlapping intensities (Fig 10.41 histogram).
    - Region growing (Fig 10.40) successfully segments the defects starting from seed points (b), resulting in segmented regions (c) and boundaries (d).

### Region Splitting and Merging

#### Region Splitting

*[Insert Image: Region Splitting Concept - From Page 66]*
*[Insert Image: Region Splitting Quadtree - From Page 67]*
*[Insert Image: Region Splitting Example (Numerical + Quadtree) - From Page 68]*

- **Concept:** Opposite of region growing (top-down).
    1. Start with a large region (often the entire image).
    2. Test if the region is **uniform** based on a predicate $P$.
    3. If the region is **not** uniform, **split** it into subregions (e.g., four quadrants).
    4. Recursively apply steps 2 and 3 to each subregion until all resulting regions are uniform.
- **Challenge:** Determining where and how to split the region.
- **Common Method: Quadtree Decomposition:**
    - Split a square region into four equal square quadrants.
    - This creates a **quadtree** structure where each node represents a region, and non-leaf nodes have exactly four children representing the sub-quadrants.
- **Predicate Example:** Region is uniform if `max intensity - min intensity <= Threshold`.

#### Region Merging

*[Insert Image: Region Merging Concept & Example - From Page 69]*

- **Concept:** Opposite of splitting (bottom-up). Often applied *after* an initial splitting phase or over-segmentation.
    1. Start with an initial segmentation (e.g., result of splitting, or even individual pixels).
    2. Consider adjacent regions $R_i$ and $R_j$.
    3. If $R_i \cup R_j$ satisfies the homogeneity predicate $P$, **merge** them into a single larger region.
    4. Repeat until no more merges are possible.
- **Predicate Example:** Merge regions if the difference in their mean intensities is below a threshold, or if the merged region's variance/range is below a threshold.

#### Split and Merge Algorithm

*[Insert Image: Split and Merge Algorithm Steps - From Page 70]*
*[Insert Image: Region Grow Result Example (Lena) - From Page 71]*
*[Insert Image: Region Split Result Example (Lena) - From Page 72]*
*[Insert Image: Split and Merge Result Example (Lena) - From Page 73]*

- Combines the top-down splitting and bottom-up merging approaches.
- **Algorithm:**
    1. **Start:** Consider the entire image as one region $R$. Define a homogeneity predicate $P$.
    2. **Split Phase:** If $P(R)$ is FALSE, split $R$ into four quadrants. Repeat this recursively for any quadrant $R_k$ where $P(R_k)$ is FALSE. Stop when all resulting regions $R_i$ satisfy $P(R_i) = TRUE$. (Result is often over-segmented).
    3. **Merge Phase:** Check any two adjacent regions $R_i, R_j$ from the splitting phase. If $P(R_i \cup R_j) = TRUE$, merge them. Repeat until no more adjacent regions can be merged.
- **Advantages:** Can handle complex regions better than splitting or growing alone.

---

## Boundary Descriptors

- Once regions are segmented, we often need to represent their **boundaries** for shape analysis or recognition.

### Chain Codes

*[Insert Image: Chain Code Directions (4 & 8) - From Page 74]*
*[Insert Image: Chain Code Resampling & Example - From Page 75]*

- **Concept:** Represent an object boundary as a connected sequence of straight-line segments of specified length and direction.
- **Process:**
    1. Define a grid (usually the pixel grid or a resampled coarser grid).
    2. Select a starting point on the boundary.
    3. Traverse the boundary, recording the direction to the next boundary pixel using a predefined numbering scheme.
- **Direction Schemes:**
    - **4-directional:** Uses codes 0, 1, 2, 3 for East, North, West, South movements.
    - **8-directional:** Uses codes 0-7 for movements in 8 directions (E, NE, N, NW, W, SW, S, SE).
- **Resampling:** To reduce noise sensitivity and shorten long codes, the boundary can be resampled on a coarser grid before generating the chain code.
- **Properties:** Very compact representation, captures shape information.

#### Problem: Starting Point Dependence & Rotation Invariance

*[Insert Image: Chain Code First Difference - From Page 76]*

- **Problem:** The chain code sequence depends on the chosen starting point.
- **Solution (Normalization):**
    1. Treat the chain code as a **circular sequence** (connect the end back to the start).
    2. Find the **first difference** of the chain code: Calculate the number of direction changes (counterclockwise turns) between consecutive elements.
        - *Example:* If code is `101...`, first element of difference is `(0-1) mod 4 = 3` for 4-dir, or `(0-1) mod 8 = 7` for 8-dir.
    3. The first difference code is **rotationally invariant**.
    4. To make it **starting-point invariant**, find the circular shift of the first difference code that results in the integer of **minimum magnitude**. This minimum magnitude sequence is the normalized representation.

### Shape Numbers

*[Insert Image: Shape Number Definition & Example - From Page 77]*
*[Insert Image: Shape Number Examples (Order 4, 6, 8) - From Page 78]*

- **Definition:** The **shape number** of a boundary is defined as the first difference chain code normalized to the minimum magnitude (as described above).
- **Order:** The **order** of a shape number is the number of digits in the sequence (related to the boundary length/complexity).
- **Properties:** Provides a representation that is invariant to starting point and rotation. Used for shape classification.

### Signatures

*[Insert Image: Signature Concept & Examples (Circle, Square) - From Page 79]*

- **Concept:** A 1-Dimensional functional representation of a boundary. Reduces the 2D boundary to a 1D function.
- **Simple Method:** Plot the **distance** from the object's **centroid** (center of mass) to the boundary points as a function of the **angle** relative to the centroid.
    - $s(\theta) = \text{distance from centroid to boundary at angle } \theta$.
- **Properties:** Simple to compute. Dependent on starting angle and orientation unless normalized. Can be sensitive to noise.

### Image Moments

*[Insert Image: Image Moments Definition - From Page 80]*
*[Insert Image: Zeroth Moment (Area) - From Page 81]*
*[Insert Image: Centroid Calculation using Moments - From Page 82]*
*[Insert Image: Moment Calculation Example (Binary Image) - From Page 83]*
*[Insert Image: Central Moments Definition - From Page 84]*
*[Insert Image: Central Moments Formulas - From Page 85]*

- **Concept:** Image moments are statistical parameters (scalar values) calculated from the image pixels that describe the distribution of pixel intensities and their spatial locations. They can characterize properties like area, position, orientation, and shape.
- **Spatial Moments (Geometric Moments):**
  $$
  M_{ij} = \sum_{x} \sum_{y} x^i y^j I(x, y)
  $$
  Where $I(x,y)$ is the pixel intensity at $(x,y)$, and $(i,j)$ define the order of the moment.
- **Zeroth Order Moment ($M_{00}$):**
  $$
  M_{00} = \sum_{x} \sum_{y} I(x, y)
  $$
    - For a **binary image** ($I=0$ or $1$), $M_{00}$ is the count of non-zero pixels, which corresponds to the **area** of the object.
    - For a **grayscale image**, $M_{00}$ is the sum of all pixel intensities (total "mass").
- **First Order Moments ($M_{10}, M_{01}$):** Used to find the **centroid** (center of mass) $(\bar{x}, \bar{y})$ of the object.
  $$
  \bar{x} = \frac{M_{10}}{M_{00}} = \frac{\sum_x \sum_y x I(x, y)}{\sum_x \sum_y I(x, y)}
  $$
  $$
  \bar{y} = \frac{M_{01}}{M_{00}} = \frac{\sum_x \sum_y y I(x, y)}{\sum_x \sum_y I(x, y)}
  $$
- **Central Moments ($\mu_{pq}$):** Moments calculated with respect to the centroid. They are **translation invariant**.
  $$
  \mu_{pq} = \sum_{x} \sum_{y} (x - \bar{x})^p (y - \bar{y})^q I(x, y)
  $$
  - Formulas for central moments up to order 3 are derived from spatial moments $M_{ij}$.
- **Higher Order Moments & Invariants:** Central moments can be further normalized (scaled) to achieve scale invariance, and combinations of normalized central moments (**Hu moments**) can be derived that are invariant to translation, scale, and rotation. These are powerful shape descriptors.

---

## Summary & Key Concepts

- **Segmentation Goal:** Partition image into meaningful connected regions (objects).
- **Approaches:**
    - **Discontinuity:** Find boundaries (points, lines, edges) using masks (Gradient, Laplacian, LoG). Sensitive to noise, requires smoothing (e.g., Canny). Edge linking connects fragments (local similarity, Hough transform).
    - **Similarity:** Group similar pixels.
        - **Thresholding:** Simple, based on intensity (Global, Adaptive, Optimal). Affected by illumination.
        - **Region Growing:** Bottom-up, needs seeds and similarity criteria. Good for noisy images.
        - **Region Splitting/Merging:** Top-down/Bottom-up, uses homogeneity predicate (Quadtree).
- **Boundary Description:** Represent segmented regions.
    - **Chain Codes:** Sequence of directions (4/8). Normalized for invariance (first difference, shape number).
    - **Signatures:** 1D representation (e.g., distance vs. angle).
    - **Moments:** Statistical descriptors (Area, Centroid, Central Moments). Basis for invariant shape features.

---

## Glossary (Chapter 10)

- **Image Segmentation:** Partitioning an image into multiple meaningful regions.
- **Region:** A set of connected pixels sharing a common property.
- **Discontinuity:** Abrupt change in image intensity or property (point, line, edge).
- **Similarity:** Shared characteristics within a region (intensity, color, texture).
- **Edge:** Boundary between two regions with different properties.
- **Mask (Kernel):** Small array used to detect features by convolution/correlation.
- **Gradient ($\nabla f$):** Vector indicating magnitude and direction of max intensity change.
- **Gradient Magnitude:** Strength of the intensity change (edge strength).
- **Gradient Direction:** Direction of the maximum intensity change.
- **Roberts, Prewitt, Sobel Operators:** Specific masks for approximating image gradients.
- **Laplacian ($\nabla^2 f$):** Second-order derivative operator, detects edges at zero-crossings.
- **Laplacian of Gaussian (LoG):** Combined Gaussian smoothing and Laplacian operation, detects edges at zero-crossings, less noise sensitive. ("Mexican Hat" filter).
- **Zero-Crossing:** Location where the sign of a function (e.g., Laplacian) changes.
- **Edge Linking:** Connecting detected edge fragments into continuous boundaries.
- **Derivative Theorem of Convolution:** Allows combining smoothing and derivative into a single filter kernel.
- **Canny Edge Detector:** Optimal edge detector aiming for good detection, localization, and single response; involves smoothing, gradient calculation, non-maximum suppression, and hysteresis thresholding.
- **Non-Maximum Suppression (NMS):** Thinning edges by keeping only pixels with locally maximal gradient magnitude along the gradient direction.
- **Hysteresis Thresholding:** Using two thresholds (high and low) to link strong edge pixels to connected weak edge pixels.
- **Hough Transform:** Global technique to detect shapes (lines, circles) by mapping image points to parameter space and finding peaks in an accumulator array.
- **Parameter Space (Hough Space):** Space representing the parameters of the shape being detected (e.g., $(a,b)$ or $(\rho,\theta)$ for lines).
- **Accumulator Array:** Grid in parameter space used to count "votes" from image points during Hough Transform.
- **Normal Form (Line):** Line representation $\rho = x \cos(\theta) + y \sin(\theta)$, avoids infinite slope problem.
- **Thresholding:** Segmentation based on comparing pixel intensity to threshold values (Global, Adaptive, Optimal).
- **Predicate (Homogeneity Criterion):** A rule defining whether a region is considered uniform (e.g., based on intensity range, variance).
- **Region Growing:** Bottom-up segmentation starting from seeds and adding similar neighbors.
- **Seed Point:** Initial starting point(s) for region growing.
- **Region Splitting:** Top-down segmentation recursively dividing non-uniform regions.
- **Quadtree:** Tree structure where each internal node has four children, used for region splitting.
- **Region Merging:** Bottom-up segmentation merging adjacent similar regions.
- **Boundary Descriptors:** Methods to represent the shape of a segmented region's boundary.
- **Chain Code:** Sequence of directional codes representing a boundary contour.
- **First Difference (Chain Code):** Sequence of direction changes, rotation invariant.
- **Shape Number:** Normalized first difference chain code, invariant to rotation and starting point.
- **Signature:** 1D function representing a 2D boundary (e.g., distance vs. angle).
- **Image Moments:** Statistical values describing pixel distribution (Spatial, Central). Used for area, centroid, shape description.
- **Centroid:** Center of mass of a region.
- **Central Moments:** Moments calculated relative to the centroid, translation invariant.
- **Hu Moments:** Set of seven moments derived from central moments, invariant to translation, scale, and rotation. (Not explicitly covered but related).

---

## Further Learning Resources

- **Digital Image Processing** by Gonzalez and Woods: Chapter 10 covers segmentation extensively. Chapter 11 covers Representation and Description (including boundary descriptors).
- **Computer Vision: Algorithms and Applications** by Richard Szeliski: Covers segmentation and feature description.
- **OpenCV Documentation:** Provides tutorials and function references for segmentation algorithms (thresholding, Canny, Hough, region growing - watershed, moments, contour analysis).
- **Scikit-Image Documentation:** Python library with implementations of Canny, thresholding methods (Otsu), region properties (moments), contours (chain codes).
