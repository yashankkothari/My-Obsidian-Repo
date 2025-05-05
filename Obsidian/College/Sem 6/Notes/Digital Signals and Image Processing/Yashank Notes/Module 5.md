Okay, here are your processed notes on Morphology and Image Compression, formatted for Obsidian and enriched according to your instructions.

# INTRODUCTION TO MORPHOLOGY AND IMAGE COMPRESSION

**(Paste Image: Title Slide from Page 1 here)**

*This opening slide introduces the two main topics covered in this section: Morphological Image Processing and Image Compression.*

---

## 5.1 Morphological Operations

**Morphological Operations** are a collection of non-linear operations related to the shape or morphology of features in an image. They are typically applied to **binary images** (images with only black and white pixels, often represented as 0s and 1s) but can be extended to grayscale images as well. These operations use a small shape or template called a **Structuring Element (SE)** to probe the image and modify it based on how the SE fits or interacts with the image features.

The fundamental morphological operations we will cover include:

1.  **Dilation:** Expands or thickens shapes.
2.  **Erosion:** Shrinks or thins shapes.
3.  **Opening:** Smoothes contours, breaks thin connections, removes small protrusions (erosion followed by dilation).
4.  **Closing:** Fills small holes, connects nearby objects, smoothes contours from the inside (dilation followed by erosion).
5.  **Hit or Miss Transform:** Detects specific patterns or shapes (template matching).
6.  **Boundary Extraction:** Finds the outer contour of shapes.

---

### Dilation

**Dilation** is a fundamental morphological operation that generally expands or thickens the foreground objects (typically represented by '1' or black pixels) in a binary image.

#### Process Description

1.  A **Structuring Element (SE)**, which is a small binary matrix (the template), is defined. It has an origin point (usually its center).
2.  The SE is conceptually **reflected** (though in practice, for symmetric SEs, this step is trivial).
3.  The reflected SE is then **shifted** across every pixel position of the input binary image (from left to right, top to bottom).
4.  At each position (shift) $x$, the algorithm checks if **any part** of the shifted, reflected SE overlaps with a foreground pixel ('1') in the input image $A$.
5.  If there is **any overlap**, the pixel in the *output* image corresponding to the *origin* (center) of the SE at that position $x$ is set to '1' (foreground/black).
6.  If there is no overlap at position $x$, the corresponding output pixel is set to '0' (background/white).

#### Mathematical Definition

The dilation of an image $A$ by a structuring element $B$, denoted $A \oplus B$, is defined as the set of all points $x$ such that the reflection of $B$, shifted by $x$, has a non-empty intersection with $A$.

$$ A \oplus B = \{x | (\hat{B})_x \cap A \neq \emptyset \} $$

Where:
-   $A$ is the input binary image (set of foreground pixel coordinates).
-   $B$ is the structuring element (set of foreground pixel coordinates relative to its origin).
-   $\oplus$ denotes the dilation operation.
-   $\hat{B}$ is the reflection of the structuring element $B$ about its origin.
-   $(\hat{B})_x$ represents the reflected structuring element $\hat{B}$ shifted (translated) so that its origin is at position $x$.
-   $\cap$ denotes the set intersection.
-   $\emptyset$ represents the empty set.
-   The condition $\neq \emptyset$ means "is not empty", signifying an overlap.

*Simplified Summary:* Think of dilation as "growing" the foreground regions. If the structuring element "touches" a foreground pixel when centered at a location, that location becomes foreground in the output.

**(Paste Image: Dilation Pixel Example from Page 4 here)**

*This image visually demonstrates dilation at the pixel level.
**Left Panel (Original Image):** Shows a shape made of dark blue foreground pixels on a light grid background.
**Right Panel (Processed Image With Dilated Pixels):** Shows the result after dilation. The original dark blue pixels remain, and new light green pixels have been added around the boundary. These light green pixels represent locations where the structuring element (implicitly a 3x3 square or cross here, centered on a background pixel) overlapped with at least one foreground pixel of the original shape, causing that background pixel location to become foreground in the dilated output. This visually confirms the "expansion" effect.*

#### Dilation Example: Character Thickening

**(Paste Image: Dilation 'A' Example from Page 5 here)**

*This example shows the effect of dilation on a binary image of the letter 'A'.
**Left:** The original binary image.
**Middle:** Result of dilation using a 3x3 square structuring element. The strokes of the 'A' are noticeably thicker.
**Right:** Result of dilation using a larger 5x5 square structuring element. The thickening effect is much more pronounced.
**Important Note:** The text specifies that in these examples, '1' refers to a **black** pixel, which is a common convention in binary image processing.*

*Real-world application:* This thickening can be useful in Optical Character Recognition (OCR) preprocessing to make characters more robust to noise or breaks, or in general image analysis to make features more prominent.

#### Dilation Example: Bridging Gaps in Text

**(Paste Image: Dilation Text Example from Page 6 here)**

*This practical example demonstrates a key application of dilation: repairing broken characters in scanned text.
**Left Panel (Original image):** Shows text where some characters have gaps or breaks (e.g., the 'e' and 'a' in 'year').
**Right Panel (After dilation):** Shows the result after applying dilation with the specified structuring element (a 3x3 pattern resembling a plus sign with corners filled). The dilation operation has effectively "bridged" the small gaps within the characters, making them appear more solid and connected. This can significantly improve the accuracy of subsequent OCR processing.*

#### What is Dilation For?

Dilation serves several purposes in image processing:

-   **Repairing Breaks:** It can connect parts of an object that are separated by small gaps.
-   **Repairing Intrusions:** It can fill small holes or indentations within an object.

**(Paste Image: Dilation Repair Examples from Page 7 here)**

*These diagrams illustrate the uses mentioned above:
**Top Pair:** Shows a ring with a break on the left. After dilation (right), the break is filled, restoring the solid ring shape.
**Bottom Pair:** Shows a solid circle with small internal holes ("intrusions") on the left. After dilation (right), these intrusions are filled in.
**Watch out:** A key characteristic (and potential side effect) of dilation is that it **enlarges objects**. The extent of enlargement depends on the size and shape of the structuring element.*

#### Dilation Example Walkthrough

This example details the step-by-step process of dilation.

**Problem:** Given an input image and a structuring element, find the dilated version.

**(Paste Image: Dilation Problem Setup from Page 8 here)**

*This image shows the input binary image (a fork-like shape) and the 2x2 structuring element (SE) to be used. The origin of the SE is typically marked, often the top-left or center; here, a dot indicates the origin in the bottom-left corner of the 2x2 SE.*

**Step 1:** Compare the structuring element with the input image at a specific point (often starting from the top-left). Check for overlap.

**(Paste Image: Dilation Step 1 from Page 9 here)**

*This image shows the SE positioned such that its origin aligns with a pixel in the input image. The dashed lines indicate the extent of the SE. An asterisk (*) marks a location where a '1' in the SE overlaps with a '1' in the input image. Because there is an overlap, the output pixel corresponding to the SE's origin is turned 'ON' (black) in the resultant image (shown on the right).*

**Steps 3 & 4 (Illustrative):** Shift the structuring element and repeat the overlap check.

**(Paste Image: Dilation Steps 3 & 4 from Page 10 here)**

*These images show the SE shifted to new positions (one step right, then another step right). In both positions shown, there is an overlap between the SE's '1's and the input image's '1's (indicated by asterisks). Therefore, the corresponding output pixels (aligned with the SE origin) are turned 'ON' in the resultant image grid on the right.*

**Step 6 (Final Result):** Repeat the process for all possible positions of the SE origin over the input image grid.

**(Paste Image: Dilation Final Result from Page 11 here)**

*This image shows the final output image after the dilation process is completed for all pixel positions. The original fork shape has been significantly expanded or thickened due to the repeated application of the dilation rule.*

#### Dilation Summary

-   **Action:** Expands/thickens foreground objects.
-   **Rule:** Output pixel is '1' if *any* part of the SE overlaps the input foreground when centered at that pixel.
-   **Uses:** Bridging gaps, filling small holes, making features larger/more connected.
-   **Effect:** Increases the size of foreground objects.

---

### Erosion

