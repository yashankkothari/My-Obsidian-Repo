# **Signal**

- **Definition**: A **signal** is a pattern of variation that carries information. It can be electrical, acoustic, mechanical, or any form of measurable variation that conveys data.
-
- **Mathematical Representation**:
    - A signal is expressed as a **function** of one or more independent variables.
    - Mathematically, a signal can be written as: x(t) where **x** represents the signal and **t** is the independent variable.

- **Examples**:
    - A **picture** is a signal where brightness is a function of two **spatial variables** (x, y).
    - A **sound wave** is a signal where air pressure varies with time.
    
- **Scope in This Course**:
    - Focus is on signals with a **single independent variable**, generally **time (t)**.
    - However, in some applications, t may represent another quantity (e.g., space, frequency).
    
- **Nature of a Signal**:
    - A signal can be **real-valued** or **scalar-valued**, meaning it consists of single numerical values for each tt.
    - Some signals can be complex-valued, but basic signals are often **real functions** of tt.

# **Classification of Signals**

Signals can be classified based on different criteria such as time representation, amplitude characteristics, and processing methods.

## **1. Continuous-Time and Discrete-Time Signals**  

### **(1) Continuous-Time Signal**  
- A **continuous-time signal** is defined for every instant of time.  
- It can take values at any real number **t**.  
- **Example:** Sinusoidal waves, electrical signals, speech signals.  
- **Mathematical Representation:**  
  $$
  x(t), \quad t \in \mathbb{R}
  $$

### **(2) Discrete-Time Signal**  
- A **discrete-time signal** is defined only at discrete time instances.  
- The signal exists only at integer values of **t**, usually indexed as **n**.  
- **Example:** Digital audio, sampled images, financial stock data.  
- **Mathematical Representation:**  
  $$
  x[n], \quad n \in \mathbb{Z}
  $$

---

## **2. Analog and Digital Signals (Time and Amplitude)**  

### **(3) Analog Signal**  
- **Definition:** A signal that has **both a continuous-time variable and a continuous amplitude**.  
- **Example:** Speech, television signals, temperature variations.  
- **Mathematical Representation:**  
  $$
  x(t), \quad t \in \mathbb{R}, \quad x(t) \in \mathbb{R}
  $$

### **(4) Digital Signal**  
- **Definition:** A signal that has **both discrete-time variables and discrete amplitude values**.  
- **Example:** Digital images, MP3 audio, binary communication signals.  
- **Mathematical Representation:**  
  $$
  x[n], \quad n \in \mathbb{Z}, \quad x[n] \in \{0,1,\dots,2^N-1\}
  $$  
- Digital signals are obtained through **quantization** of analog signals.  

---

## **3. Signal Processing**  

Signal processing involves the **representation, transformation, and manipulation** of signals to extract useful information.  

### **Development**  
- **1960s-1970s:** Signal processing evolved with advancements in **computers, semiconductors, and information science**.  
- Modern digital signal processing (DSP) techniques revolutionized fields such as communications, audio processing, and image processing.  

### **Key Signal Processing Operations**  
1. **Transformation & Filtering:** Fourier transform, Laplace transform, convolution.  
2. **Modulation & Coding:** Used in telecommunications (AM/FM, digital modulation).  
3. **Analog Signal Processing:** Uses circuits like filters and amplifiers.  
4. **Digital Signal Processing (DSP):** Algorithm-based processing using computers and microcontrollers.  

---

## **4. Processing of Analog Signals with Digital Methods**  

### **(1) Digitization of Analog Signals**  
- **Steps:**  
  1. **Sampling:** Converts a continuous signal into discrete-time values.  
  2. **Quantization:** Rounds sampled values to discrete levels.  
  3. **Coding:** Converts quantized values into binary representation.  

**Mathematical Representation:**  
$$
a(t) \rightarrow x(n)  \quad \text{(Analog → Digital)}
$$
![[Pasted image 20250228130902.png]]
### **(2) Digital Processing Method**  
- **A/D Conversion (Analog to Digital) → DSP Processing → D/A Conversion (Digital to Analog).**  
- **Filtering:** Applied to remove noise or enhance features.  

