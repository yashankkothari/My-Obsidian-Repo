
# Chapter 3: Image Transform: Frequency Domain Representation and Enhancement

## Course Outcome (CO3)

- Understand and apply image transforms for frequency domain representation and enhancement techniques.

## Chapter Outline

### 3.1 Introduction to Frequency Domain

- Introduction
- **Discrete Fourier Transform (DFT)** and its properties
- Radix-2 algorithm (specifically 2-point DFT)
- **Fast Fourier Transform (FFT)** algorithm:
    - Divide and conquer approach
    - Decimation in Time (DIT)-FFT

### 3.2 Other Important Image Transforms

- **Discrete Cosine Transform (DCT)**
- **Walsh Transform**
- **Hadamard Transform**
- **Haar Transform**
- **Principal Component Analysis (PCA)** / **Hotelling Transform** (also known as Karhunen-Loève Transform or KLT)
- Introduction to **Wavelet Transform**

### 3.3 Frequency Domain Filtering

- Low Pass (LP) and High Pass (HP) Frequency domain filters:
    - Ideal Filters (ILPF, IHPF)
    - Butterworth Filters (BLPF, BHPF)
    - Gaussian Filters (GLPF, GHPF)
- **Homomorphic Filter**

### Self-Learning Topic

- Discrete Sine Transform (DST)

---

## 3.1 Introduction to Frequency Domain & DFT

### What are Image Transforms?

*[Insert Image: Basic Concept of Transformation - From Page 23, Fig 4.2]*

- **Image Transforms** are powerful mathematical tools used extensively in image processing and analysis.
- They allow us to change the representation of an image from one domain to another, most commonly from the **spatial domain** (pixels arranged by location) to the **frequency domain** (pixels arranged by their rate of change, or frequency).
- **Why Transform?** Migrating to a different domain often makes specific tasks much easier to perform.
    - **Mathematical Convenience:** Complex operations like convolution in the spatial domain become simpler multiplication in the frequency domain.
    - **Extracting Information:** Transforms can reveal information not easily visible in the spatial domain, like the constituent frequencies of an image (similar to how a prism separates white light into its color spectrum).

*[Insert Image: Mathematical Convenience Diagram (Convolution vs. Multiplication) - From Page 22]*
*[Insert Image: Analogy: Prism splitting white light - From Page 23, Fig 4.1]*

- **Information Preservation:** Importantly, transforms themselves do not change the *information content* present in the signal; they just represent it differently.
- **Applications:** Transforms are fundamental to:
    - Image Analysis
    - Image Enhancement
    - Image Filtering (Noise Reduction, Sharpening)
    - Image Compression
    - Fast computation of convolution and correlation.

### Need for Transforms Summarized

- Most signals and images are initially acquired or represented as **time-domain** (for 1D signals) or **spatial-domain** (for 2D images) signals, where the value is measured as a function of time or spatial coordinates.
- This representation isn't always the most effective for processing or analysis.
- Applying mathematical transformations allows us to extract further, often hidden, information or perform operations more efficiently.

### Discrete Fourier Transform (DFT)

- The **Discrete Fourier Transform (DFT)** converts a finite sequence of equally-spaced samples of a function (e.g., pixel values along a line or in an image) into a same-length sequence of equally-spaced samples of its frequency representation.

#### DFT Formula (1D)

- The DFT for a finite sequence $x(n)$ of length $N$ is given by $X(k)$:
  $$
  X(k) = \sum_{n=0}^{N-1} x(n) e^{-j 2 \pi \frac{kn}{N}} \quad \text{for } k = 0, 1, 2, \dots, N-1
  $$
  *[Insert Image: DFT Formula - From Page 2]*
- **Explanation:**
    - $x(n)$: Input sequence (e.g., pixel values) at discrete time/spatial index $n$.
    - $X(k)$: DFT coefficient at discrete frequency index $k$. Represents the amplitude and phase of a specific frequency component.
    - $N$: Length of the sequence (number of samples). Corresponds to the time duration or spatial extent for discrete signals.
    - $n$: Index for the input sequence samples ($0$ to $N-1$).
    - $k$: Index for the frequency components ($0$ to $N-1$).
    - $e^{-j 2 \pi \frac{kn}{N}}$: The **DFT basis function** (a complex exponential). It represents a sinusoid/cosinusoid of a specific frequency.
    - $j$: Imaginary unit ($\sqrt{-1}$).
    - The summation is evaluated for the finite sequence from $n=0$ to $N-1$.
- **Frequency Interpretation:**
    - The term $k/N$ corresponds to the discrete frequency $F$. The $k=0$ term represents the DC component (average value), and higher values of $k$ represent higher frequencies (faster changes in the signal).

#### DFT Output: Magnitude and Phase

- Since the DFT output $X(k)$ is generally complex, it's often represented by its magnitude and phase:
    - **Magnitude Function** $|X(k)|$: Represents the strength or amplitude of each frequency component.
      $$
      |X(k)| = \sqrt{ (\text{Re}\{X(k)\})^2 + (\text{Im}\{X(k)\})^2 }
      $$
      (Where Re is the real part and Im is the imaginary part. Sometimes denoted as $X_r(k)$ and $X_i(k)$).
      $$
      |X(k)| = \sqrt{X_r^2(k) + X_i^2(k)}
      $$
      *[Insert Image: DFT Magnitude Formula - From Page 3]*
    - **Phase Function** $\angle X(k)$: Represents the phase shift of each frequency component.
      $$
      \angle X(k) = \text{atan2}(\text{Im}\{X(k)\}, \text{Re}\{X(k)\})
      $$
      (Using atan2 is preferred for correct quadrant). Alternatively:
      $$
      \angle X(k) = \tan^{-1}\left[\frac{X_i(k)}{X_r(k)}\right]
      $$
      *[Insert Image: DFT Phase Formula - From Page 3]*
    - **Power Spectrum:** $|X(k)|^2$ is often used and is called the power spectrum.

#### Inverse Discrete Fourier Transform (IDFT)

- The **Inverse Discrete Fourier Transform (IDFT)** converts the frequency domain representation $X(k)$ back to the original spatial/time domain sequence $x(n)$.
- The IDFT is defined as:
  $$
  x(n) = \frac{1}{N} \sum_{k=0}^{N-1} X(k) e^{j 2 \pi \frac{kn}{N}} \quad \text{for } n = 0, 1, 2, \dots, N-1
  $$
  *[Insert Image: IDFT Formula - From Page 4]*
- **Key Differences from DFT:**
    - $1/N$ scaling factor.
    - Positive sign in the exponent ($+j$).
- Both $k$ and $n$ are in the range $0, 1, 2, \dots, N-1$. For example, if $N=4$, then $k = 0, 1, 2, 3$ and $n = 0, 1, 2, 3$.

### Properties of DFT

Let $x(n)$ and $X(k)$ be a DFT pair: $x(n) \leftrightarrow X(k)$. Similarly, $x_1(n) \leftrightarrow X_1(k)$ and $x_2(n) \leftrightarrow X_2(k)$.

1.  **Periodicity:**
    - Both the time-domain sequence $x(n)$ and the frequency-domain sequence $X(k)$ are periodic with period $N$.
    - $x(n+N) = x(n)$ for all $n$.
    - $X(k+N) = X(k)$ for all $k$.
    *[Insert Image: Periodicity Property Formulas - From Page 5]*
    - **Simplified:** If you extend the signal or its spectrum beyond the $N$ points, they just repeat.

2.  **Linearity:**
    - The DFT is a linear operation. The DFT of a linear combination of signals is the same linear combination of their individual DFTs.
    - If $x(n) = a_1 x_1(n) + a_2 x_2(n)$, then $X(k) = a_1 X_1(k) + a_2 X_2(k)$.
    *[Insert Image: Linearity Property Diagram - From Page 6]*
    - **Simplified:** Scaling and adding signals in the time domain corresponds to scaling and adding their spectra in the frequency domain.

3.  **Circular Convolution:**
    - Multiplication in one domain corresponds to **circular convolution** in the other domain.
    - If $y(n) = x_1(n) \circledast x_2(n)$ (circular convolution), then $Y(k) = X_1(k) X_2(k)$.
    - Circular convolution of $x_1(n)$ and $x_2(n)$ is defined as:
      $$
      y(m) = \sum_{n=0}^{N-1} x_1(n) x_2((m-n)_N) = \sum_{n=0}^{N-1} x_1((m-n)_N) x_2(n)
      $$
      where $(m-n)_N$ means $(m-n)$ modulo $N$.
      *[Insert Image: Circular Convolution Property Diagram & Formula - From Page 7]*
    - **Simplified:** Multiplying the frequency spectra of two signals is equivalent to circularly convolving them in the time domain. This is crucial for efficient filtering via FFT. *Note: Standard linear convolution requires zero-padding to avoid wrap-around effects when using DFT/FFT.*