**Erosion** is the morphological dual of dilation. If dilation expands foreground objects, erosion **shrinks** or **thins** them. It can be used to remove small noise objects or thin connections between larger objects.

#### Process Description

1.  A **Structuring Element (SE)** with an origin is defined (same as in dilation).
2.  The SE is shifted across every pixel position of the input binary image.
3.  At each position, the algorithm checks if the SE **completely** fits *within* the foreground ('1' pixels) of the input image. That is, every '1' pixel in the SE must align with a '1' pixel in the input image.
4.  If the SE **fits completely**, the pixel in the *output* image corresponding to the SE's origin is set to '1' (foreground/black).
5.  If the SE does **not** fit completely (i.e., at least one '1' in the SE aligns with a '0' in the input image), the output pixel is set to '0' (background/white).

#### Mathematical Definition

The erosion of an image $A$ by a structuring element $B$, denoted $A \ominus B$, is defined as the set of all points $x$ such that $B$, shifted by $x$, is entirely contained within $A$.

$$ A \ominus B = \{x | (B)_x \subseteq A \} $$

Where:
-   $A$ is the input binary image.
-   $B$ is the structuring element.
-   $\ominus$ denotes the erosion operation.
-   $(B)_x$ represents the structuring element $B$ shifted (translated) so that its origin is at position $x$.
-   $\subseteq$ denotes "is a subset of", meaning $B$ shifted by $x$ must only cover pixels that are also in $A$.

*Simplified Summary:* Think of erosion as "shrinking" the foreground regions. A pixel remains foreground only if the entire structuring element fits inside the original shape when centered at that pixel.

**(Paste Image: Erosion Process Figure 10.15 from Page 13 here)**

*This figure (Fig. 10.15) illustrates the erosion process.
**Left (Input image):** The original shape in black. Asterisks likely indicate points being tested.
**Middle (Structuring element):** A cross-shaped SE with its origin marked.
**Right (Eroded image):** The result after erosion. Notice the shape is smaller than the input, and potentially disconnected if the SE couldn't fit across thin bridges. Pixels are kept only where the *entire* cross SE fits within the original black shape when centered there.*

#### Erosion Example Walkthrough

This example details the step-by-step process of erosion.

**Problem:** Given an input image (letter 'H') and a structuring element, find the eroded version.

**(Paste Image: Erosion Problem Setup from Page 14 here)**

*This image shows the input binary image ('H') and the 1x2 horizontal structuring element (SE) to be used. The origin is marked on the left pixel of the SE.*

**Step 1:** Compare the structuring element with the input image, checking for a complete match.

**(Paste Image: Erosion Step 1 from Page 15 here)**

*This image shows the process starting. The SE is shifted across the first row of the input image 'H'. Because the 1x2 SE never completely overlaps with only foreground ('H') pixels in this first row (it always partially covers background), the entire first row of the output image remains background ('OFF' or white).*

**Step 2:** Continue shifting the SE. Find locations where it fits perfectly.

**(Paste Image: Erosion Step 2 from Page 16 here)**

*This image shows the SE being mapped against the second row. After shifting one pixel to the right from the initial position, the 1x2 SE (marked with '*') perfectly aligns with two foreground pixels of the 'H'. Because it's a perfect match, the output pixel corresponding to the SE's origin is turned 'ON' (black).*

**Step 3 (Final Result):** Repeat the process until the SE has been compared at all possible positions.

**(Paste Image: Erosion Final Result from Page 17 here)**

*This image shows the final eroded image after the process is completed for all rows and columns. The original 'H' shape has been thinned, particularly the horizontal bar, because the 1x2 horizontal SE could fit along the vertical bars more easily than across the single-pixel-thick horizontal bar.*

#### Erosion Summary

-   **Action:** Shrinks/thins foreground objects.
-   **Rule:** Output pixel is '1' only if the *entire* SE fits within the input foreground when centered at that pixel.
-   **Uses:** Removing small noise objects, separating loosely connected elements, thinning shapes.
-   **Effect:** Decreases the size of foreground objects.

---

### Compound Operations

More complex and often more useful morphological operations can be created by performing combinations of the basic erosion and dilation operations. The two most widely used compound operations are **Opening** and **Closing**.

---

#### Opening

**Opening** is a compound morphological operation defined as an **erosion followed by a dilation**, using the same structuring element ($B$) for both steps.

#### Definition

The opening of an image $A$ by a structuring element $B$, denoted $A \circ B$, is:

$$ A \circ B = (A \ominus B) \oplus B $$

#### Process & Effect

1.  **Erode** the image $A$ with $B$. This step removes small objects, breaks thin connections, and tends to smooth contours by removing small peninsulas.
2.  **Dilate** the result of the erosion with the same $B$. This step partially restores the size of the objects that survived the erosion, but it generally does not reconnect broken parts or bring back removed small objects.

**Overall Effect:** Opening generally smooths the contour of an object, breaks narrow connections (isthmuses), and eliminates small islands and thin protrusions (noise). It does this without significantly changing the overall size of larger objects. Think of it as 'sweeping' the SE around the *inside* boundary of objects.

**(Paste Image: Opening Definition Diagram from Page 19 here)**

*This diagram visually explains opening.
**Left (Original shape A):** A shape with protrusions and a thin connecting bridge.
**Middle (After erosion $A \ominus B$):** The shape is shrunk. The thin bridge is broken, and the protrusions are reduced/removed. A disc-shaped SE is noted.
**Right (After dilation $(A \ominus B) \oplus B$):** The remaining parts are dilated back, smoothing the contour further, but the broken bridge remains broken. This final result is the opened image $A \circ B$.*

##### Opening Example: Noise Removal

**(Paste Image: Opening Example 1 from Page 20 here)**

*This example (from Gonzalez & Woods, 2002) shows the practical effect of opening.
**Left (Original Image):** Contains two main shapes connected by a bridge, with jagged protrusions on the left shape and a separate small square object.
**Right (Image After Opening):** The opening operation has smoothed the jagged edges of the left shape, completely removed the thin connecting bridge, and entirely eliminated the small isolated square (as it was likely smaller than the structuring element). The main bodies of the two larger shapes remain, relatively unchanged in size.*

##### Opening Example: Pixel Level

**(Paste Image: Opening Pixel Example from Page 21 here)**

*This pixel-level example further clarifies opening.
**Left (Original Image):** Shows two cross-like shapes connected by a single diagonal pixel bridge.
**Bottom (Structuring Element):** A 3x3 cross shape.
**Right (Processed Image):** The result after applying opening (erosion then dilation) with the SE. The erosion step removes the single-pixel bridge and likely some pixels from the tips of the crosses. The subsequent dilation expands the remaining parts slightly but cannot reconnect the bridge. The result is two separated, slightly smoothed cross shapes.*

---

#### Closing

**Closing** is the morphological dual of opening. It is defined as a **dilation followed by an erosion**, using the same structuring element ($B$) for both steps.

#### Definition

The closing of an image $A$ by a structuring element $B$, denoted $A \bullet B$, is:

$$ A \bullet B = (A \oplus B) \ominus B $$

#### Process & Effect

1.  **Dilate** the image $A$ with $B$. This step fills small holes, connects nearby objects, and tends to smooth contours by filling small inlets or gaps.
2.  **Erode** the result of the dilation with the same $B$. This step shrinks the expanded objects back towards their original size, but the connections and filled holes created by the dilation tend to remain.

**Overall Effect:** Closing generally smooths contours, fuses narrow breaks and long thin gulfs, eliminates small holes, and fills gaps in the contour. It does this without significantly changing the overall size of larger objects. Think of it as 'sweeping' the SE around the *outside* boundary of objects.

**(Paste Image: Closing Definition Diagram from Page 22 here)**

*This diagram (from Gonzalez & Woods, 2002) visually explains closing.
**Left (Original shape A):** A shape with an internal gap or gulf.
**Middle (After dilation $A \oplus B$):** The shape is expanded, and the dilation fills the internal gap. A disc-shaped SE is noted.
**Right (After erosion $(A \oplus B) \ominus B$):** The expanded shape is eroded back towards its original size, but the gap that was filled during dilation remains largely filled. This final result is the closed image $A \bullet B$.*