**Block Diagram:**  
$$
a(t) \rightarrow x(n) \rightarrow \text{DSP Processing} \rightarrow y(n) \rightarrow y_a(t)
$$
![[Pasted image 20250228130910.png]]
---

## **5. Features of Digital Signal Processing Systems**  

1. **High Accuracy:** Floating-point precision (8, 16, 32, 64-bit formats).  
2. **High Reliability:** Uses **VLSI (Very Large Scale Integration)** chips, unlike analog circuits which need calibration.  
3. **Flexibility:** Implemented using **DSP processors, software, FPGA, and VHDL**.  
4. **Easy Integration:** Can be combined with other digital systems.  
5. **Handles High-Dimensional Signals:** Efficient for images, videos, and multidimensional data.  
6. **Low Cost:** **Reusable and reconfigurable** systems reduce expenses.  
7. **Data Logging:** Can store and analyze past data.  
8. **Adaptive Capability:** Can modify processing dynamically based on conditions.  

# **Objective of Digital Signal Processing (DSP)**  

The main goal of **Digital Signal Processing (DSP)** is to manipulate digital signals to extract useful information, enhance signal quality, and enable efficient storage and transmission.

## **Key Objectives of DSP:**  
1. **Signal Enhancement:** Improve the quality of signals by removing noise and distortion.  
2. **Signal Compression:** Reduce data size for efficient storage and transmission.  
3. **Feature Extraction:** Identify key characteristics for classification and analysis.  
4. **Efficient Signal Representation:** Convert signals into digital form for easier processing.  
5. **Real-time Processing:** Perform operations quickly for applications like audio processing and radar systems.  

---

# **Digital Signals**  

## **Definition:**  
- A **digital signal** is a sequence of discrete values representing continuous information.  
- It is obtained by **sampling and quantizing** an analog signal.  
- **Mathematical Representation:**  
  $$
  x[n], \quad n \in \mathbb{Z}, \quad x[n] \in \{0,1,\dots,2^N-1\}
  $$  
- **Example Applications:**  
  - **Audio Signals:** MP3, VoIP.  
  - **Image Processing:** JPEG, PNG formats.  
  - **Communication Systems:** Digital TV, mobile networks.  

---

## **Digital Signal Manipulation - Digital Filters**  

## **Purpose of Digital Filters:**  
Digital filters are used to modify signals by **removing noise, extracting features, and enhancing signal clarity**.

### **Types of Digital Filters:**  
1. **Low-pass filter (LPF):** Allows low-frequency components and removes high-frequency noise.  
2. **High-pass filter (HPF):** Removes low-frequency noise while preserving high-frequency details.  
3. **Band-pass filter (BPF):** Passes a specific frequency range while rejecting others.  
4. **Notch filter:** Suppresses a narrow frequency band (e.g., removing 50Hz power line noise).  

### **Mathematical Representation:**  
**Finite Impulse Response (FIR) Filter:**  
$$
y(n) = \sum_{k=0}^{M} b_k x(n-k)
$$  
**Infinite Impulse Response (IIR) Filter:**  
$$
y(n) = \sum_{k=0}^{M} b_k x(n-k) - \sum_{j=1}^{N} a_j y(n-j)
$$  

---

## **Measurement of Digital Signals**  

## **(1) Spectrum Analysis**  
- Examines signal properties in the **frequency domain**.  
- **Fourier Transform (FT):** Converts time-domain signals to frequency-domain for analysis.  
- **Applications:** Speech processing, biomedical signals, radar analysis.

## **(2) Frequency Division**  
- Splitting signals into different frequency bands for multiplexing.  
- **Example:**  
  - **FDMA (Frequency Division Multiple Access):** Used in analog cellular systems.  
  - **OFDM (Orthogonal Frequency Division Multiplexing):** Used in Wi-Fi and 4G/5G.  

## **(3) Disturbance Attenuation**  
- **Objective:** Reduce the impact of **unwanted noise** in digital signals.  
- **Methods:**  
  - **Adaptive Filtering:** Adjusts filter properties based on signal conditions.  
  - **Noise Cancellation:** Used in hearing aids, telecommunication, and speech enhancement.  

---

## **Digital Signal Processing Workflow**  