4.  **Multiplication:**
    - Conversely, multiplication in the time/spatial domain corresponds to circular convolution in the frequency domain (with a scaling factor).
    - If $y(n) = x_1(n) x_2(n)$, then $Y(k) = \frac{1}{N} X_1(k) \circledast X_2(k)$.
    *[Insert Image: Multiplication Property Diagram - From Page 8]*
    - **Simplified:** Multiplying two signals directly (point-wise) results in their spectra being circularly convolved.

5.  **Time Reversal:**
    - Reversing the sequence in time corresponds to reversing the sequence in frequency (with modulo N indexing).
    - If $y(n) = x((-n)_N) = x((N-n)_N)$, then $Y(k) = X((-k)_N) = X((N-k)_N)$.
    *[Insert Image: Time Reversal Property Diagram - From Page 9]*
    - **Simplified:** Flipping the signal backward in time flips its spectrum backward in frequency.

6.  **Circular Time Shift:**
    - Shifting the sequence circularly in time by $l$ samples corresponds to multiplying its DFT by a complex exponential phase factor.
    - If $y(n) = x((n-l)_N)$, then $Y(k) = X(k) e^{-j 2 \pi \frac{kl}{N}}$.
    *[Insert Image: Circular Time Shift Property Diagram - From Page 10]*
    - **Simplified:** Delaying a signal in time changes the phase of its frequency components, but not their magnitude.

7.  **Conjugation:**
    - The DFT of the complex conjugate of a sequence is related to the complex conjugate of the original DFT, but with frequency reversal.
    - DFT{$x^*(n)$} = $X^*((N-k)_N)$.
    *[Insert Image: Conjugation Property Formulas - From Page 11]*
    - **Simplified:** Taking the complex conjugate of the signal leads to a conjugate and frequency-reversed spectrum.
    - **Important Consequence (Symmetry for Real Inputs):** If $x(n)$ is real, then $x(n) = x^*(n)$. This implies $X(k) = X^*((N-k)_N)$. This means the magnitude spectrum is symmetric ($|X(k)| = |X(N-k)|$) and the phase spectrum is anti-symmetric ($\angle X(k) = - \angle X(N-k)|$). We only need to compute/store roughly half the DFT coefficients for real signals.