##### Closing Example: Gap Filling

**(Paste Image: Closing Example 1 from Page 23 here)**

*This example (from Gonzalez & Woods, 2002) shows the practical effect of closing.
**Left (Original Image):** Contains shapes with internal gaps: a missing corner piece on the left shape, and a small square hole within the right shape.
**Right (Image After Closing):** The closing operation has filled in the missing corner and the small internal hole, making the objects appear more solid.*

##### Closing Example: Pixel Level

**(Paste Image: Closing Pixel Example from Page 24 here)**

*This pixel-level example further clarifies closing.
**Left (Original Image):** Shows shapes with small internal background pixels (holes/gaps).
**Bottom (Structuring Element):** A 3x3 cross shape.
**Right (Processed Image):** The result after applying closing (dilation then erosion) with the SE. The dilation step expands the foreground, filling the gaps. The subsequent erosion shrinks the shape back somewhat, but the filled gaps persist. The result is a more solid foreground shape.*

#### Opening vs. Closing Mnemonics

-   **Opening:** "Opens up" small gaps between objects, removes small objects. Like rolling a ball *inside* the boundary.
-   **Closing:** "Closes up" small holes within objects, connects close objects. Like rolling a ball *outside* the boundary.

---

### Morphological Processing Example: Fingerprint Enhancement

**(Paste Image: Fingerprint Processing Example from Page 25 here)**

*This figure (from Gonzalez & Woods, 2002) demonstrates how sequences of morphological operations can be used for practical tasks like fingerprint enhancement.
**Top Left (A):** The original noisy fingerprint image.
**Top Middle (B):** A 3x3 square structuring element.
**Middle Left ($A \ominus B$):** Result of eroding the original image 'A' with SE 'B'. This thins the fingerprint ridges significantly.
**Middle Right ($(A \ominus B) \oplus B = A \circ B$):** Result of dilating the eroded image, effectively performing an **opening** operation ($A \circ B$). This smooths the contours and removes small noise specks (salt noise) while partially restoring ridge thickness.
**Bottom Left ($(A \circ B) \ominus B$):** Result of eroding the opened image. (Seems like an intermediate step shown for illustration).
**Bottom Right ($[(A \circ B) \oplus B] \ominus B = (A \circ B) \bullet B$?):** The diagram implies a **closing** operation applied *after* the opening operation. This sequence ($ (A \circ B) \bullet B $) can be effective for removing both small noise objects (via opening) and small gaps within ridges (via closing), leading to a cleaner fingerprint image.*

*This example highlights how combining basic morphological operations allows for sophisticated image processing tailored to specific application goals.*

---

### Morphological Algorithms

Using the simple techniques of erosion, dilation, opening, and closing as building blocks, we can construct more interesting and complex morphological algorithms to perform specific image analysis tasks. We will look at algorithms for:

-   **Boundary extraction:** Isolating the outline of objects.
-   **Region filling:** Filling holes within connected boundaries.
-   **Extraction of connected components:** Identifying and labeling separate objects.
-   **Thinning/thickening:** Reducing/expanding objects to a skeletal representation or a specific thickness.
-   **Skeletonization:** Finding the central "skeleton" of an object.
-   **Convex Hull:** Finding the smallest convex shape enclosing an object.
-   **Pruning:** Removing small spurs or branches from thinned objects.

---

### Hit or Miss Transform

The **Hit-or-Miss Transform (HMT)** is a basic morphological tool used primarily for **shape detection** or **template matching** in binary images. It finds the locations where a specific pattern (defined by both foreground and background pixels) exactly matches the image content.

#### Concept

The HMT uses *two* disjoint structuring elements, $B_1$ and $B_2$, often derived from a single target pattern $B$.
-   $B_1$ represents the **foreground** pixels of the pattern we want to find (the "hit" part).
-   $B_2$ represents the **background** pixels in the immediate neighborhood of the pattern (the "miss" part). This ensures we match the pattern only when it has the correct surrounding background.

The transformation finds all pixels (origins of the SEs) where $B_1$ finds a match in the image foreground *AND* $B_2$ finds a match in the image background simultaneously.

#### Process

The HMT is formally defined as the intersection ($\cap$) of two erosions:
1.  The erosion of the input image $X$ by the foreground structuring element $B_1$. This finds all locations where the foreground pattern $B_1$ fits within $X$. Let this result be $E_1 = X \ominus B_1$.
2.  The erosion of the **complement** (background) of the input image, $X^c$, by the background structuring element $B_2$. This finds all locations where the background pattern $B_2$ fits within the background of $X$. Let this result be $E_2 = X^c \ominus B_2$.
3.  The final Hit-or-Miss result is the **intersection** of these two erosions: $HMT = E_1 \cap E_2$. The output image will have foreground pixels only at the locations where the complete pattern (foreground $B_1$ surrounded by background $B_2$) was found.

#### Mathematical Definition (using slide notation)

The Hit-or-Miss transform of image $X$ using composite structuring element $B = (B_{hit}, B_{miss})$ (where $B_{hit}$ is the foreground pattern and $B_{miss}$ is the background pattern, often denoted $W-B$ where W is a window containing B) is defined as:

$$ HM(X, B) = (X \ominus B_{hit}) \cap (X^c \ominus B_{miss}) $$

*The slide uses $B$ for $B_{hit}$ and $W-B$ for $B_{miss}$:*
$$ HM(X, B) = (X \ominus B) \cap (X^c \ominus (W-B)) $$

Where:
-   $X$ is the input image.
-   $X^c$ is the complement (background) of $X$.
-   $B$ is the foreground structuring element.
-   $W-B$ is the background structuring element (local window $W$ minus foreground $B$).
-   $\ominus$ is erosion.
-   $\cap$ is intersection.

#### Hit-or-Miss Example Walkthrough

**Problem:** Find locations of a specific pattern (cross shape within checkerboard background) in an input image using HMT.

**(Paste Image: HMT Problem Setup from Page 29 here)**

*This image shows:
(a) The input image $X$ (a grid pattern).
(b) The foreground structuring element $B$ (a cross shape).
(c) The background structuring element $W-B$ (corner pixels corresponding to the background around the cross).
The task is to find where the cross pattern $B$ exists in the image $X$ AND is surrounded by the background pattern $W-B$.*

**Solution Steps:**

**Step 1:** Erode the input image $X$ with the foreground SE $B$.

**(Paste Image: HMT Steps 1 & 2 from Page 30 here - Focus on Step 1 explanation)**

*The top part of this image shows Step 1. The input grid $X$ is eroded by the cross $B$. The result (top right) shows pixels where the *entire* cross shape fits within the foreground grid lines of $X$. These are the potential 'hit' locations.*

**Step 2:** Erode the **complement** image $X^c$ with the background SE $W-B$.

**(Paste Image: HMT Steps 1 & 2 from Page 30 here - Focus on Step 2 explanation)**

*The bottom part of this image shows Step 2. The complement image $X^c$ (background of the original grid) is eroded by the corner pattern $W-B$. The result (bottom right) shows pixels where the *entire* corner background pattern fits within the original image's background ($X^c$). These are the potential 'miss' locations (meaning the required background is present).*

**Step 3:** Find the intersection of the results from Step 1 and Step 2.

**(Paste Image: HMT Step 3 from Page 31 here)**

*This image shows the final result. It is the pixel-wise intersection (logical AND) of the output from Step 1 and the output from Step 2. The only pixels remaining 'ON' (black) are those that were 'ON' in *both* intermediate results. These locations correspond exactly to the origins (centers) where the specific foreground cross pattern $B$ was found with its required surrounding background pattern $W-B$.*

---
---

## Image Compression

**Image compression** is the process of reducing the amount of data required to represent a digital image. This is achieved by removing redundant data while aiming to retain the necessary visual information.

### 5.2 Introduction, Redundancies, Lossless Methods

-   **Introduction:** Basic concepts and goals of compression.
-   **Redundancies:** Types of data repetition or predictability exploited by compression.
    -   Coding redundancy
    -   Inter-pixel redundancy
    -   Psycho-visual redundancy