### **(1) Selective A/D Conversion → Signal Representation (Sampling)**  
- **Process:**  
  1. **Sampling:** Converts a continuous signal into discrete values.  
  2. **Quantization:** Maps sampled values to finite levels.  
  3. **Coding:** Represents quantized values in binary format.  
- **Nyquist Theorem:**  
  $$
  f_s \geq 2 f_m
  $$  
  where \( f_s \) is the sampling rate and \( f_m \) is the highest frequency in the signal.

### **(2) Manipulation & Transform → Feature Extraction & Analysis**  
- **Techniques:**  
  - Fourier Transform → Frequency Analysis.  
  - Wavelet Transform → Time-Frequency Analysis.  
  - PCA → Dimensionality Reduction.  

### **(3) Noise Process → Digital Filtering**  
- **Noise Removal Methods:**  
  - **Low-pass filters** for high-frequency noise.  
  - **High-pass filters** for low-frequency noise.  
  - **Adaptive filtering** for real-time noise suppression.  


# **Discrete Signal and Discrete-Time Signal**  

## **Discrete Signal**  
- A **discrete signal** is a function of a **discrete independent variable**.  
- The independent variable is divided into **uniform intervals**, each represented by an integer.  
- The letter **"n"** is used to denote the independent variable.  
- A **discrete or digital signal** is represented as **x(n)**.

### **Example of a Discrete Signal:**  
Given:  
$$
x(n) = \{2, 4, -1, 3, 3, 4\}
$$  
For **\( n = 0, 1, 2, 3, 4, 5 \)**:  
- \( x(0) = 2 \)  
- \( x(1) = 4 \)  
- \( x(2) = -1 \)  
- \( x(3) = 3 \)  
- \( x(4) = 3 \)  
- \( x(5) = 4 \)  

---

## **Discrete-Time Signal**  
- When the independent variable represents **time \( t \)**, the signal is called a **discrete-time signal**.  
- The time variable **\( t \)** is divided into uniform intervals using:  
  $$
  t = nT
  $$  
  where **\( T \)** is the **sampling time period**.  
- The sampling time period **\( T \)** is the **inverse** of the sampling frequency **\( f_s \)**:  
  $$
  T = \frac{1}{f_s}
  $$  
- A discrete-time signal is denoted as **x(n)** or **x(nT)**.

### **Key Points:**  
- **Discrete-Time Signal:** A signal defined only at discrete time instances \( nT \).  
- **Uniform Sampling:** The time intervals remain constant.  
- **Applications:** Digital audio, video processing, speech signals.  

---

# **Digital Signal and Quantization**  

## **Digital Signal vs. Discrete Signal**  
- A **digital signal** is similar to a **discrete signal**, except that its **magnitude is quantized**.  
- **Quantization** means the signal's amplitude can only take **finite discrete values** from a predefined set.  
- **Quantization is necessary** for representing signals in **binary codes** for digital processing.  

---

## **Quantization and Digital Signal Representation**  
### **Example Data Points:**  
The values of **\( x(t) \)** at specific time instances:  

![[Pasted image 20250228131858.png]]

| **Time \( t \)** | **\( x(t) \)** |
|--------------|------------|
| \( t = 0 \)  | \( x(t) = 0 \)  |
| \( t = 1T \) | \( x(t) = 0.1 \) |
| \( t = 2T \) | \( x(t) = 0.3 \) |
| \( t = 3T \) | \( x(t) = 0.35 \) |
| \( t = 4T \) | \( x(t) = 0.55 \) |
| \( t = 5T \) | \( x(t) = 0.8 \) |
| \( t = 6T \) | \( x(t) = 0.8 \) |
| \( t = 7T \) | \( x(t) = 0.9 \) |

The corresponding **digital signal representation** in quantized form:  
$$
x(n) = \{0, 0.1, 0.3, 0.35, 0.55, 0.8, 0.8, 0.9\}
$$  
where **\( n = 0, 1, 2, 3, 4, 5, 6, 7 \)**.  

![[Pasted image 20250228131927.png]]
---