*(Other properties like Parseval's Theorem exist but are not covered in these specific slides).*

#### DFT Properties Mnemonics

Think "LP CC M TCS TC":
- **L**inearity
- **P**eriodicity
- **C**ircular **C**onvolution <=> Multiplication
- **M**ultiplication <=> Circular Convolution
- **T**ime **S**hift <=> Phase Multiplication
- **T**ime Reversal <=> Frequency Reversal
- **C**onjugation Property

### Fast Fourier Transform (FFT)

- The **Fast Fourier Transform (FFT)** is not a different transform, but rather a highly efficient **algorithm** for computing the DFT.
- **Problem:** Direct computation of DFT requires approximately $O(N^2)$ complex multiplications and additions. This becomes computationally very expensive for large $N$.
- **Solution:** FFT reduces the number of calculations significantly, typically to $O(N \log N)$.
- **Approach:** FFT algorithms achieve this computational efficiency using a **divide and conquer** strategy.
    - The core idea is to break down an $N$-point DFT into successively smaller DFTs.

#### Radix-2 FFT

- A common family of FFT algorithms, particularly when $N$ is a power of 2.
- Let $N = 2^m$, where $m$ is an integer.
- **Stages:** The computation involves $m = \log_2 N$ stages.
- **Decimation:** An $N$-point sequence is broken down (decimated) into two $(N/2)$-point sequences. These are further broken down until we reach 2-point DFTs, which are trivial to compute. The results are then combined efficiently.
    - Example: An 8-point DFT ($N=8, m=3$) is broken into two 4-point DFTs, which are each broken into two 2-point DFTs. There are 3 stages of computation.

#### Phase Factor / Twiddle Factor

- The complex exponential term $e^{-j 2 \pi / N}$ appears frequently in DFT and FFT calculations. It is often represented by $W_N$.
- **Twiddle Factor Definition:**
  $$
  W_N = e^{-j 2 \pi / N}
  $$
  So the DFT formula can be written as:
  $$
  X(k) = \sum_{n=0}^{N-1} x(n) W_N^{kn}
  $$
  *[Insert Image: DFT Formula with W_N notation - From Page 14]*
- The term $W_N^{kn}$ is the specific twiddle factor used in the calculation.
- These factors have symmetry and periodicity properties that FFT algorithms exploit to reduce calculations.
  *[Insert Image: Twiddle Factor Definition W = e^(-j2*pi) - From Page 14 - Note: This seems incomplete, should be W_N]*
- Twiddle factors can be multiplied or divided (powers can be added/subtracted).

#### Decimation in Time (DIT) FFT

- One of the main types of Radix-2 FFT algorithms.
- **Process:** It works by breaking the input sequence $x(n)$ into smaller sub-sequences (even and odd indices) recursively.
- **Butterfly Diagram:** The computational flow of DIT-FFT is often visualized using a **butterfly diagram**. Each butterfly represents a 2-point DFT calculation and combination step.
    - **Basic Butterfly Operation:**
        *[Insert Image: Basic DIT-FFT Butterfly Structure - From Page 15]*
        - Takes two complex inputs (e.g., $a$ and $b$).
        - Multiplies $b$ by a twiddle factor $W_N^k$.
        - Computes outputs $A = a + b W_N^k$ and $B = a - b W_N^k$.
    - **Full Diagram:** Connecting these butterflies across $\log_2 N$ stages computes the full DFT. The inputs might need to be reordered (bit-reversal permutation), and the outputs will be in natural order (or vice-versa depending on the specific algorithm variant).
        *[Insert Image: Handwritten 8-point DIT-FFT Butterfly Diagram - From Page 16]*
        *[Insert Image: Handwritten Twiddle Factor Calculations (W2, W4) - From Page 17]*
        *[Insert Image: Handwritten Twiddle Factor Calculations (W8) - From Page 18]*
        - **Description:** The diagram shows an 8-point DIT-FFT. Inputs $x(0)$ to $x(7)$ are on the left (potentially in bit-reversed order, as indicated by "Input Reversed"). The computation flows through three stages ($\log_2 8 = 3$). Each stage combines results from the previous stage using butterfly operations with specific twiddle factors ($W_8^0, W_8^1, W_8^2, W_8^3$, etc.). The final outputs $X(0)$ to $X(7)$ appear on the right in natural order. The handwritten notes show calculations for the required twiddle factors $W_2$, $W_4$, and $W_8$.

#### FFT Computational Efficiency

- FFT significantly reduces the number of complex multiplications and additions compared to direct DFT computation.

| Number of points N | Direct DFT Complex Additions N(N-1) | Direct DFT Complex Multiplications N² | Radix-2 FFT Complex Additions N log₂ N | Radix-2 FFT Complex Multiplications (N/2) log₂ N |
| :----------------- | :---------------------------------- | :----------------------------------- | :------------------------------------- | :---------------------------------------------- |
| 4 ($2^2$)         | 12                                  | 16                                   | $4 \times 2 = 8$                       | $(4/2) \times 2 = 4$                            |
| 8 ($2^3$)         | 56                                  | 64                                   | $8 \times 3 = 24$                      | $(8/2) \times 3 = 12$                           |
| 16 ($2^4$)        | 240                                 | 256                                  | $16 \times 4 = 64$                     | $(16/2) \times 4 = 32$                          |
| 32 ($2^5$)        | 992                                 | 1,024                                | $32 \times 5 = 160$                    | $(32/2) \times 5 = 80$                          |
| 64 ($2^6$)        | 4,032                               | 4,096                                | $64 \times 6 = 384$                    | $(64/2) \times 6 = 192$                         |
| 128 ($2^7$)       | 16,256                              | 16,384                               | $128 \times 7 = 896$                   | $(128/2) \times 7 = 448$                        |

*[Insert Image: Table comparing DFT and FFT computations - From Page 19]*

- **Significance:** The difference becomes dramatic for large images (e.g., N=1024x1024). FFT makes frequency domain processing computationally feasible.

### Unitary Transforms

- A discrete linear transform is **unitary** if its transform matrix $A$ conforms to the unitary condition:
  $$
  A \times A^H = I \quad \text{or} \quad A^H \times A = I
  $$
  *[Insert Image: Unitary Condition Formula - From Page 30]*
  Where:
    - $A$: Transformation matrix.
    - $A^H$: **Hermitian transpose** (or conjugate transpose) of $A$. Calculated as $A^H = (A^*)^T$, meaning take the complex conjugate of each element ($A^*$) and then transpose the matrix ($T$).
    - $I$: Identity matrix.
- If a transform matrix $A$ is unitary, the defined transform is called a **unitary transform**.

#### Properties of Unitary Transforms

- **Signal Energy Preservation:** Unitary transforms preserve the signal energy (Parseval's Theorem is related). The energy calculated in the original domain equals the energy calculated in the transformed domain.
- **Energy Compaction:** Most unitary transforms used in image processing tend to pack a large fraction of the image energy into relatively few transform coefficients.
    - Typically, only a few coefficients (often those corresponding to low frequencies, close to the origin of the transform domain) have significant values.
- **Application:** This energy compaction property is fundamental to **image compression**, as many small coefficients can be discarded or quantized heavily with minimal perceptual loss.

#### Orthogonal Transform

- If a transform matrix $A$ is unitary **and** has only real elements, then $A^H = A^T$ (since $A^* = A$).
- The condition becomes $A \times A^T = I$.
- Such a real unitary matrix is called an **orthogonal matrix**.
- The corresponding transform is an **orthogonal transform**.
  $$
  A \text{ is orthogonal if } A \cdot A^T = I
  $$
  *[Insert Image: Orthogonal Matrix Condition - From Page 31]*
- **Examples:** DCT, Hadamard, Haar transforms often use orthogonal matrices. DFT uses a unitary matrix (it's complex).

#### Example: Checking if the DFT Matrix is Unitary

- **Goal:** Check if the 4-point DFT matrix ($N=4$) satisfies the unitary condition $A \times A^H = I$.

1.  **Determine the DFT Matrix A:**
    - Use the DFT formula $X(k) = \sum_{n=0}^{3} x(n) e^{-j 2 \pi kn / 4}$ for $k=0, 1, 2, 3$.
    - Find the coefficients for $x(0), x(1), x(2), x(3)$ for each $X(k)$.
    *[Insert Image: Step 1 - Finding X(0) - From Page 32]*
    *[Insert Image: Step 1 - Finding X(1) - From Page 33]*
    *[Insert Image: Step 1 - Finding X(2) - From Page 33]*
    *[Insert Image: Step 1 - Finding X(3) & Matrix A - From Page 34]*
    - The resulting unnormalized DFT matrix $A_{un}$ is:
      $$
      A_{un} = \begin{bmatrix}
      1 & 1 & 1 & 1 \\
      1 & -j & -1 & j \\
      1 & -1 & 1 & -1 \\
      1 & j & -1 & -j
      \end{bmatrix}
      $$
    - *Note:* Often, the DFT matrix is normalized by $1/\sqrt{N}$ to make it truly unitary. The example seems to check if $A_{un} \times A_{un}^H = N \times I$. Let's follow the example's steps.

2.  **Compute the Hermitian Transpose $A^H$:**
    - Step 2a: Find the complex conjugate $A^*$. Change $j$ to $-j$.
      *[Insert Image: Step 2a - Conjugate A* - From Page 35]*
      $$
      A_{un}^* = \begin{bmatrix}
      1 & 1 & 1 & 1 \\
      1 & j & -1 & -j \\
      1 & -1 & 1 & -1 \\
      1 & -j & -1 & j
      \end{bmatrix}
      $$
    - Step 2b: Find the transpose $(A^*)^T$. Swap rows and columns.
      *[Insert Image: Step 2b - Transpose (A*)^T = A^H - From Page 36]*
      $$
      A_{un}^H = (A_{un}^*)^T = \begin{bmatrix}
      1 & 1 & 1 & 1 \\
      1 & j & -1 & -j \\
      1 & -1 & 1 & -1 \\
      1 & -j & -1 & j
      \end{bmatrix}^T = \begin{bmatrix}
      1 & 1 & 1 & 1 \\
      1 & j & -1 & -j \\
      -1 & -1 & 1 & -1 \\
      1 & -j & -1 & j
      \end{bmatrix}
      $$
      *Correction:* The calculation shown on Page 36 seems incorrect. Let's re-calculate $A_{un}^H$.
      $$
       A_{un}^* = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & j & -1 & -j \\ 1 & -1 & 1 & -1 \\ 1 & -j & -1 & j \end{bmatrix}
      $$
      $$
       A_{un}^H = (A_{un}^*)^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & j & -1 & -j \\ 1 & -1 & 1 & -1 \\ 1 & -j & -1 & j \end{bmatrix}^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & j & -1 & -j \\ 1 & -1 & 1 & -1 \\ 1 & -j & -1 & j \end{bmatrix} \quad \text{(Oops, matrix A* is correct, but the transpose on page 36 seems wrong. Let's assume the matrix A on page 36 is correct A and A^H calculation from it is correct.)}
      $$
      Let's use the matrix A and A^H as shown on Page 36:
      $$
      A = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix} \quad A^H = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & j & -1 & -j \\ 1 & -1 & 1 & -1 \\ 1 & -j & -1 & j \end{bmatrix}
      $$

3.  **Determine $A \times A^H$:**
    - Multiply the matrix $A$ by its Hermitian transpose $A^H$.
    *[Insert Image: Step 3 - Determination of A x A^H - From Page 36]*
    - The calculation shows:
      $$
      A \times A^H = \begin{bmatrix} 4 & 0 & 0 & 0 \\ 0 & 4 & 0 & 0 \\ 0 & 0 & 4 & 0 \\ 0 & 0 & 0 & 4 \end{bmatrix} = 4 \times \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} = 4I = NI
      $$
- **Conclusion:** The result is $N \times I$. This shows the unnormalized DFT matrix satisfies $A \times A^H = NI$. If we used the normalized DFT matrix $A_{norm} = \frac{1}{\sqrt{N}} A$, then $A_{norm} \times A_{norm}^H = (\frac{1}{\sqrt{N}} A) \times (\frac{1}{\sqrt{N}} A^H) = \frac{1}{N} (A \times A^H) = \frac{1}{N} (NI) = I$. Therefore, the **normalized** DFT is a unitary transform.

### 2D DFT for Images

- Images are 2D signals $f(m, n)$. The 2D DFT $F(k, l)$ can be computed using a **separable** approach: apply the 1D DFT along each row, and then apply the 1D DFT along each column of the result (or vice-versa).
- **Matrix Formulation:** Using the (normalized) 1D DFT matrix $A$, the 2D DFT $F$ of an image matrix $f$ can be computed as:
  $$
  F = A \times f \times A^T
  $$
  (If A is complex/unitary, use $A^H$ or $A^*$ depending on convention, but often $A^T$ is shown assuming separability structure).
  The example uses the unnormalized DFT matrix (Kernel) $K$:
  $$
  F[k, l] = K \times f[m, n] \times K^T
  $$
  *[Insert Image: 2D DFT Concept and Formula - From Page 38]*

#### Example: Compute 2D DFT of a 4x4 Grayscale Image

- **Input Image:** A 4x4 matrix $f[m, n]$ of all ones.
  $$
  f[m, n] = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \end{bmatrix}
  $$
- **DFT Basis (Kernel) for N=4:** The unnormalized DFT matrix $K = A_{un}$.
  $$
  K = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix}
  $$
  *[Insert Image: Input Image and DFT Kernel - From Page 38]*
- **Calculation:** $F(k, l) = K \times f \times K^T$ (Note: The example uses $K$ for both pre and post multiplication, suggesting $K^T$ might be implicitly used or the kernel is symmetric in some way - DFT Kernel is not symmetric, $K^T$ should be used. Let's follow the image calculation).
  $$
  F(k, l) = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix} \times \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \end{bmatrix} \times \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix}
  $$
  *[Insert Image: 2D DFT Matrix Multiplication Setup - From Page 39]*
  First multiplication $K \times f$:
  $$
  K \times f = \begin{bmatrix} 4 & 4 & 4 & 4 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix}
  $$
  Second multiplication $(K \times f) \times K$ (as shown in image, assuming $K$ instead of $K^T$):
  $$
  \begin{bmatrix} 4 & 4 & 4 & 4 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix} \times \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix} = \begin{bmatrix} 16 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix}
  $$
  *[Insert Image: 2D DFT Matrix Multiplication Result - From Page 39]*
- **Result:**
  $$
  F(k, l) = \begin{bmatrix} 16 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix}
  $$
- **Interpretation:** The only non-zero coefficient is $F(0, 0)$, the DC component. This makes sense because the input image is constant (zero frequency). $F(0,0) = N \times N \times \text{average pixel value} = 4 \times 4 \times 1 = 16$.

#### Example: Compute Inverse 2D DFT

- **Input:** The transform coefficients $F(k, l)$ calculated above.
  $$
  F[k, l] = \begin{bmatrix} 16 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix}
  $$
  *[Insert Image: Inverse 2D DFT Input F[k,l] - From Page 40]*