-   **Compression Ratio:** Measure of compression effectiveness.
-   **Fidelity Criteria:** How to measure the quality of compressed images (especially for lossy methods).
-   **Lossless Compression Techniques:** Methods that allow perfect reconstruction of the original image.
    -   Run-length coding (RLE)
    -   Arithmetic coding
    -   Huffman coding
    -   Differential PCM (DPCM) - often a component in other schemes.

### 5.3 Lossy Compression Techniques

-   **Lossy Compression Techniques:** Methods that achieve higher compression ratios by discarding some information, resulting in an approximation of the original image.
    -   Improved grey scale quantization (IGS)
    -   Vector quantization (VQ)
    -   Transform coding (e.g., DCT used in JPEG)
    -   JPEG standard

---

### Fundamentals of Image Compression

#### Definition and Goal

-   **Image compression** involves reducing the size (number of bits) of image data files.
-   The primary goal is to minimize storage space and transmission bandwidth/time.
-   This is achieved by identifying and removing **redundant data**.
-   The process involves:
    1.  **Compression/Encoding:** Transforming the original image data into a smaller representation.
    2.  **Storage/Transmission:** Handling the compressed data.
    3.  **Decompression/Decoding:** Reconstructing the image from the compressed data. The result is either the exact original (**lossless** compression) or an approximation (**lossy** compression).

#### Mathematical Viewpoint

-   Mathematically, compression often involves transforming the original 2D pixel array (which usually has high correlation between adjacent pixels) into a more compact, statistically uncorrelated data set (e.g., transform coefficients, difference values, run-length pairs).

#### Compression Ratio

-   The **Compression Ratio ($C_R$)** quantifies how much smaller the compressed data is compared to the original.
    $$ C_R = \frac{\text{Uncompressed Image Size}}{\text{Compressed Image Size}} = \frac{U_{size}}{C_{size}} $$
-   Where:
    -   `$U_{size}$` = Size of the original uncompressed image (e.g., in bytes or bits). Calculated as $M \times N \times k$, where $M \times N$ are pixel dimensions, and $k$ is bits per pixel.
    -   `$C_{size}$` = Size of the compressed image file.

##### Compression Ratio Example

-   **Problem:** Consider an 8-bit grayscale image of size 256x256 pixels. After compression, the file size is 6,554 bytes. Find the compression ratio.
-   **Solution:**
    -   Uncompressed Size ($U_{size}$):
        $U_{size} = 256 \text{ pixels} \times 256 \text{ pixels} \times 8 \text{ bits/pixel}$
        $U_{size} = 524,288 \text{ bits}$
        $U_{size} = 524,288 \text{ bits} / (8 \text{ bits/byte}) = 65,536 \text{ bytes}$
    -   Compressed Size ($C_{size}$) = 6,554 bytes (given).
    -   Compression Ratio ($C_R$):
        $C_R = \frac{65,536}{6,554} \approx 9.999 \approx 10$
-   **Interpretation:** The compression ratio is approximately 10:1. This means the compressed image occupies only about 1/10th of the space of the original image (or, for every 10 bytes in the original, there is 1 byte in the compressed version).

#### Redundancy and Compression Ratio

-   Let $n_1$ represent the number of information-carrying units (e.g., bits) in the original data set and $n_2$ represent the units in the compressed data set.
-   The **Compression Ratio** is $C_R = n_1 / n_2$.
-   The **Relative Data Redundancy ($R_D$)** of the original data set ($n_1$) is defined as:
    $$ R_D = 1 - \frac{1}{C_R} $$
-   **Interpretation:**
    -   If $n_1 = n_2 \implies C_R = 1 \implies R_D = 0$: No redundancy removed, no compression achieved.
    -   If $n_2 << n_1 \implies C_R \to \infty \implies R_D \to 1$: High redundancy present, significant compression achieved. $R_D=1$ represents maximum possible redundancy removal relative to the $n_2$ representation.
    -   If $n_2 >> n_1 \implies C_R \to 0 \implies R_D \to -\infty$: Data size increased (expansion), not compression.

#### Image Data Redundancies

Compression algorithms work by reducing or eliminating different types of redundancies present in typical image data.

##### 1. Coding Redundancy

-   **Definition:** Occurs when the codes used to represent image pixel values (e.g., gray levels or colors) are longer than necessary, given the statistical probabilities of those values.
-   **Example:** An 8-bit image format allows 256 gray levels, using 8 bits per pixel (fixed-length code). If the actual image only contains 16 distinct gray levels, these could theoretically be represented using only 4 bits per pixel. Using 8 bits is therefore redundant.
-   **Exploitation:** Variable-length coding techniques (like Huffman coding or Arithmetic coding) assign shorter codes to more frequent pixel values and longer codes to less frequent ones, reducing the average number of bits per pixel.

**(Paste Image: Coding Redundancy Table from Page 39 here)**

*This table illustrates coding redundancy. It shows 8 possible gray levels ($r_0$ to $r_7$) and their probabilities ($p_r(r_k)$).
**Code 1:** A natural 3-bit fixed-length binary code ($l_1(r_k)=3$ for all k). The average length $L_{avg}$ is 3 bits/pixel.
**Code 2:** A variable-length code. More probable levels ($r_0, r_1, r_2$) get shorter 2-bit codes, while less probable levels ($r_7$) get longer 6-bit codes ($l_2(r_k)$ varies). This aims to reduce the *average* code length.*

*Calculation (from Page 40):*
-   Average length for Code 2:
    $L_{avg} = \sum l_2(r_k)p_r(r_k) = 2(0.19)+2(0.25)+2(0.21)+3(0.16)+4(0.08)+5(0.06)+6(0.03)+6(0.02) = 2.7 \text{ bits/pixel}$
-   Compression Ratio relative to Code 1: $C_R = 3 / 2.7 \approx 1.11$
-   Relative Data Redundancy removed by using Code 2 instead of Code 1: $R_D = 1 - 1/1.11 \approx 0.099$ (approx 9.9% redundancy reduced).

*This demonstrates how variable-length coding, by exploiting the probability distribution of pixel values, removes coding redundancy.*

##### 2. Interpixel Redundancy (Spatial Redundancy)

-   **Definition:** Occurs because adjacent pixels in an image tend to have similar values (i.e., they are highly correlated). The value of a pixel is often predictable from its neighbors.
-   **Example:** Large areas of sky or a uniform wall in a photograph. The gray levels change gradually or not at all across these regions.
-   **Exploitation:**
    -   **Mapping:** Instead of coding each pixel independently, represent the image in terms of differences between adjacent pixels (Differential Coding, DPCM), or by encoding runs of identical pixels (Run-Length Encoding, RLE).
    -   **Transformation:** Transform blocks of pixels into a domain (like frequency domain via DCT) where the correlation is more effectively captured and redundancy can be removed via quantization.

**(Paste Image: Interpixel Redundancy Pencils from Page 43 here)**

*This image cleverly illustrates interpixel redundancy. Both panels show 5 pencils.
**Left Panel:** Randomly arranged pencils. High spatial variation.
**Right Panel:** Parallel pencils. Strong spatial correlation – knowing one pixel's value gives a strong clue about its horizontal neighbors.
**Key Point:** Both images have the *same histogram* (same number of black/white pixels) and the same gray level probabilities. Therefore, methods relying only on *coding redundancy* (like Huffman) would achieve the same compression for both. However, the right image contains significant *interpixel redundancy* that could be exploited by methods like RLE or transform coding, leading to much higher compression for the right image than the left.*

*The example text mentions encoding 1024 bits of binary data as pairs like (1,63), (0,87)... requiring only 88 bits, likely using a run-length approach for the patterned image.*

##### 3. Psychovisual Redundancy

-   **Definition:** Relates to the characteristics of the Human Visual System (HVS). The eye and brain do not perceive all visual information with the same sensitivity. Some information is less important or even imperceptible.
-   **Example:** Humans are generally less sensitive to fine details (high spatial frequencies) compared to coarse features (low frequencies), and less sensitive to subtle changes in color (chrominance) compared to changes in brightness (luminance).
-   **Exploitation:** This information is considered **psychovisually redundant** and can be **eliminated** or heavily compressed without significantly affecting the *perceived* image quality. This is the basis of **lossy compression**.
    -   **Quantization:** A key technique where information is discarded, often by reducing the precision of pixel values or transform coefficients. For example, reducing 256 gray levels to 16 by grouping. While this achieves compression (e.g., 2:1), aggressive quantization can lead to visible artifacts like **graininess** or **contouring** (posterization).