## **Key Points:**  
- **Discrete Signal:** Has discrete time values but continuous amplitude.  
- **Digital Signal:** Has both discrete time and discrete (quantized) amplitude.  
- **Quantization:** Converts continuous amplitude into a **finite set of levels** for digital processing.  
- **Binary Representation:** Quantized values are stored in **binary format** for digital computation.  

# **Representation of Discrete-Time Signals**  

Discrete-time signals can be represented in multiple ways for analysis and processing. The primary methods include **functional, graphical, tabular, and sequence representations**.

---

## **Functional Representation**  
- A **mathematical function** defines the discrete-time signal.  
- The signal is represented as a function of discrete-time index **\( n \)**.  
- Example:  
  ![[Pasted image 20250228132150.png]]

---

## **Graphical Representation**  
- The signal is plotted as a **stem plot**, with discrete values marked on a graph.  
- The x-axis represents **time index \( n \)**, and the y-axis represents the **signal amplitude \( x(n) \)**.  
- Example Plot:  

![[Pasted image 20250228132235.png]]


---

## **Tabular Representation**  
- The signal values are arranged in a table for clarity.  
![[Pasted image 20250228132917.png]]

---

## **Sequence Representation**  
- The signal is written as a **sequence of values**.  
- Example:  

![[Pasted image 20250228132937.png]]

## **Key Points:**  
- **Functional Representation:** Uses mathematical equations or direct notation.  
- **Graphical Representation:** Visualizes discrete-time signals using stem plots.  
- **Tabular Representation:** Organizes values in a structured format.  
- **Sequence Representation:** Expresses signals as ordered lists.  

This **markdown format is structured for Obsidian** with equations, tables, and clear explanations. 🚀 Let me know if you need more details!  

# **Standard Discrete-Time Signals**  

Standard discrete-time signals are fundamental signals that form the basis of signal processing and system analysis.

---

## **Digital Impulse Signal (Unit Sample Sequence)  
- The **unit impulse signal** (Kronecker delta function) is defined as:  
  $$
  \delta(n) =
  \begin{cases} 
  1, & \text{if } n = 0 \\
  0, & \text{otherwise}
  \end{cases}
  $$
![[Pasted image 20250228133926.png]]

- **Key Properties:**  
  - Used to determine **impulse response** of a system.  
  - Acts as an identity for **convolution**.  

---

## **Unit Step Signal - u(n)**  
- The **unit step signal** is defined as:  
  $$
  u(n) =
  \begin{cases} 
  1, & \text{if } n \geq 0 \\
  0, & \text{if } n < 0
  \end{cases}
  $$
![[Pasted image 20250228133935.png]]

- **Key Properties:**  
  - Used in system analysis to represent **causal systems**.  
  - Acts as a **cumulative sum** of the impulse function.  

---

## **Ramp Signal - r(n)**  
- The **ramp signal** is defined as:  
  $$
  r(n) =
  \begin{cases} 
  n, & \text{if } n \geq 0 \\
  0, & \text{if } n < 0
  \end{cases}
  $$
![[Pasted image 20250228133951.png]]

- **Key Properties:**  
  - Represents **linearly increasing** discrete-time signals.  
  - Can be obtained by summing the **unit step function**.  

---

## **Exponential Signal - g(n)**  
- The **discrete-time exponential signal** is defined as:  
  $$
  g(n) = 
  \begin{cases} 
  a^n, & \text{if } n \geq 0 \\
  0, & \text{if } n < 0
  \end{cases}
  $$

![[Pasted image 20250228134004.png]]

- **Key Properties:**  
  - If \( n < 1 \), the signal decays over time.  
  - If \( n > 1 \), the signal grows exponentially.  

---

## **Discrete-Time Sinusoidal Signal**  
- The **sinusoidal signal** is given by:  

 ![[Pasted image 20250228134031.png]]
- **Key Properties:**  
  - Periodic if (omega/2pi) is a rational number.  
  - Represents oscillatory signals in **discrete-time systems**.  

![[Pasted image 20250228134130.png]]
---

## **Discrete-Time Complex Exponential Signal**  
- The **complex exponential signal** is given by:  
![[Pasted image 20250228134153.png]]
- **Key Properties:**  
  - Used in **Fourier analysis** and **signal decomposition**.  
  - The magnitude remains **constant** (unit circle in complex plane).  