- **Inverse 2D DFT Formula:** Using the unnormalized kernel $K$:
  $$
  f[m, n] = \frac{1}{N^2} \times K^* \times F[k, l] \times (K^*)^T \quad \text{(Common form)}
  $$
  Or, using the IDFT relationship $A_{IDFT} = \frac{1}{N} A_{DFT}^*$:
  Let the Inverse Kernel be $K_{inv}$. $K_{inv} = \frac{1}{N} K^*$.
  $$
  f[m, n] = K_{inv} \times F[k, l] \times K_{inv}^T
  $$
  The formula provided in the slide uses a slightly different structure involving $K$ and $K^T$ with a scaling factor:
  $$
  f[m, n] = \frac{1}{N^2} \times K \times F[k, l] \times K^T \quad \text{(Formula from slide, for N=4)}
  $$
  *Note: There might be inconsistencies in using $K, K^*, K^T, K^H$. Let's follow the slide's calculation flow.*
  The slide formula seems to be: $f[m, n] = \frac{1}{N^2} \times \text{kernel} \times F[k, l] \times (\text{kernel})^T$
  It calculates: $f[m, n] = \frac{1}{16} K \times F \times K^T$
  $$
  f[m, n] = \frac{1}{16} \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix} \begin{bmatrix} 16 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 \end{bmatrix} \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix}^T
  $$
  *[Insert Image: Inverse 2D DFT Calculation Steps - From Page 41]*
  Calculation:
  $$
  K \times F = \begin{bmatrix} 16 & 0 & 0 & 0 \\ 16 & 0 & 0 & 0 \\ 16 & 0 & 0 & 0 \\ 16 & 0 & 0 & 0 \end{bmatrix}
  $$
  $$
  K^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix}^T = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix} \quad \text{(Kernel is symmetric? No, K != K^T. Let's use K as written in example.)}
  $$
  $(K \times F) \times K^T = \begin{bmatrix} 16 & 0 & 0 & 0 \\ 16 & 0 & 0 & 0 \\ 16 & 0 & 0 & 0 \\ 16 & 0 & 0 & 0 \end{bmatrix} \times \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -j & -1 & j \\ 1 & -1 & 1 & -1 \\ 1 & j & -1 & -j \end{bmatrix} = \begin{bmatrix} 16 & 16 & 16 & 16 \\ 16 & 16 & 16 & 16 \\ 16 & 16 & 16 & 16 \\ 16 & 16 & 16 & 16 \end{bmatrix}$
  Finally, multiply by $1/16$:
  $$
  f[m, n] = \frac{1}{16} \begin{bmatrix} 16 & 16 & 16 & 16 \\ 16 & 16 & 16 & 16 \\ 16 & 16 & 16 & 16 \\ 16 & 16 & 16 & 16 \end{bmatrix} = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \\ 1 & 1 & 1 & 1 \end{bmatrix}
  $$
  *[Insert Image: Final Result of Inverse 2D DFT - From Page 42]*
- **Result:** We correctly recovered the original image matrix $f[m, n]$.

---

## 3.2 Other Important Image Transforms

### Classification of Image Transforms

*[Insert Image: Diagram Classifying Image Transforms - From Page 24]*

- **Description:** This diagram classifies image transforms based on their basis functions:
    1.  **Orthogonal Sinusoidal Basis Functions:** Basis functions are sines and cosines.
        - Examples: Fourier Transform (DFT), Discrete Cosine Transform (DCT), Discrete Sine Transform (DST).
    2.  **Non-sinusoidal Orthogonal Basis Functions:** Basis functions are orthogonal but not sines/cosines (often piecewise constant or square waves).
        - Examples: Haar Transform, Walsh Transform, Hadamard Transform, Slant Transform.
    3.  **Basis Function Depending on Statistics:** Basis functions are derived from the input signal's statistics (data-dependent).
        - Examples: Karhunen-Loève Transform (KLT) / PCA, Singular Value Decomposition (SVD).
    4.  **Directional Transformation:** Basis functions are designed to capture directional features effectively.
        - Examples: Hough Transform, Radon Transform, Ridgelet Transform, Contourlet Transform.

#### 1) Orthogonal Sinusoidal Basis Function Transforms

- **Fourier Transform (DFT/FFT):** Already discussed. Powerful general-purpose transform. Basis functions are complex exponentials (sines and cosines).
- **Discrete Cosine Transform (DCT):**
    - Belongs to a family of **real-valued** discrete sinusoidal **unitary (orthogonal)** transforms.
    - **Basis Vectors:** Consist of sampled cosine functions.
    - **Key Use:** Widely used in **image compression** (e.g., JPEG standard).
    - **Reason for Use in Compression:** Excellent **energy compaction** for highly correlated data like images. It packs most signal energy into a few low-frequency coefficients. Avoids complex numbers, unlike DFT.

#### 2) Non-sinusoidal Orthogonal Basis Function Transforms

- These transforms use basis functions that are not sinusoidal (e.g., square waves, piecewise functions).
- **Examples:** Walsh, Hadamard, Haar.
- **Wavelet Transform:** An important class mentioned here. A key advantage is its ability to represent signals (images) in **different resolutions** (multi-resolution analysis), providing both frequency and spatial localization, unlike DFT/DCT which only give frequency localization.

#### 3) Basis Function Depending on Statistics of Input Signal

- The basis functions are not fixed but are derived from the statistical properties (e.g., covariance matrix) of the input signal itself.
- **Karhunen-Loève Transform (KLT)** (also called Hotelling Transform or PCA):
    - Considered the **optimal** linear transform in terms of **energy compaction** and **decorrelation**. It provides the best representation using the fewest coefficients for a given signal class, on average.
    - **Drawback:** Data-dependent (basis functions must be calculated for each image or image class), computationally more expensive than fixed transforms like DCT or DFT.
- **Singular Value Decomposition (SVD):** Related technique also based on data statistics.

#### 4) Directional Transformation

- Basis functions are specifically designed to be effective in representing **directional information** within a signal or image (e.g., lines, edges, contours).
- **Examples:** Hough Transform (detecting lines/circles), Radon Transform (used in tomography), Ridgelet, Contourlet (better at capturing curved edges than wavelets).

### Discrete Cosine Transform (DCT)

- As mentioned, DCT is a real-valued, orthogonal transform using cosine basis functions.
- Widely used in image and video compression (JPEG, MPEG, etc.).

#### 1D DCT Formula (Type-II DCT is common)

- The kernel (basis function) of a one-dimensional DCT is given by:
  $$
  X[k] = \alpha(k) \sum_{n=0}^{N-1} x[n] \cos\left[\frac{(2n+1)k\pi}{2N}\right], \quad \text{where } 0 \le k \le N-1
  $$
  With the normalization factor $\alpha(k)$:
  $$
  \alpha(k) = \begin{cases} \sqrt{\frac{1}{N}} & \text{if } k = 0 \\ \sqrt{\frac{2}{N}} & \text{if } k \neq 0 \end{cases}
  $$
  *[Insert Image: 1D DCT Formula and alpha(k) definition - From Page 44]*

#### Example: Compute the DCT Matrix for N = 4

- **Goal:** Find the 4x4 transformation matrix for the DCT.
- **Formula:**
  $$
  X[k] = \alpha(k) \sum_{n=0}^{3} x[n] \cos\left[\frac{(2n+1)k\pi}{8}\right]
  $$
  *[Insert Image: DCT Example Setup N=4 - From Page 45]*
- **Calculate row k=0:** $$\alpha(0) = \sqrt{1/4} = 1/2$. $\cos(0) = 1$$
  $$
  X[0] = \frac{1}{2} \sum_{n=0}^{3} x[n] (1) = 0.5x(0) + 0.5x(1) + 0.5x(2) + 0.5x(3)
  $$
  *[Insert Image: DCT Calculation for k=0 - From Page 46]*
- **Calculate row k=1:** $\alpha(1) = \sqrt{2/4} = 1/\sqrt{2} \approx 0.707$.
  $$
  X[1] = \frac{1}{\sqrt{2}} \sum_{n=0}^{3} x[n] \cos\left[\frac{(2n+1)\pi}{8}\right]
  $$
  $X[1] = \frac{1}{\sqrt{2}} [x(0)\cos(\frac{\pi}{8}) + x(1)\cos(\frac{3\pi}{8}) + x(2)\cos(\frac{5\pi}{8}) + x(3)\cos(\frac{7\pi}{8})]$
  $X[1] \approx 0.707 [x(0)(0.9239) + x(1)(0.3827) + x(2)(-0.3827) + x(3)(-0.9239)]$
  $X[1] \approx 0.6532x(0) + 0.2706x(1) - 0.2706x(2) - 0.6532x(3)$
  *[Insert Image: DCT Calculation for k=1 - From Page 47]*
- **Calculate row k=2:** $\alpha(2) = \sqrt{2/4} = 1/\sqrt{2}$.
  $$
  X[2] = \frac{1}{\sqrt{2}} \sum_{n=0}^{3} x[n] \cos\left[\frac{(2n+1)2\pi}{8}\right] = \frac{1}{\sqrt{2}} \sum_{n=0}^{3} x[n] \cos\left[\frac{(2n+1)\pi}{4}\right]
  $$
  $$X[2] = \frac{1}{\sqrt{2}} [x(0)\cos(\frac{\pi}{4}) + x(1)\cos(\frac{3\pi}{4}) + x(2)\cos(\frac{5\pi}{4}) + x(3)\cos(\frac{7\pi}{4})]$$
  $$X[2] \approx 0.7071 [x(0)(0.7071) + x(1)(-0.7071) + x(2)(-0.7071) + x(3)(0.7071)]$$
  $$X[2] \approx 0.5x(0) - 0.5x(1) - 0.5x(2) + 0.5x(3)$$
  *[Insert Image: DCT Calculation for k=2 - From Page 48]*
- **Calculate row k=3:** $\alpha(3) = \sqrt{2/4} = 1/\sqrt{2}$.
  $$
  X[3] = \frac{1}{\sqrt{2}} \sum_{n=0}^{3} x[n] \cos\left[\frac{(2n+1)3\pi}{8}\right]
  $$
  $X[3] = \frac{1}{\sqrt{2}} [x(0)\cos(\frac{3\pi}{8}) + x(1)\cos(\frac{9\pi}{8}) + x(2)\cos(\frac{15\pi}{8}) + x(3)\cos(\frac{21\pi}{8})]$
  $X[3] \approx 0.7071 [x(0)(0.3827) + x(1)(-0.9239) + x(2)(0.9239) + x(3)(-0.3827)]$
  $X[3] \approx 0.2706x(0) - 0.6533x(1) + 0.6533x(2) - 0.2706x(3)$
  *[Insert Image: DCT Calculation for k=3 - From Page 49]*
- **Collect coefficients into the DCT matrix T (or A):**
  $$
  \begin{bmatrix} X[0] \\ X[1] \\ X[2] \\ X[3] \end{bmatrix} = \begin{bmatrix}
  0.5 & 0.5 & 0.5 & 0.5 \\
  0.6532 & 0.2706 & -0.2706 & -0.6532 \\
  0.5 & -0.5 & -0.5 & 0.5 \\
  0.2706 & -0.6533 & 0.6533 & -0.2706
  \end{bmatrix} \begin{bmatrix} x[0] \\ x[1] \\ x[2] \\ x[3] \end{bmatrix}
  $$
  So the N=4 DCT Matrix is:
  $$
  T_{DCT, N=4} = \begin{bmatrix}
  0.5 & 0.5 & 0.5 & 0.5 \\
  0.653 & 0.271 & -0.271 & -0.653 \\
  0.5 & -0.5 & -0.5 & 0.5 \\
  0.271 & -0.653 & 0.653 & -0.271
  \end{bmatrix}
  $$
  (Using rounded values from calculation).
  *[Insert Image: Final DCT Matrix for N=4 - From Page 50]*
  *Verification:* This matrix should be orthogonal ($T \times T^T = I$).

#### Inverse DCT (IDCT)

- The Inverse DCT transforms the coefficients $X[k]$ back to the original sequence $x[n]$.
- Since the DCT matrix $T$ is orthogonal ($T^T = T^{-1}$), the IDCT is simply the transpose of the DCT matrix (possibly with scaling differences depending on normalization conventions).
- The formula for the IDCT (Type-III DCT) matching the Type-II DCT forward transform is:
  $$
  x[n] = \sum_{k=0}^{N-1} \alpha(k) X[k] \cos\left[\frac{(2n+1)k\pi}{2N}\right], \quad \text{where } 0 \le n \le N-1
  $$
  (Note the similarity to the forward transform, $\alpha(k)$ is applied again).
  *[Insert Image: IDCT Formula - From Page 51]*

#### 2D DCT

- Like the 2D DFT, the 2D DCT is separable. For an image matrix $f$ and DCT matrix $T$:
  $$
  F = T \times f \times T^T
  $$
- Because the DCT matrix $T$ is real and orthogonal, $T^T = T^{-1}$.
- **Symmetric vs. Asymmetric Transform Kernels:**
    - **Transformation Matrix:** T
    - **Image Matrix:** f
    - If the Transformation matrix T is **symmetric** ($T = T^T$):
        - $F = T \times f \times T$
    - If the Transformation matrix T is **asymmetric** ($T \neq T^T$):
        - $F = T \times f \times T'$ (where $T'$ usually means $T^T$)
    *[Insert Image: Symmetric/Asymmetric Formulas - From Page 52]*
    - **Note:** The DCT matrix is generally **not** symmetric. The Hadamard matrix (discussed next) **is** symmetric.

### Hadamard Transform

- An orthogonal transform using basis functions that are square waves (values +1 and -1).
- Computationally very simple (only additions and subtractions).
- **Hadamard Matrix:** A square matrix with entries +1 and -1, whose rows (and columns) are orthogonal.
- **Generation:** Hadamard matrices of order $2N$ can be generated recursively from a Hadamard matrix of order $N$ using the Kronecker product structure. Start with $H_1 = [1]$ or the core $H_2$:
  $$
  H_2 = \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}
  $$
  *[Insert Image: H2 Matrix - From Page 53]*
  Then,
  $$
  H_{2N} = \begin{bmatrix} H_N & H_N \\ H_N & -H_N \end{bmatrix}
  $$
  *[Insert Image: Recursive Hadamard Formula - From Page 53]*