*Image compression is achieved when one or more of these redundancies (Coding, Interpixel, Psychovisual) are reduced or eliminated.*

---

### Fidelity Criteria

When **lossy compression** is used, the reconstructed image $\hat{f}(x,y)$ is only an approximation of the original image $f(x,y)$. **Fidelity criteria** are used to measure the nature and extent of the information loss, or how "faithful" the reconstruction is to the original.

There are two general classes:

A)  **Objective Fidelity Criteria:** Quantitative measures based on mathematical differences between the original and reconstructed images.
B)  **Subjective Fidelity Criteria:** Qualitative assessments based on human perception.

#### Objective Fidelity Criteria

-   These criteria express the level of information loss as a mathematical function of the original ($f$) and decompressed ($\hat{f}$) images.
-   Common measures include:
    -   **Pixel Error:** $e(x, y) = \hat{f}(x, y) - f(x, y)$
    -   **Root Mean Square (RMS) Error:** Measures the average magnitude of the error per pixel.
        $$ e_{rms} = \sqrt{\frac{1}{MN} \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} [\hat{f}(x,y) - f(x,y)]^2} $$
        (Where M, N are image dimensions)
    -   **Mean Square Signal-to-Noise Ratio (SNR<sub>ms</sub>):** Ratio of signal power (often approximated by the power of the reconstructed image) to error power.
        $$ SNR_{ms} = \frac{\sum_{x=0}^{M-1} \sum_{y=0}^{N-1} [\hat{f}(x,y)]^2}{\sum_{x=0}^{M-1} \sum_{y=0}^{N-1} [\hat{f}(x,y) - f(x,y)]^2} $$
        (Note: Sometimes the numerator uses the original image $f(x,y)$ instead of $\hat{f}(x,y)$).
    -   **Peak Signal-to-Noise Ratio (PSNR):** A variation of SNR often used for images, typically expressed in decibels (dB). Higher PSNR generally indicates better objective quality.

-   **Pros:** Simple to calculate, repeatable, quantitative.
-   **Cons:** May not correlate well with human perception of image quality. An image with lower RMS error might look worse to a human than one with slightly higher RMS error.

#### Subjective Fidelity Criteria

-   These criteria rely on the evaluation of image quality by human observers. Since most images are ultimately viewed by people, this is often considered the most appropriate measure.
-   **Methods:**
    -   Showing a "typical" decompressed image to a panel of viewers.
    -   Using an **absolute rating scale** (e.g., Mean Opinion Score - MOS, often 1=Bad to 5=Excellent).
    -   Performing **side-by-side comparisons** of the original $f(x,y)$ and the decompressed $\hat{f}(x,y)$.
-   **Pros:** Reflects perceived visual quality.
-   **Cons:** Complex and time-consuming to perform, results can vary between viewers and viewing conditions, less easily quantifiable or reproducible than objective measures.

---

### Lossless Technique: Huffman Coding

**Huffman Coding** is a widely used **lossless** entropy coding algorithm that addresses **coding redundancy**. It assigns variable-length binary codes to input symbols (e.g., pixel values, run-length pairs) based on their probabilities of occurrence. More frequent symbols get shorter codes, and less frequent symbols get longer codes, minimizing the average code length.

#### Example Walkthrough

**Setup:** Consider symbols {a1, a2, a3, a4, a5, a6} representing intensity levels in a 10x10 image. Their frequencies and calculated probabilities are given.

**(Paste Image: Huffman Coding Example Setup from Page 41 here)**

*This table shows the initial setup for Huffman coding. The symbols (a2, a6, a1, a4, a3, a5) are listed along with their probabilities, sorted in descending order (0.4, 0.3, 0.1, 0.1, 0.06, 0.04). The columns labeled 1, 2, 3, 4 represent the stages of the source reduction process.*

**Process (Source Reduction):**

1.  **Combine Lowest Probabilities:** Take the two symbols with the lowest probabilities (a5: 0.04, a3: 0.06). Combine them into a new node with probability 0.04 + 0.06 = 0.10.
2.  **Re-sort:** Insert this new node back into the list, maintaining sorted order. The list might now be {a2:0.4, a6:0.3, a1:0.1, a4:0.1, new:0.1}.
3.  **Repeat:** Continue combining the two lowest probability nodes/symbols at each step and re-sorting until only two nodes remain.

**(Paste Image: Huffman Coding Example Steps & Results from Page 42 here)**

*This image shows the completed table and the results.
**Table:** Tracks the source reduction steps. Arrows show how probabilities are combined. For instance, in step 1, 0.06 and 0.04 combine to 0.1 (labeled '0.1>'). In step 2, 0.1 and 0.1 combine to 0.2. In step 3, 0.1 and 0.2 combine to 0.3. Finally, 0.4 and 0.3 combine with the result of step 3 (0.3) until two final probabilities (0.6 and 0.4) are left.
**Code Assignment:** Assign '0' and '1' to the final two branches. Trace back through the merge steps, appending '0' or '1' at each split to form the code for each original symbol. The resulting Huffman codes are shown next to the probabilities (e.g., a2: 1, a6: 00, a1: 011, a4: 0100, a3: 01010, a5: 01011).
**Parameters:**
1.  **Average Length ($L_{avg}$):** $\sum (\text{probability} \times \text{code length})$
    $L_{avg} = (0.4 \times 1) + (0.3 \times 2) + (0.1 \times 3) + (0.1 \times 4) + (0.06 \times 5) + (0.04 \times 5) = 2.2 \text{ bits/symbol}$
2.  **Total Bits:** For the 10x10 image = $10 \times 10 \times 2.2 = 220$ bits.
3.  **Entropy:** The theoretical minimum average code length is mentioned as 2.1396 bits/symbol. Huffman coding is very close to this optimal value.
4.  **Savings:** Assuming original was 5 bits/symbol (e.g., if there were up to 32 levels), original size = $10 \times 10 \times 5 = 500$ bits. Savings = $(500 - 220) / 500 = 0.56 = 56\%$.*

---

### Lossless Technique: Run-Length Encoding (RLE)

**Run-Length Encoding (RLE)** is a simple **lossless** compression technique particularly effective at handling **interpixel redundancy** when there are long sequences (runs) of identical pixel values.

#### Concept

RLE replaces consecutive sequences of the same data value (a "run") with a pair of values: the data value itself and the count (length) of the run.

**(Paste Image: RLE Diagram from Page 44 here)**

*This diagram illustrates the basic principle. The input sequence `a a a b c c c c` contains a run of three 'a's, one 'b', and four 'c's. The RLE output represents this as `a 3 b 1 c 4`.*

#### Suitability

-   **Works Best:** Images with large areas of constant color or intensity, such as graphics, icons, cartoons, scanned documents, and simple animations. Especially useful for binary images.
-   **Works Poorly:** Complex images like photographs with continuous tone variations usually have very few runs, and RLE can actually *increase* the file size due to the overhead of storing counts for short runs.

#### Process

-   Scan the image data (e.g., pixel by pixel, row by row).
-   Identify consecutive runs of identical values.
-   Store each run as (value, count).
-   Decompression simply reconstructs the runs from the (value, count) pairs.

*Real-world uses:* Found in formats like PCX, BMP, TGA, TIFF, and used in fax machines.

---

### Lossless Technique: Arithmetic Coding

**Arithmetic Coding** is another **lossless** entropy coding technique that often achieves slightly higher compression ratios than Huffman coding. It addresses **coding redundancy**.

#### Main Idea

Instead of assigning a specific binary code to each symbol, Arithmetic Coding represents an entire sequence of input symbols as a **single fraction** $F$ within the range $[0, 1)$.

**(Paste Image: Arithmetic Coding Main Idea from Page 51 here)**