![[Pasted image 20250228134205.png]]
![[Pasted image 20250228134213.png]]

# **Sampling Theorem**  

## **Definition**  
- A **continuous-time signal** can be represented by its **samples** and can be **recovered** if the **sampling frequency** $f_s$ is at least **twice** the **highest frequency component** $f_m$ of the message signal.  
- Mathematically: $f_s \geq 2 f_m$  

## **Relationship Between Analog and Digital Signal by Sampling**  
- The **time interval** between successive samples is called **sampling time**.  
- The **inverse** of the sampling period is called **sampling frequency** $f_s$ (or sampling rate).  
- Let:  
  - $x_a(t)$ = Analog / Continuous-time signal.  
  - $x(n)$ = Discrete-time signal obtained by sampling $x_a(t)$.  
- The relationship is expressed as: $x(n) = x_a(nT)$  
  where:
  - $T$ = Sampling period (in seconds).  
  - $f_s = \frac{1}{T}$ = Sampling frequency (in Hz).  
  
![[Pasted image 20250301190414.png]]


---

# **Classification of Discrete Time Signals**  

## **Deterministic and Nondeterministic Signals**  
- **Deterministic Signals**: Can be **completely described** by a **mathematical equation**. Examples: **Ramp, Unit Step, Exponential, Sinusoidal Signals**.  
- **Nondeterministic (Random) Signals**: Have **random characteristics**, not predictable. Example: **Noise**.  

## **Periodic and Aperiodic Signals**  
- **Periodic Signal**: A discrete-time signal $x(n)$ is **periodic** if it satisfies: $x(n + N) = x(n)$ for an integer $N$.  
  - $N$ is the **fundamental period** (smallest value of $N$ for which the equation holds).  
  - **Periodic signals** are **power signals**.  
  - Examples: **Discrete-time sinusoidal and complex exponential signals (if their fundamental frequency is a rational number)**.  
  
![[Pasted image 20250301190516.png]]
- **Aperiodic (Nonperiodic) Signal**: If no value of $N$ satisfies the periodicity condition, the signal is **aperiodic**.  

## **Symmetric and Antisymmetric Signals**  
- **Even (Symmetric) Signals**: A signal is **even** if it satisfies: $$x(-n) = x(n)$$
- **Odd (Antisymmetric) Signals**: A signal is **odd** if it satisfies: $$x(-n) = -x(n)$$
![[Pasted image 20250301190654.png]]
![[Pasted image 20250301190721.png]]

### Numerical Example

![[Pasted image 20250301190744.png]]
![[Pasted image 20250301190804.png]]


## **Energy and Power Signals**  
- **Energy Signal**: A discrete-time signal $x(n)$ is an **energy signal** if it has **finite energy** and is **nonzero**:  
  $$E = \sum_{n=-\infty}^{\infty} |x(n)|^2 < \infty$$  
- The **Exponential Signals** are examples of energy signals

- **Power Signal**: A signal is a **power signal** if its **average power** is **finite** and **nonzero**:  
  $$P = \lim_{N \to \infty} \frac{1}{2N+1} \sum_{n=-N}^{N} |x(n)|^2$$  
- A **signal cannot be both an energy and a power signal**.  

![[Pasted image 20250301190940.png]]

### Numerical Example

![[Pasted image 20250301191022.png]]
![[Pasted image 20250301191027.png]]
![[Pasted image 20250301191037.png]]



## **Causal and Noncausal Signals**  
- **Causal Signal**: A signal is **causal** if it is **zero** for **all negative values** of $n$: $$x(n) = 0,for \: n < 0$$
- **Noncausal Signal**: A signal is **noncausal** if it is **defined for** $n \leq 0$ **or for both** $n > 0$ **and** $n \leq 0$.  
- **if system is non causal** then $$x(n) \neq 0,for \: n < 0$$
  - A **noncausal signal** can be **converted into a causal signal** by **multiplying it with a unit step signal**.  
  
- **Anticausal Signal**: A signal is **anticausal** if it is **defined only for** $n < 0$.  

![[Pasted image 20250301191354.png]]