- **Example H4:** Substituting $N=2$:
  $$
  H_4 = \begin{bmatrix} H_2 & H_2 \\ H_2 & -H_2 \end{bmatrix} = \begin{bmatrix} 1 & 1 & 1 & 1 \\ 1 & -1 & 1 & -1 \\ 1 & 1 & -1 & -1 \\ 1 & -1 & -1 & 1 \end{bmatrix}
  $$
  *[Insert Image: H4 Matrix Calculation - From Page 53]*
- **Example H8:** Substituting $N=4$:
  $$
  H_8 = \begin{bmatrix} H_4 & H_4 \\ H_4 & -H_4 \end{bmatrix} = \begin{bmatrix}
  1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
  1 & -1 & 1 & -1 & 1 & -1 & 1 & -1 \\
  1 & 1 & -1 & -1 & 1 & 1 & -1 & -1 \\
  1 & -1 & -1 & 1 & 1 & -1 & -1 & 1 \\
  1 & 1 & 1 & 1 & -1 & -1 & -1 & -1 \\
  1 & -1 & 1 & -1 & -1 & 1 & -1 & 1 \\
  1 & 1 & -1 & -1 & -1 & -1 & 1 & 1 \\
  1 & -1 & -1 & 1 & -1 & 1 & 1 & -1
  \end{bmatrix}
  $$
  *[Insert Image: H8 Matrix Calculation - From Page 54]*
- **Properties:** Hadamard matrices generated this way are **symmetric** ($H_N = H_N^T$).
- **Normalization:** To make the transform unitary/orthogonal, the matrix is usually normalized by $1/\sqrt{N}$. Let $T = \frac{1}{\sqrt{N}} H_N$. Then $T \times T^T = I$.

#### Hadamard Transform Formulas

- Let $H(N)$ be the (unnormalized) Hadamard matrix of order N.
- **Hadamard Transform of Sequence:**
    - $X = H(N) \cdot x$
    (Or $X[k] = \sum_n H_{kn} x[n]$)
- **Inverse Hadamard Transform of Sequence:**
    - Since $H(N)$ is symmetric and $H(N) \times H(N) = N \times I$, the inverse is $H^{-1}(N) = \frac{1}{N} H(N)$.
    - $x = \frac{1}{N} H(N) \cdot X$
    (Or $x[n] = \frac{1}{N} \sum_k H_{nk} X[k]$)
    *[Insert Image: 1D Hadamard Formulas - From Page 55]*
- **Hadamard Transform of Image (2D):**
    - Let $T$ be the normalized Hadamard matrix $T = \frac{1}{\sqrt{N}} H_N$.
    - Since Hadamard matrix is **symmetric**, $T=T^T$.
    - The 2D transform $F$ of image $f$ is:
        - $F = T \times f \times T$
    *[Insert Image: 2D Hadamard Formula - From Page 55]*

### Walsh Transform

- Closely related to the Hadamard transform. Uses the same basis vectors (+1, -1 values) but orders them differently.
- **Ordering:** Walsh functions are ordered by **sequency**, which is the number of zero-crossings (sign changes) per unit time interval. The Hadamard matrix generated by the recursive method has rows ordered by sequency only for $N=1, 2, 4, 8$. For larger $N$, the rows need reordering to get the Walsh matrix.
- **Walsh Matrix W(8):**
  *[Insert Image: H8 matrix showing sequency order (0,7,3,4,1,6,2,5) and the reordered W(8) matrix - From Page 56]*
  *[Insert Image: W(8) Walsh Matrix - From Page 57]*
- Computation and properties are similar to Hadamard, but the interpretation of coefficients relates directly to sequency.

### Haar Transform