*This diagram shows the core concept: A sequence of symbols $S_1 S_2 S_3 S_4 ...$ is mapped to a unique floating-point number within the interval $[0, 1)$. The example shows a mapping to approximately 0.6457351...*

-   The mapping depends on the **probabilities** of the input symbols.
-   The process involves progressively **narrowing down** a sub-interval within $[0, 1)$ based on the sequence of input symbols. The final fraction chosen falls within the final, very small sub-interval.
-   It doesn't require generating codes for all possible sequences *a priori*.

#### Example Walkthrough

**Setup:** Alphabet $A = \{a, b, c\}$, Probabilities $p = (0.2, 0.5, 0.3)$, Message $M = babc$.

**(Paste Image: Arithmetic Coding Diagram & Initial Step from Page 52 here)**
**(Paste Image: Arithmetic Coding Diagram & Step 2 Calc from Page 53 here)**
**(Paste Image: Arithmetic Coding Diagram & Step 3 Calc from Page 54 here)**
**(Paste Image: Arithmetic Coding Diagram & Table Summary from Page 55 here)**

*These images collectively illustrate the process:
**Diagram:** Shows the interval $[0, 1)$ being subdivided.
**Process:**
1.  **Start:** Interval is $[0.0, 1.0)$.
2.  **Symbol 'b':** Probability p(b)=0.5. It occupies the sub-interval corresponding to cumulative probability [p(a), p(a)+p(b)) = [0.2, 0.7). New interval is $[0.2, 0.7)$. (Range = 0.5).
3.  **Symbol 'a':** Probability p(a)=0.2. Within the current interval $[0.2, 0.7)$, 'a' occupies the first 0.2 fraction of the range. New interval:
    -   Low = Old Low + Range * CumulativeProb(before 'a') = $0.2 + 0.5 \times 0.0 = 0.2$
    -   High = Old Low + Range * CumulativeProb(up to 'a') = $0.2 + 0.5 \times 0.2 = 0.3$
    New interval is $[0.2, 0.3)$. (Range = 0.1).
4.  **Symbol 'b':** Probability p(b)=0.5. Within $[0.2, 0.3)$, 'b' occupies the sub-interval corresponding to cumulative probability [p(a), p(a)+p(b)) = [0.2, 0.7) within this scaled range.
    -   Low = Old Low + Range * CumulativeProb(before 'b') = $0.2 + 0.1 \times 0.2 = 0.22$
    -   High = Old Low + Range * CumulativeProb(up to 'b') = $0.2 + 0.1 \times (0.2 + 0.5) = 0.2 + 0.1 \times 0.7 = 0.27$
    New interval is $[0.22, 0.27)$. (Range = 0.05).
5.  **Symbol 'c':** Probability p(c)=0.3. Within $[0.22, 0.27)$, 'c' occupies the sub-interval corresponding to cumulative probability [p(a)+p(b), p(a)+p(b)+p(c)) = [0.7, 1.0).
    -   Low = Old Low + Range * CumulativeProb(before 'c') = $0.22 + 0.05 \times 0.7 = 0.22 + 0.035 = 0.255$
    -   High = Old Low + Range * CumulativeProb(up to 'c') = $0.22 + 0.05 \times 1.0 = 0.22 + 0.05 = 0.27$
    Final interval for 'babc' is $[0.255, 0.270)$.
**Result:** Any fraction within this final interval (e.g., 0.26) uniquely represents the sequence "babc". The decoder uses the same probability model to reverse the process and retrieve the sequence.*

**Advantages over Huffman:** Often achieves compression closer to the theoretical entropy limit, especially for skewed probabilities or small alphabets.
**Disadvantages:** Can be more computationally intensive, more sensitive to transmission errors.

---

### Lossy Technique: Improved Grey Scale (IGS) Quantization

**Improved Grey Scale (IGS) Quantization** is a **lossy** technique designed to reduce the visible artifacts (like contouring and graininess) caused by simple **quantization**, thereby exploiting **psychovisual redundancy** more effectively.

#### Concept

-   Standard quantization reduces the number of gray levels, which can create abrupt jumps in intensity (contours) that are easily visible.
-   IGS aims to break up these contours by adding a small amount of **pseudo-random noise** to each pixel *before* it is quantized.
-   This noise is typically generated based on the **low-order bits** of neighboring pixels, creating a form of **dithering**.
-   The added noise causes pixels near a quantization threshold to sometimes fall above and sometimes below it, effectively smoothing the transition and making the quantization less apparent.

**(Paste Image: IGS Quantization Table from Page 47 here)**

*This table demonstrates the IGS idea.
**Pixel Column:** Shows neighboring pixels i-1, i, i+1, etc.
**Gray Level:** Original pixel values (e.g., pixel i+1 is 10001011).
**Sum:** Represents the value *after* adding the pseudo-random number derived from neighbors (details not shown, but for pixel i+1, the value becomes 10010111). The rule "If most significant bits are all 1, the 0s are added" seems like a specific edge case handling.
**IGS Code:** The result after quantizing the 'Sum'. Typically, this involves taking the most significant bits (MSBs) of the 'Sum'. For i+1, the IGS code is 1001 (the top 4 MSBs).
The overall effect is that the quantization boundaries become 'fuzzier', reducing visible contouring.*

---

### Lossy Technique: Vector Quantization (VQ)

**Vector Quantization (VQ)** is a **lossy** compression technique that quantizes **groups of pixels (vectors)** rather than individual pixels (scalars). It leverages **interpixel redundancy** within blocks and can theoretically achieve better compression than scalar quantization for the same level of distortion.

#### Concept

1.  **Vector Formation:** Divide the image into small, non-overlapping blocks (e.g., 4x4 pixels). Each block is treated as a single **vector** (e.g., a 16-dimensional vector by concatenating rows).
2.  **Codebook:** Maintain a **codebook**, which is a pre-defined set of representative vectors (codewords). This codebook is generated beforehand using a training process on typical image data.
3.  **Encoding:** For each input vector (image block), find the **closest matching vector** (codeword) in the codebook according to some distance measure (e.g., Euclidean distance). Store or transmit only the **index** (address) of that best-matching codeword in the codebook.
4.  **Decoding:** Use the received index to look up the corresponding codeword vector in the (identical) codebook and place that vector back into the image grid.

**(Paste Image: VQ 4x4 Subimage Example from Page 58 here)**

*This image shows step 1: A 4x4 subimage block of pixel values is rearranged into a 1D vector of 16 elements: `[65 70 71 75 71 70 71 81 81 80 81 82 90 90 91 92]`. This is the vector that VQ operates on.*

#### VQ vs Scalar Quantization

-   **Scalar:** Quantizes each pixel value independently (e.g., rounding 65, 70, 71... individually). Doesn't exploit correlation between pixels.
-   **Vector:** Quantizes the entire block/vector as one unit. Can exploit the relationships *between* the pixel values within the block, leading to potentially better compression according to Information Theory.

#### Codebook and Indexing

**(Paste Image: Figure 10.3-7 VQ with Codebook from Page 62 here)**

*Figure 10.3-7 illustrates the VQ process with a codebook.
(a) An original 256x256 image is divided into 4x4 blocks.
(b) A codebook contains 256 entries (indexed 0-255). Each entry is a 16-byte vector representing a typical 4x4 pattern.
(c) Encoding: A specific input block is compared to all 256 codebook entries. If entry #122 is the best match, the compressed data for that block is simply the index '122'.
(d) Decoding: Receiving index '122', the decoder retrieves the 16-byte vector stored at address 122 in the codebook and uses it to reconstruct the 4x4 block (shown as 'abcd efgh...').*

#### Compression Ratio & Codebook Storage

-   **Example Calculation (Ideal):** If the original uses 8 bits (1 byte) per pixel, a 4x4 block is 16 bytes. If the codebook has 256 entries, the index requires $\log_2(256) = 8$ bits = 1 byte. The compression ratio *for the block data* is 16 bytes / 1 byte = 16:1.
-   **Codebook Overhead:** However, the decoder needs the codebook. If the codebook must be stored/transmitted with the compressed data, this significantly impacts the overall compression ratio.
    -   **(Recalculation from Page 64):** For a 256x256 image (4096 blocks) and a 256-entry codebook (where each entry is 16 bytes):
        -   Index data size = 4096 blocks * 1 byte/index = 4096 bytes.
        -   Codebook size = 256 entries * 16 bytes/entry = 4096 bytes.
        -   Total compressed size = 4096 + 4096 = 8192 bytes.
        -   Original size = 256 * 256 * 1 byte = 65,536 bytes.
        -   Effective $C_R = 65536 / 8192 = 8:1$. Including the codebook cut the CR in half.