- Another orthogonal transform using piecewise constant basis functions. It's the simplest wavelet transform.
- **Basis Functions:** Include a constant function and then functions capturing differences at different scales and locations (square pulses).
- Computationally very fast ($O(N)$ operations).
- **Matrices:**
    *[Insert Image: Haar Transform Hr2, Hr4 definition and Properties - From Page 58]*
    - Properties listed:
        1. Real and orthogonal: $Hr \cdot Hr^T = I$ (assuming normalized). $Hr^{-1} = Hr^T$.
        2. Very fast transform: $O(N)$ operations.
        3. Poor energy compaction for images compared to DCT or KLT.
    *[Insert Image: N=8 Haar Transform Matrix H3 - From Page 59]*
- **Use:** Useful in some applications due to speed and localization properties, but less common for image compression due to poorer energy compaction.

### Karhunen-Loève Transform (KLT) / Hotelling Transform / PCA

- Also called **Eigen Vector Transform**.
- **Foundation:** Based on the **statistical properties** (covariance) of the image data, not fixed basis functions.
- **Goal:** To decorrelate the data and achieve optimal energy compaction.
- **Relevance to Compression:**
    - Data in images, especially neighboring pixels, is usually **highly correlated**.
    - Directly compressing correlated data is inefficient.
    - KLT **decorrelates** the data by finding a new set of basis vectors (eigenvectors of the covariance matrix) along which the data variance is maximized and uncorrelated.
    - This decorrelation facilitates much higher degrees of compression because the transformed coefficients are largely independent, and energy is packed into the first few coefficients corresponding to the largest variances (eigenvalues).
- **Challenge:** Achieving compression without losing significant image quality is the main challenge KLT addresses optimally (among linear transforms).

#### Steps to Compute KLT

1.  **(Optional: Data Representation)** Represent the image or image blocks as vectors.
2.  **Find the Mean Vector:** Calculate the average vector $m$ over the dataset (e.g., average of all image blocks).
    *[Insert Image: Formula for Mean Vector mf - From Page 92]*
3.  **Find the Covariance Matrix:** Calculate the covariance matrix $C_x$ (or $C_f$) of the data vectors. This matrix describes how pixel values vary and co-vary.
    *[Insert Image: Formula for Covariance Matrix Cf - From Page 95]*
4.  **Find Eigenvalues and Eigenvectors:** Calculate the eigenvalues ($\lambda_i$) and eigenvectors ($v_i$) of the covariance matrix $C_x$.
    - Solve the characteristic equation $|C_x - \lambda I| = 0$ for eigenvalues $\lambda$.
    - For each $\lambda_i$, solve $(C_x - \lambda_i I) v_i = 0$ for the corresponding eigenvector $v_i$.
    *[Insert Image: Eigenvalue Calculation Setup - From Page 96]*
    *[Insert Image: Eigenvalue Results - From Page 97]*
    *[Insert Image: Eigenvector v1 Calculation - From Page 98]*
    *[Insert Image: Eigenvector v2 Calculation - From Page 99]*
    *[Insert Image: Eigenvector v2 Calculation cont. - From Page 100]*
5.  **Create Transformation Matrix T:** Form the matrix $T$ whose rows are the normalized eigenvectors, usually ordered from the one corresponding to the largest eigenvalue to the one corresponding to the smallest. (The eigenvectors form the basis functions).
    *[Insert Image: Eigenvector Normalization - From Page 101]*
    *[Insert Image: Final Transformation Matrix T - From Page 102]*
6.  **Transform the Data:** Transform each data vector $x$ (or $f_k$) by projecting it onto the new basis:
    - $X = T \cdot (x - m)$ (Subtract the mean first)
    *[Insert Image: KLT Transform Step - From Page 91 (Step iv)]*
    *[Insert Image: Example KLT Transformation of vectors F1, F2, F3, F4 - From Page 103]*

- **Summary of Example Calculation:** The pages show a step-by-step calculation for a small dataset: finding the mean vector, covariance matrix, eigenvalues, eigenvectors, normalizing eigenvectors, forming the transform matrix T, and finally transforming the original data vectors (columns of f) into the KLT coefficients (columns of F).

---

## Section Summary: Image Transforms

- **Purpose:** Represent image data in a different domain (often frequency) for easier analysis, filtering, or compression.
- **Key Transforms:**
    - **DFT/FFT:** General purpose, complex basis, efficient computation via FFT. Links convolution and multiplication.
    - **DCT:** Real, orthogonal, excellent energy compaction for correlated data (images). Basis of JPEG.
    - **Hadamard/Walsh:** Real, orthogonal, very fast (only additions/subtractions), square wave basis. Walsh ordered by sequency.
    - **Haar:** Real, orthogonal, fastest ($O(N)$), simplest wavelet, poor energy compaction.
    - **KLT/PCA:** Optimal energy compaction & decorrelation, data-dependent basis (eigenvectors), computationally intensive.
- **Unitary/Orthogonal:** Preserve energy, enable efficient inverse transforms ($A^{-1}=A^H$ or $A^{-1}=A^T$). Crucial for energy compaction.

---

## 3.3 Frequency Domain Filtering

### Concept

- **Goal:** Enhance an image or suppress noise by manipulating its frequency components in the DFT domain.
- **Mechanism:** Multiply each element (coefficient) of the image's Fourier transform $F(k, l)$ by a **weighting function** $H(k, l)$, called a **filter transfer function**. This allows accentuating desired frequencies and attenuating others.
  $$
  G(k, l) = F(k, l) \times H(k, l)
  $$
  Where $G(k,l)$ is the DFT of the filtered image. The filtered image $g(m,n)$ is obtained by taking the Inverse DFT of $G(k,l)$.
- **Terminology:** This process is called **Fourier filtering** or **frequency domain filtering**.
- **Spatial vs. Frequency View:**
    - **Spatial:** Describes adjacency relationships between pixels. Filtering is done by **convolution** with a spatial mask $h(m, n)$.
    - **Frequency:** Clusters data by frequency distribution (rate of change). Filtering is done by **multiplication** with a frequency domain filter $H(k, l)$.
    - **Relationship:** $H(k, l)$ is the DFT of $h(m, n)$, and $G(k,l) = F(k,l)H(k,l)$ corresponds to $g(m,n) = f(m,n) * h(m,n)$ (convolution).
    *[Insert Image: Spatial vs Frequency Filtering Formulas - From Page 61]*
- **Process:** Specify which frequencies to keep (pass) and which to discard (block) by designing $H(k, l)$. The image data is dissected into **spectral bands**, each representing a range of details.

### Low-Pass (LP) Filtering

- **Purpose:** Preserves **low frequencies** (slow changes, general shapes, overall illumination) and attenuates **high frequencies** (fast changes, fine details, edges, noise). Result is often **smoothing** or **blurring**.
- **Ideal Low-Pass Filter (ILPF):**
    - Sharply cuts off all frequencies above a certain **cut-off frequency** $D_0$.
    - Transfer function $H(u, v)$ (using continuous frequency variables $u, v$ for illustration):
      $$
      H(u, v) = \begin{cases} 1 & \text{if } D(u, v) \le D_0 \\ 0 & \text{if } D(u, v) > D_0 \end{cases}
      $$
      Where $D(u, v) = \sqrt{u^2 + v^2}$ is the distance from the frequency origin (DC component). For discrete DFT, $D(k, l) = \sqrt{k^2 + l^2}$.
      *[Insert Image: Ideal LP Filter Formula - From Page 62]*
      *[Insert Image: Ideal LP Filter Graph (1D cross-section) - From Page 62, left]*
    - **Cut-off Frequency ($D_0$):** Determines the amount of frequency components passed.
        - Smaller $D_0 \implies$ More high frequencies eliminated $\implies$ More blurring/smoothing.
        - Larger $D_0 \implies$ Fewer high frequencies eliminated $\implies$ Less blurring.
        - Chosen based on which components are desired (signal) vs. undesired (noise).
        *[Insert Image: Explanation of D0 - From Page 63]*
        *[Insert Image: Effect of D0 on smoothing illustration - From Page 64]*
- **Problem with ILPF: Ringing Effect**
    - The sharp cutoff of the ILPF in the frequency domain corresponds to a `sinc` function (`sin(x)/x`) in the spatial domain, which has oscillations (ripples).
    - Convolving the image with this `sinc`-like function produces **ringing artifacts** (overshoots and ripples) near sharp edges in the image.
    *[Insert Image: Ringing Effect Illustration (graphs and images) - From Page 65]*

#### Practical LP Filters (Smoother Cutoff)

- To reduce ringing, filters with smoother transitions between passband and stopband are used.
- Types:
    1.  **Ideal Low-Pass Filter (ILPF)** (already discussed, causes ringing)
    2.  **Butterworth Low-Pass Filter (BLPF)**
    3.  **Gaussian Low-Pass Filter (GLPF)**
    *[Insert Image: List of LP Filters - From Page 66]*

##### Butterworth Low-Pass Filter (BLPF)

- Provides a smooth transition from passband to stopband.
- Transfer Function:
  $$
  H(k, l) = \frac{1}{1 + \left[\frac{D(k, l)}{D_0}\right]^{2n}}
  $$
  Where:
    - $D(k, l) = \sqrt{k^2 + l^2}$ (distance from center in frequency domain)
    - $D_0$: Cut-off frequency (frequency at which H is $1/\sqrt{2}$ or 0.707, approx -3dB point, though definition here puts it at $H=0.5$ for large n).
    - $n$: **Order** of the filter. Controls the steepness of the transition.
        - Higher $n \implies$ Steeper transition, closer to Ideal LPF, more potential ringing.
        - Lower $n \implies$ Gradual transition, less ringing, but less sharp frequency selection.
  *[Insert Image: Butterworth LP Filter Formula - From Page 67]*
  *[Insert Image: Butterworth LP Filter 3D Plot and Frequency Response Curves (n=1, 4, 16 shown) - From Page 68]*
- **Advantage:** Significantly reduces ringing compared to ILPF, especially for lower orders ($n=1, 2$).
- **Spatial Representation:** The spatial domain representation of BLPFs shows that ringing increases as the filter order $n$ increases (becomes sharper in frequency).
  *[Insert Image: Spatial Representation of BLPFs (n=1, 2, 5, 20) - From Page 69]*
- **Comparison ILPF vs BLPF:**
  *[Insert Image: Comparison Images ILPF vs BLPF - From Page 70]*
  - Shows that BLPF (with n=2) produces smoother results with less ringing than ILPF for various cutoff frequencies $D_0$.

##### Gaussian Low-Pass Filter (GLPF)

- Uses a Gaussian function shape in the frequency domain.
- Transfer Function:
  $$
  H(u, v) = e^{-D(u, v)^2 / (2\sigma^2)}
  $$
  Often, the cutoff $D_0$ is defined such that $\sigma = D_0$ or related, leading to:
  $$
  H(u, v) = e^{-D(u, v)^2 / (2 D_0^2)}
  $$
  *[Insert Image: Gaussian LP Filter Formulas and Plots - From Page 71]*
- **Advantage:** Very smooth transition. The Fourier transform of a Gaussian is also a Gaussian. This means the spatial domain filter $h(m,n)$ is also Gaussian and has no ringing artifacts at all.
- **Disadvantage:** Transition is less sharp than Butterworth for comparable parameters.
- **Examples of Smoothing:**
    *[Insert Image: GLPF smoothing example (text) - From Page 72]* (Shows joining broken characters)
    *[Insert Image: GLPF smoothing example (portrait) - From Page 73]* (Shows reduction in fine skin lines)

### High-Pass (HP) Filtering

- **Purpose:** Preserves **high frequencies** (edges, details, noise) and attenuates **low frequencies** (slow variations, background). Often used for **sharpening** or **edge detection**.
- **Relationship to LP Filters:** An HP filter can be obtained by subtracting the corresponding LP filter from 1:
  $$
  H_{HP}(u, v) = 1 - H_{LP}(u, v)
  $$
  *[Insert Image: HP derivation from LP (formula and graph) - From Page 74]*
- **Ideal High-Pass Filter (IHPF):**
  $$
  H_{HP}(u, v) = \begin{cases} 0 & \text{if } D(u, v) \le D_0 \\ 1 & \text{if } D(u, v) > D_0 \end{cases}
  $$
  *[Insert Image: Ideal HP Filter Formula and 3D plot - From Page 75]*
- **Problem:** Like ILPF, IHPF suffers from **ringing artifacts**.

#### Practical HP Filters (Smoother Attenuation)

- Use smoother functions to attenuate low frequencies.
- Can be derived using $H_{HP} = 1 - H_{LP}$.

##### Butterworth High-Pass Filter (BHPF)

- Transfer Function:
  $$
  H_{BHPF}(u, v) = 1 - H_{BLPF}(u, v) = 1 - \frac{1}{1 + \left[\frac{D(u, v)}{D_0}\right]^{2n}} = \frac{\left[\frac{D(u, v)}{D_0}\right]^{2n}}{1 + \left[\frac{D(u, v)}{D_0}\right]^{2n}}
  $$
  Alternatively, sometimes defined directly swapping $D(u,v)$ and $D_0$:
  $$
  H(u, v) = \frac{1}{1 + \left[\frac{D_0}{D(u, v)}\right]^{2n}}
  $$
  *[Insert Image: Butterworth HP Filter Formula and Plots - From Page 76]*
- **Advantage:** Attenuates low frequencies smoothly, less ringing than IHPF.
- **Comparison IHPF vs BHPF:**
  *[Insert Image: Comparison Images IHPF vs BHPF - From Page 77]*
  - BHPF (n=2) results are much smoother than IHPF.

##### Gaussian High-Pass Filter (GHPF)

- Transfer Function:
  $$
  H_{GHPF}(u, v) = 1 - H_{GLPF}(u, v) = 1 - e^{-D(u, v)^2 / (2 D_0^2)}
  $$
  *[Insert Image: Gaussian HP Filter Formula and Plots (comparing GHPF and BHPF) - From Page 78]*
- **Advantage:** No ringing, very smooth attenuation of low frequencies.
- **Comparison BHPF vs GHPF:**
  *[Insert Image: Comparison Images BHPF vs GHPF - From Page 79]*
  - GHPF results are generally smoother than BHPF.

### Homomorphic Filtering

- **Purpose:** A specialized technique used to correct for **non-uniform illumination** or **shading effects** while simultaneously enhancing contrast or detail. Addresses situations where image intensity is a product of illumination and reflectance.
- **Goal:**
    - Enhance high frequencies (associated with reflectance/details).
    - Attenuate low frequencies (associated with slow-varying illumination) **but** preserve some fine detail that might fall into lower frequencies.
    *[Insert Image: Example Image with Uneven Illumination - From Page 80]*

#### Image Formation Model

- Assumes the image $f(x, y)$ is formed by the product of an **illumination component** $i(x, y)$ and a **reflectance component** $r(x, y)$:
  $$
  f(x, y) = i(x, y) \times r(x, y)
  $$
  *[Insert Image: Homomorphic Model - From Page 81]*
  - **Illumination $i(x, y)$:** Typically varies **slowly** across the image (spatially low frequency). Represents the amount of light falling on the scene.
  - **Reflectance $r(x, y)$:** Typically varies **faster** (spatially high frequency). Represents the properties of the objects in the scene (how much light they reflect), related to object details. Values are usually between 0 and 1.
- **Problem:** Since illumination and reflectance are multiplied, their frequency components are mixed together (via convolution in the frequency domain: $F(u,v) = I(u,v) * R(u,v)$). Standard filtering ($G = F \times H = (I * R) H$) makes it difficult to separate and process them independently.
  *[Insert Image: Frequency Mixing Problem - From Page 82]*

#### Homomorphic Filtering Approach

- **Idea:** Convert the multiplication into addition using the natural logarithm, then apply linear filtering.
- **Steps:**
    1.  **Take Natural Logarithm:**
        $$
        \ln(f(x, y)) = \ln(i(x, y)) + \ln(r(x, y))
        $$
        Let $z(x, y) = \ln(f(x, y))$, $i'(x,y) = \ln(i(x,y))$, $r'(x,y) = \ln(r(x,y))$. So $z = i' + r'$.
        *[Insert Image: Logarithm Step - From Page 83]*
        *[Insert Image: Step 1 Formula - From Page 84]*
    2.  **Apply Fourier Transform (FT):**
        Linearity of FT applies:
        $$
        Z(u, v) = \mathcal{F}\{z(x, y)\} = \mathcal{F}\{i'(x, y)\} + \mathcal{F}\{r'(x, y)\}
        $$
        $$
        Z(u, v) = I'(u, v) + R'(u, v)
        $$
        (Using notation $I'(u,v)$ for FT of $\ln(i)$ and $R'(u,v)$ for FT of $\ln(r)$).
        *[Insert Image: Step 2 Formula - From Page 84]*
        Now illumination (low freq) and reflectance (high freq) components are additive in the frequency domain of the log-transformed image.
    3.  **Apply Filter $H(u, v)$:**
        Multiply $Z(u, v)$ by a filter $H(u, v)$ designed to attenuate low frequencies (illumination) and enhance high frequencies (reflectance).
        $$
        S(u, v) = Z(u, v) \times H(u, v) = I'(u, v)H(u, v) + R'(u, v)H(u, v)
        $$
        *[Insert Image: Step 3 Formula - From Page 84]*
    4.  **Take Inverse Fourier Transform (IFT):**
        Transform back to the log-domain spatial representation.
        $$
        s(x, y) = \mathcal{F}^{-1}\{S(u, v)\} = \mathcal{F}^{-1}\{I'H\} + \mathcal{F}^{-1}\{R'H\}
        $$
        Let $s(x, y) = i''(x, y) + r''(x, y)$.
        *[Insert Image: Step 4 Formula - From Page 85]*
    5.  **Take Exponential:**
        Apply the exponential function to invert the initial logarithm step and get the final processed image $g(x, y)$.
        $$
        g(x, y) = \exp(s(x, y)) = \exp(i''(x, y) + r''(x, y)) = \exp(i''(x, y)) \times \exp(r''(x, y))
        $$
        Let $i_0(x, y) = \exp(i''(x, y))$ and $r_0(x, y) = \exp(r''(x, y))$.
        $$
        g(x, y) = i_0(x, y) \times r_0(x, y)
        $$
        The processed image still has illumination and reflectance components, but their relative contributions have been modified by the filter $H$.
        *[Insert Image: Step 5 Formula - From Page 85]*
        *[Insert Image: Block Diagram of Homomorphic Filtering - From Page 85]*