-   **Options:** Use generic codebooks (less optimal compression) or image-specific codebooks (better compression but requires overhead).

#### Codebook Generation (Training)

-   The codebook is crucial and is generated using a **training algorithm** (e.g., LBG algorithm, similar to k-means clustering) on a set of representative image blocks.
-   The algorithm aims to find a set of codebook vectors that minimizes the average **distortion** (error) between the original training blocks and their corresponding closest codebook vectors.

---

### Lossy Technique: JPEG Compression

**JPEG (Joint Photographic Experts Group)** is the most widely used standard for **lossy compression** of continuous-tone images (like photographs). It typically achieves high compression ratios (e.g., 10:1 to 20:1 or more) with good perceived image quality.

#### Why JPEG? Motivation

-   Lossless methods (Huffman, RLE, LZW) usually provide insufficient compression (often only 2:1 or 3:1) for large images and video.
-   JPEG leverages **transform coding**, specifically the **Discrete Cosine Transform (DCT)**, based on key observations about images and human vision:
    1.  **Energy Compaction:** Images typically have strong spatial correlation (interpixel redundancy). The DCT concentrates most of this signal energy into a few low-frequency coefficients.
    2.  **Psychovisual Redundancy:** The HVS is less sensitive to errors in high-frequency components than low-frequency ones.

#### JPEG Baseline Sequential Steps

This is the most common mode of JPEG operation.

**(Paste Image: JPEG Coding Block Diagram from Page 67 here)**

*This block diagram outlines the core stages of JPEG encoding:*

1.  **(Implicit: Color Space Conversion & Subsampling):** Input image (often RGB) is typically converted to YCbCr (Luminance, Chrominance Blue, Chrominance Red). The Cb and Cr components are often subsampled (e.g., 4:2:0) because the eye is less sensitive to color detail than brightness, providing initial compression.
2.  **Block Splitting:** Divide each component (Y, Cb, Cr) into 8x8 pixel blocks. The following steps are applied to each block independently.
3.  **Discrete Cosine Transform (DCT):** Apply a 2D DCT to each 8x8 block ($f(i,j)$). This transforms the 64 spatial pixel values into 64 frequency coefficients ($F(u,v)$), where $F(0,0)$ is the **DC coefficient** (average block value) and the other 63 are **AC coefficients** representing increasing frequencies.
    **(Formula Reference - see Page 68/69 for DCT details and example)**
    **(2D DCT Process - see Page 70 for row-column transform)**
4.  **Quantization:** This is the **main lossy step**. Divide each of the 64 DCT coefficients $F(u,v)$ by a corresponding value from an 8x8 **Quantization Table** $Q(u,v)$ and round the result to the nearest integer: $F_q(u,v) = \text{round}(F(u,v) / Q(u,v))$.
    -   The quantization table has larger values for higher frequencies (bottom-right) and smaller values for lower frequencies (top-left, especially DC).
    -   This selectively discards precision, especially for high-frequency AC coefficients that are less perceptually important. Many AC coefficients become zero after this step.
    **(See Page 72 for Quantization details and rationale)**
5.  **Zig-Zag Scan:** Reorder the 64 quantized coefficients ($F_q$) from the 8x8 matrix into a 1D vector using a zig-zag pattern. This groups the DC coefficient first, followed by low-frequency ACs, and pushes the many zero high-frequency ACs towards the end of the vector.
    **(See Page 73 for Zig-Zag diagram)**
6.  **Differential DC Encoding (DPCM):** Encode the DC coefficient ($F_q(0,0)$) of the current block as the *difference* from the DC coefficient of the previous block in the scan order. This exploits the correlation between DC values of adjacent blocks.
    **(See Page 74 for DPCM concept)**
7.  **Run-Length Encoding (RLE) of AC:** Encode the 63 AC coefficients in the 1D zig-zag vector. Use `(skip, value)` pairs, where `skip` is the number of consecutive zeros before the next non-zero `value`. Use a special End-Of-Block (EOB) code `(0,0)` if the remaining AC coefficients are all zero.
    **(See Page 75 for RLE on AC concept and example)**
8.  **Entropy Coding (Huffman/Arithmetic):** Apply a lossless entropy coding scheme (typically Huffman coding in baseline JPEG) to further compress:
    -   The DPCM-encoded DC differences (represented as `(SIZE, VALUE)` pairs).
    -   The RLE-encoded AC coefficients (represented as `(RunLength/SIZE, VALUE)` pairs).
    **(See Pages 76-79 for detailed DC/AC Entropy Coding examples)**
9.  **(Implicit: Formatting):** Combine the encoded data with headers containing quantization tables, Huffman tables, image dimensions, etc., to form the final JPEG file.

#### JPEG Modes

Besides the common Baseline Sequential mode, the JPEG standard defines other modes:

##### 1. Sequential Mode

-   Encodes the image in a single scan (left-to-right, top-to-bottom).
-   **Baseline Sequential:** The mode described above, using DCT, quantization, and Huffman coding. Typically supports 8-bit per component images.
-   **Extended Sequential:** Adds features like 12-bit support, arithmetic coding option.

##### 2. Lossless Mode

-   Provides **truly lossless** compression (guaranteed perfect reconstruction).
-   Uses **predictive coding**, *not* DCT and quantization.
-   **Mechanism:** Predicts each pixel's value based on its already coded neighbors (using one of 7 predictors). Encodes the (usually small) *difference* between the actual and predicted values using Huffman or arithmetic coding.
-   Achieves much lower compression ratios (typically 2:1 - 3:1) than lossy modes.

**(Paste Image: Lossless JPEG Diagram from Page 81 here)**
**(Paste Image: Lossless JPEG Predictors from Page 82 here)**

*These images show the predictive difference concept and the neighbor-based prediction formulas used in Lossless JPEG.*

##### 3. Progressive Mode

-   Allows an image to be transmitted in multiple scans, enabling a coarse preview that improves in quality with subsequent scans. Useful for viewing images over slow network connections.
-   Two main methods:
    -   **Spectral Selection:** Sends low-frequency DCT coefficients first (e.g., DC and first few ACs in scan 1), then gradually adds more higher-frequency ACs in later scans.
        **(Paste Image: Progressive JPEG - Spectral Selection from Page 83 here)**
    -   **Successive Approximation:** Sends all DCT coefficients in each scan, but with increasing precision. Scan 1 sends the most significant bits (MSBs) of all coefficients, scan 2 sends the next bit(s), and so on.
        **(Paste Image: Progressive JPEG - Successive Approximation from Page 84 here)**

##### 4. Hierarchical Mode

-   Encodes the image at multiple spatial resolutions (like an image pyramid).
-   Allows a decoder to retrieve only the resolution needed (e.g., a low-resolution thumbnail or the full-resolution image).
-   **Mechanism:** Encodes a downsampled version of the image, then encodes the difference required to reconstruct the next higher resolution based on an upsampled version of the lower one, repeating for multiple levels.

**(Paste Image: Hierarchical JPEG Encoder/Decoder Diagram from Page 85 here)**

*This diagram shows a 3-level hierarchical scheme. The encoder creates progressively lower-resolution versions (I, I2, I4) and encodes them (L1, L2, L4), often encoding differences between levels. The decoder reconstructs level by level.*

---

## Summary of Image Compression Methods

**(Paste Image: Image Compression Methods Chart from Page 86 here)**

*This chart provides a high-level overview:
**Data Compression Methods** branch into:
-   **Lossless Methods:** Used for text, programs, data where perfect reconstruction is essential. Examples: Run-length, Huffman, Lempel-Ziv (family including LZW).
-   **Lossy Methods:** Used for images, video, audio where some data loss is acceptable for higher compression. Examples: JPEG, MPEG (video), MP3 (audio).*

---

### Lossless Techniques List

Common lossless image compression techniques include:

1.  **Run-length encoding (RLE):** Used in PCX, BMP, TGA, TIFF.
2.  **Variable-length coding:** Huffman coding, Arithmetic coding (often used within other schemes like JPEG, PNG).
3.  **Bit Plane coding:** Decomposing image into bit planes and compressing each plane.
4.  **DPCM and Predictive Coding:** Encoding differences between pixels or predictions (basis of lossless JPEG, PNG filters).
5.  **Entropy encoding:** General term for methods like Huffman/Arithmetic that exploit symbol probabilities.
6.  **LZW (Lempel-Ziv-Welch) coding:** Adaptive dictionary-based method used in GIF, TIFF.
7.  **Adaptive dictionary algorithms:** General class including LZW variants.
8.  **Deflation:** Combination of LZ77 (another dictionary method) and Huffman coding, used in PNG, MNG, TIFF.
9.  **Chain codes:** Representing boundaries/contours efficiently.

### Lossy Techniques List

Common lossy compression techniques include:

1.  **Reducing the color space:** E.g., converting 24-bit color to 8-bit indexed color (color quantization/palettization).
2.  **Chroma subsampling:** Reducing resolution of color components (Cb, Cr) relative to luminance (Y), used in JPEG, MPEG.
3.  **Fractal compression:** Representing image parts using iterated function systems (less common now).
4.  **Transform coding:** Transforming blocks to another domain (frequency/wavelet) and quantizing coefficients.
    -   **DCT (Discrete Cosine Transform):** Used in JPEG, MPEG video.
    -   **Wavelet Transform:** Used in JPEG 2000, some video codecs.

---
---

## Glossary

-   **AC Coefficients:** (Alternating Current) In DCT-based compression (like JPEG), the DCT coefficients other than the DC coefficient, representing higher spatial frequencies.
-   **Arithmetic Coding:** A lossless entropy coding technique that represents an entire sequence of symbols as a single fraction in the range [0, 1), often achieving slightly better compression than Huffman coding.
-   **Binary Image:** An image where each pixel has only one of two possible values, typically black (1) or white (0).
-   **Closing:** A compound morphological operation (dilation followed by erosion) used to fill small holes, connect gaps, and smooth contours from the outside. ($A \bullet B = (A \oplus B) \ominus B$).
-   **Codebook:** In Vector Quantization (VQ), a pre-defined set of representative vectors (codewords) used as a lookup table during compression and decompression.
-   **Coding Redundancy:** Inefficiency in data representation where the codes used are longer than necessary given the probabilities of the symbols being coded. Addressed by entropy coding like Huffman or Arithmetic coding.
-   **Compound Operations:** Morphological operations created by combining basic operations (erosion, dilation). Opening and Closing are the most common.
-   **Compression Ratio (CR):** A measure of compression effectiveness, calculated as (Uncompressed Size) / (Compressed Size). A CR of 10:1 means the compressed file is 1/10th the size of the original.
-   **Contouring:** An artifact in quantized images where gradual changes in intensity are replaced by abrupt steps, visible as false edges or bands. Also known as posterization.
-   **DC Coefficient:** (Direct Current) In DCT-based compression, the coefficient $F(0,0)$ representing the average intensity or color of an 8x8 block (the lowest spatial frequency).
-   **DCT (Discrete Cosine Transform):** A mathematical transform used extensively in lossy compression (JPEG, MPEG) to convert spatial image data into frequency components, concentrating energy into low frequencies.
-   **Dilation:** A basic morphological operation that expands or thickens foreground objects in an image. ($A \oplus B$).
-   **DPCM (Differential Pulse Code Modulation):** A technique that encodes the difference between a current sample/value and a prediction (often the previous sample/value), exploiting temporal or spatial redundancy. Used for DC coefficients in JPEG.
-   **Entropy Coding:** Lossless compression techniques (e.g., Huffman, Arithmetic coding) that assign codes based on symbol probabilities to reduce coding redundancy, approaching the theoretical minimum average code length (entropy).
-   **EOB (End-of-Block):** A special code used in JPEG's RLE stage to signify that all remaining AC coefficients in the current 8x8 block are zero.
-   **Erosion:** A basic morphological operation that shrinks or thins foreground objects in an image. ($A \ominus B$).
-   **Fidelity Criteria:** Measures used to assess the quality of a reconstructed image after lossy compression, comparing it to the original. Can be objective (mathematical error) or subjective (human perception).
-   **Graininess:** An artifact in quantized images perceived as random noise or texture, often due to the reduction of smooth tonal gradations.
-   **Hit-or-Miss Transform (HMT):** A morphological operation used for detecting specific patterns (foreground and background) in a binary image via template matching using two structuring elements.
-   **Huffman Coding:** A popular lossless entropy coding algorithm that builds a variable-length prefix code tree based on symbol probabilities to minimize average code length.
-   **Human Visual System (HVS):** The perceptual system of human eye and brain, whose characteristics (e.g., lower sensitivity to high frequencies) are exploited by psychovisual redundancy removal in lossy compression.
-   **IGS (Improved Grey Scale) Quantization:** A lossy quantization technique that adds pseudo-random noise (dithering) before quantization to reduce visible contouring artifacts.
-   **Image Compression:** The process of reducing the amount of data needed to represent a digital image by removing redundancies. Can be lossless or lossy.
-   **Interpixel Redundancy:** Correlation between adjacent pixel values in an image (spatial redundancy). Exploited by RLE, DPCM, transform coding.
-   **JPEG (Joint Photographic Experts Group):** A standard and file format for lossy compression of continuous-tone images, primarily based on DCT, quantization, and entropy coding. Also defines lossless, progressive, and hierarchical modes.
-   **Lossless Compression:** Compression techniques where the original data can be perfectly reconstructed from the compressed data (e.g., RLE, Huffman, PNG, GIF).
-   **Lossy Compression:** Compression techniques that achieve higher compression ratios by permanently discarding some information deemed less important, resulting in an approximation of the original (e.g., JPEG, MP3).
-   **Morphological Operations:** Non-linear image processing operations based on shape, using a structuring element to probe and modify image features (e.g., dilation, erosion, opening, closing).
-   **Objective Fidelity Criteria:** Mathematical measures of the difference (error) between an original and a lossy-compressed image (e.g., RMS Error, PSNR).
-   **Opening:** A compound morphological operation (erosion followed by dilation) used to remove small objects, break thin connections, and smooth contours from the inside. ($A \circ B = (A \ominus B) \oplus B$).
-   **Psychovisual Redundancy:** Information in an image that is less important or imperceptible to the human visual system, which can be discarded in lossy compression.
-   **Quantization:** The process of reducing the number of possible values for a signal or coefficient, typically by rounding or truncation. The main source of information loss in lossy transform coding like JPEG.
-   **Quantization Table:** In JPEG, an 8x8 table specifying the step size used to quantize each of the 64 DCT coefficients. Larger values cause more information loss.
-   **Relative Data Redundancy ($R_D$):** A measure related to the compression ratio, defined as $R_D = 1 - 1/C_R$.
-   **RLE (Run-Length Encoding):** A lossless compression technique that replaces sequences (runs) of identical data values with a count and the value. Used for AC coefficients in JPEG.
-   **Structuring Element (SE):** A small binary matrix (shape/template) with an origin, used as a probe in morphological operations.
-   **Subjective Fidelity Criteria:** Assessment of lossy compression quality based on human perception and opinion (e.g., rating scales, side-by-side comparison).
-   **Transform Coding:** A compression strategy that transforms data (e.g., image blocks) into another domain (e.g., frequency via DCT, or wavelet) where redundancy can be more effectively removed, typically via quantization.
-   **Vector Quantization (VQ):** A lossy compression technique that quantizes groups of samples (vectors, e.g., image blocks) by mapping them to entries in a codebook.
-   **Zig-Zag Scan:** The specific pattern used in JPEG to reorder the 64 quantized DCT coefficients from an 8x8 block into a 1D vector, grouping low frequencies first and facilitating RLE of zero coefficients.