#### Homomorphic Filter Design ($H(u,v)$)

- Typically a **high-frequency emphasis** filter is used. It attenuates low frequencies and amplifies high frequencies, often with control over the amount of attenuation/amplification.
- Example Filter Profile:
  $$
  H(u, v) = (\gamma_H - \gamma_L) \left[ 1 - e^{-c (D(u, v)^2 / D_0^2)} \right] + \gamma_L
  $$
  *[Insert Image: High-Frequency Emphasis Filter Formula - From Page 86]*
  *[Insert Image: High-Frequency Emphasis Filter Profile Graph - From Page 86]*
  - $D(u, v)$: Distance from frequency origin.
  - $D_0$: Controls the transition point (often related to cutoff).
  - $c$: Controls the sharpness of the slope.
  - $\gamma_L$: Gain for low frequencies ($< 1$ to attenuate illumination).
  - $\gamma_H$: Gain for high frequencies ($> 1$ to enhance reflectance/details).
- **Interpretation:** The filter attenuates the contribution made by illumination ($\gamma_L < 1$) and amplifies the contribution made by reflectance ($\gamma_H > 1$).

#### Homomorphic Filtering Examples

- **Shelter Image:**
    *[Insert Image: Homomorphic Filtering Example (Shelter) - Original (a) and Processed (b) - From Page 87]*
    - Shows improved detail visibility inside the shelter after processing.
- **PET Scan Image:**
    *[Insert Image: Homomorphic Filtering Example (PET Scan) - Original (a) and Processed (b) with parameters - From Page 88]*
    - Parameters used: $\gamma_L = 0.25$, $\gamma_H = 2$, $c = 1$, $D_0 = 80$.
    - Shows enhanced contrast and visibility of features in the full body scan.

---

## Section Summary: Frequency Domain Filtering

- **Concept:** Modify image characteristics by multiplying the image's DFT with a filter transfer function $H(k,l)$.
- **LP Filters (ILPF, BLPF, GLPF):** Attenuate high frequencies -> Smoothing, Noise Reduction. Suffer from ringing (ILPF > BLPF > GLPF=none). $D_0$ controls cutoff.
- **HP Filters (IHPF, BHPF, GHPF):** Attenuate low frequencies -> Sharpening, Edge Enhancement. Suffer from ringing (IHPF > BHPF > GHPF=none). Derived as $1 - H_{LP}$.
- **Homomorphic Filtering:** Corrects non-uniform illumination by working in the log-domain. Uses high-frequency emphasis filter ($H$) to separate and adjust illumination (low freq) and reflectance (high freq) components. Steps: ln -> FT -> Filter H -> IFT -> exp.

---

## Glossary of New Terms

- **Image Transform:** A mathematical operation that changes the representation of an image from one domain (e.g., spatial) to another (e.g., frequency).
- **Spatial Domain:** Representation of an image by pixel values at specific (x, y) coordinates.
- **Frequency Domain:** Representation of an image based on the rate of change of pixel values (frequencies). Obtained via transforms like DFT.
- **Discrete Fourier Transform (DFT):** A specific transform converting a discrete sequence into its discrete frequency components (magnitude and phase).
- **Fast Fourier Transform (FFT):** An efficient algorithm to compute the DFT, typically $O(N \log N)$.
- **DFT Coefficient:** A complex value $X(k)$ representing the magnitude and phase of a specific frequency component $k$.
- **Magnitude Spectrum:** The magnitudes $|X(k)|$ of the DFT coefficients plotted against frequency $k$.
- **Phase Spectrum:** The phases $\angle X(k)$ of the DFT coefficients plotted against frequency $k$.
- **Inverse DFT (IDFT):** Transforms frequency domain coefficients back to the spatial/time domain sequence.
- **Periodicity (DFT Property):** Both the signal $x(n)$ and its DFT $X(k)$ are periodic with period N.
- **Linearity (DFT Property):** DFT of a sum is the sum of DFTs. DFT of a scaled signal is the scaled DFT.
- **Circular Convolution:** A type of convolution where indices wrap around (modulo N). Multiplication in DFT domain corresponds to circular convolution in time domain.
- **Twiddle Factor ($W_N$):** The complex exponential term $e^{-j 2 \pi / N}$ used in DFT/FFT computations.
- **Radix-2 FFT:** An FFT algorithm optimized for sequence lengths $N$ that are powers of 2.
- **Decimation in Time (DIT):** A specific FFT algorithm strategy that recursively breaks down the input time sequence.
- **Butterfly Diagram:** A graphical representation of the computations in an FFT algorithm.
- **Unitary Transform:** A transform whose matrix $A$ satisfies $A \times A^H = I$. Preserves signal energy.
- **Hermitian Transpose ($A^H$):** Conjugate transpose of a matrix $A$, $(A^*)^T$.
- **Orthogonal Transform:** A unitary transform whose matrix $A$ is real ($A \times A^T = I$).
- **Energy Compaction:** The property of a transform to concentrate most of the signal's energy into a small number of coefficients.
- **Basis Function/Vector:** The set of elementary functions/vectors that are linearly combined to represent the signal in the transformed domain.
- **Discrete Cosine Transform (DCT):** An orthogonal transform using real cosine basis functions, excellent for energy compaction of correlated signals (images).
- **Hadamard Transform:** An orthogonal transform using square wave basis functions (+1, -1), computationally simple. Matrix is symmetric.
- **Walsh Transform:** Similar to Hadamard but basis functions ordered by sequency (number of sign changes).
- **Sequency:** Generalized notion of frequency for non-sinusoidal waveforms, typically number of zero crossings.
- **Haar Transform:** Simplest wavelet transform, orthogonal, very fast ($O(N)$), piecewise constant basis, poor energy compaction.
- **Karhunen-Loève Transform (KLT) / Hotelling / PCA:** Optimal linear transform for energy compaction and decorrelation. Data-dependent basis functions (eigenvectors of covariance matrix).
- **Covariance Matrix:** Matrix describing the variance and correlation between elements of data vectors.
- **Eigenvalue / Eigenvector:** Special scalar/vector pair associated with a linear transformation (matrix), where applying the transformation scales the eigenvector by the eigenvalue. Used as basis in KLT.
- **Frequency Domain Filtering:** Modifying an image by multiplying its DFT coefficients by a filter transfer function $H(k,l)$.
- **Filter Transfer Function ($H(k,l)$):** The function defining the filter's effect in the frequency domain (multiplies the DFT).
- **Low-Pass Filter (LPF):** Filter that passes low frequencies and attenuates high frequencies (smoothing).
- **High-Pass Filter (HPF):** Filter that passes high frequencies and attenuates low frequencies (sharpening).
- **Cut-off Frequency ($D_0$):** The frequency defining the boundary between passband and stopband in a filter.
- **Ideal Filter (ILPF/IHPF):** Filter with an infinitely sharp cutoff. Causes ringing artifacts.
- **Butterworth Filter (BLPF/BHPF):** Filter with a smooth, monotonically decreasing transition, controlled by order $n$. Reduces ringing.
- **Gaussian Filter (GLPF/GHPF):** Filter with a Gaussian shape. Very smooth, no ringing.
- **Ringing Artifact:** Oscillations appearing near sharp edges in an image after filtering with a sharp-cutoff filter.
- **Homomorphic Filtering:** Technique to separate multiplicative components (illumination, reflectance) using logarithms, filter in the frequency domain, and then use exponentiation. Corrects non-uniform illumination.
- **Illumination Component ($i(x,y)$):** Slow-varying (low frequency) part of an image representing lighting.
- **Reflectance Component ($r(x,y)$):** Faster-varying (high frequency) part of an image representing object properties/details.

---

## Further Learning Resources

- **Digital Image Processing** by Gonzalez and Woods: A standard textbook covering these topics in detail.
- **Digital Signal Processing** by Oppenheim and Schafer: Covers DFT, FFT, and filtering concepts thoroughly.
- **Online Tutorials:** Search for "DFT tutorial", "FFT algorithm explained", "Image transforms comparison", "Frequency domain filtering", "Homomorphic filtering explanation". Websites like MathWorks (MATLAB), OpenCV documentation, and university course pages often have good materials.
- **Python Libraries:** Explore `numpy.fft` (for FFT), `scipy.fftpack` (includes DCT), `scikit-image` (filtering functions).

