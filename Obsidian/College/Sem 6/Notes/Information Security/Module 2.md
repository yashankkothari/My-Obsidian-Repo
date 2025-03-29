### **Buffer Overflows**
- Occur when **data is written beyond allocated space**, e.g., writing a **10th byte** in a **9-byte array**.
- In **exploitable buffer overflows**, attacker inputs overwrite **executable memory**, leading to potential code execution.
- Attackers look for **buffer overflow vulnerabilities** that allow them to **execute arbitrary code**.


#### **Example of Buffer Overflow**
```c
char sample[10];
int i;
for (i=0; i<=9; i++)
    sample[i] = 'A';
sample[10] = 'B';  // Buffer Overflow: Writing outside allocated memory

```

## **Harm from Buffer Overflows**
### **Overwrite Possibilities**
- **Program Data**: Alters another variable’s value.
- **Program Instructions**: Modifies execution flow.
- **Other Programs' Data/Code**: Affects unrelated processes.
- **Operating System Data/Code**: Can lead to system-wide compromise.

### **Security Impact**
- **Privilege Escalation**: Overwriting instructions can grant attackers execution privileges of:
  - **The program** (if it modifies program instructions).
  - **The operating system** (if it modifies OS instructions).
- **Denial of Service (DoS)**:
  - Random input may **crash** the program, preventing service availability.
  - Sophisticated attacks can **modify return values** to execute attacker-controlled code.

---
## **Where a Buffer Can Overflow**
- The impact of a **buffer overflow** depends on **where the buffer is located** in memory.
- Example: **"AAAAAAAAAAB"** overwriting adjacent memory.

### **Possible Overwrite Targets**
1. **Stack**:  
   - Can overwrite **function return addresses**, altering control flow.
2. **Heap**:  
   - Can corrupt **adjacent memory allocations**, leading to unpredictable behavior.
3. **Global Data**:  
   - Can modify **static variables**, affecting program state.
4. **Code Segments**:  
   - Overwriting executable code can **inject malicious instructions**.

![[Pasted image 20250303232432.png]]

## **The Stack after Procedure Calls**

![[Pasted image 20250303232545.png]]

- When **Procedure A calls Procedure B**, the **stack** stores:
  - Procedure B's **local variables**.
  - A **return address** pointing back to Procedure A.

- When **Procedure B finishes execution**:
  - Its **stack frame is removed** (popped off the stack).
  - The program **returns to Procedure A**, continuing execution **from where it left off**.

#### **Stack Execution Flow**
1. **Procedure A calls Procedure B** → **B's frame is pushed onto the stack**.
2. **Procedure B executes and completes** → **B's frame is popped**.
3. **Control returns to Procedure A**, resuming execution.

This structured stack behavior is essential for function execution and is a key target for **buffer overflow attacks**.


## **Common Causes of Buffer Overflows**
- **Improper Memory Handling**: Occurs in **C and C++** due to lack of memory safety.
- **Lack of Bounds Checking**: Writing beyond allocated space.
- **Unsafe String Functions**: Functions without size enforcement:
  - `gets(buffer)` – Reads input **without size restrictions**.
  - `strcpy(dest, src)` – **No destination size check**.
  - `strcat(dest, src)` – **No space verification** before concatenation.
  - `sprintf(dest, format, args...)` – **No bounds check** for formatted output.
  - `scanf("%s", buffer)` – **Reads input without length validation**.
- **Stack-Based Overflow**: Writing past a function’s local variable space can **overwrite the return address**.

---

## **Buffer Overflow Defenses**
### **Compile-Time Defenses**
- Prevent vulnerabilities **before** program execution.
- Used for **new programs** to mitigate buffer overflows.

### **Run-Time Defenses**
- Detect and stop attacks in **existing** programs.
- Applied via **OS updates and security patches**.
- Essential due to the **large number of vulnerable programs**.

## **Memory Organization**
### **Memory Layout**
- **System Data & Code**: Resides at **high addresses**.
- **Program Code & Local Data**: Resides at **low addresses**.
- **Stack**: Grows **downward**, used for function calls and local variables.
- **Heap**: Grows **upward**, used for dynamic memory allocation.

![[Pasted image 20250303232329.png]]
### **Importance of Memory Context**
- Helps understand **attack impact**:
  - **Inside the program**: Affects only that program.
  - **Outside the program**: Can compromise the **entire system**.

### **Compromised Stack**

![[Pasted image 20250303232710.png]]

- Normally, the **program counter (PC)** returns to the **calling procedure** after a function call.
- In a **buffer overflow attack**, the return address is **overwritten**, causing:
  - The **PC to point to malicious code** instead of returning correctly.
  - Execution of **attacker-controlled instructions** instead of the intended program flow.

#### **Impact of a Compromised Stack**
- **Hijacks program execution**, allowing arbitrary code execution.
- **Escalates privileges** if the compromised program has higher access rights.
- **Leads to system compromise**, enabling further exploits.

This is a common attack vector used in **stack-based buffer overflow attacks**.

### **Overwriting Memory for Execution**
- **Modify the program counter** stored in the stack.
- **Overwrite low memory code**, replacing it with malicious instructions.
- **Redirect execution** by pointing the program counter to attacker-controlled stack data.

### **Memory Organization**
- **Text Segment** → Stores program code (executable instructions).
- **Data Segment** → Holds static/global variables.
- **Heap** → Used for dynamic memory allocation.
- **Stack** → Temporary storage for:
  - **Local variables**
  - **Function parameters**
  - **Return addresses**

![[Pasted image 20250303232813.png]]

### **Smashing the Stack**
- **What happens if a buffer overflows?**
  - Overflows into adjacent memory.
  - Can overwrite critical values like return addresses.

- **Consequences:**
  - **Stack Pointer (SP) moves incorrectly.**
  - **Return address is corrupted**, causing the program to jump to the wrong location.
  - **Program crashes** or exhibits unintended behavior.
![[Pasted image 20250303232946.png]]

- **Buffer Overflow Attack:**
  - Instead of just crashing the program, Trudy **injects malicious code** into the stack.
  - She **overwrites the return address** to point to her injected code.

- **Impact:**
  - Trudy **gains control** of the program execution.
  - She can **run arbitrary code** with the program’s privileges.
  - This can lead to **privilege escalation**, system compromise, or further exploits.

![[Pasted image 20250303233021.png]]

### **Trudy's Challenges and Solutions**
#### **Challenges:**
- **Unknown Address:** Trudy may not know:
  - The exact **address of her injected code**.
  - The **location of the return address** on the stack.

#### **Solutions:**
- **NOP Sled (Landing Pad):**  
  - Precede the **malicious code** with a sequence of **NOP (No Operation) instructions**.  
  - This increases the chance that execution "slides" into the injected code.

- **Return-Oriented Programming (ROP):**  
  - Insert **multiple return addresses** to increase the chances of hijacking execution.
  - Chain small code snippets (gadgets) to **bypass security measures**.

![[Pasted image 20250303233055.png]]

### **Harm from Buffer Overflows**
- **Overwrite:**
  - Another piece of the program’s **data**.
  - An **instruction** in the program.
  - **Data or code** belonging to another program.
  - **Data or code** belonging to the operating system.

- **Security Impact:**
  - **Overwriting program instructions** gives attackers **execution privileges** of that program.
  - **Overwriting OS instructions** grants attackers **OS-level execution privileges**.

---

### **Stack Buffer Overflow - Denial of Service (DOS)**
- Supplying **random input** can **crash** a program.
- When a program **crashes**, it can no longer provide its intended function, leading to a **denial-of-service attack**.
- **More dangerous attacks** involve controlling program execution:
  - The attacker injects a **target address** into the buffer overflow.
  - This address **overwrites the saved return address** in the stack.
  - When the function returns, it **jumps to the attacker's code** instead of the correct function.

---
### **Stack Buffer Overflows**

- **Common Practice in C Programs:**
  - Buffers are often defined with **fixed sizes**.
  - The **standard C IO library** defines `BUFSIZ` as the default size for input buffers.
  
- **Problem with Buffer Merging:**
  - When **merging data** from one buffer to another, space **may be exceeded**.
  - If the new data **overflows**, it may **corrupt adjacent memory**.

---

### **Example: Stack Buffer Overflow**
```c
void getinp(char *inp, int siz) {
    puts("Input value: ");
    fgets(inp, siz, stdin);
    printf("buffer3 getinp read %s\n", inp);
}

void display(char *val) {
    char tmp[16];
    sprintf(tmp, "read val: %s\n", val);
    puts(tmp);
}

int main(int argc, char *argv[]) {
    char buf[16];
    getinp(buf, sizeof(buf));
    display(buf);
    printf("buffer3 done\n");
}
```
### **Understanding the Vulnerability**

#### **First Run (Safe Input)**

```shell
$ ./buffer3
Input value:
SAFE
buffer3 getinp read SAFE
read val: SAFE
buffer3 done
```

- **Input size fits within the buffer.**
- **No corruption occurs.**

#### **Second Run (Overflow Attempt)**

```shell
$ ./buffer3
Input value:
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
buffer3 getinp read XXXXXXXXXXXXXXX
read val: XXXXXXXXXXXXXXX
buffer3 done
Segmentation fault (core dumped)
```

- **Input exceeds buffer size.**
- **Only 15 characters were read** (due to `fgets`), preventing immediate overwriting of the **return address**.
- However, **merging this input with another string caused an overflow**.
- The **stack frame got corrupted**, leading to a **crash**.

---

#### **Key Takeaways**

- **Buffer overflows occur** when input **exceeds available space**.
- **If the return address is overwritten, execution can be hijacked.**
- **Proper bounds checking and safer input handling** (e.g., using `snprintf` instead of `sprintf`) can help prevent attacks.


### **Unsafe C Standard Library Routines**
- **Buffer overflows** can occur wherever externally sourced data are **copied or merged**.
- **Not limited to program code**—they can occur in **standard libraries** or **third-party libraries**.
- **Attackers and defenders** must consider **all possible locations** of buffer overflows.

#### **Common Unsafe C Library Functions**
| Function | Description |
|----------|------------|
| `gets(char *str)` | Reads a line from standard input into `str` (unsafe due to no bounds checking). |
| `sprintf(char *str, char *format, ...)` | Creates `str` according to supplied format and variables. |
| `strcat(char *dest, char *src)` | Appends contents of `src` to `dest`, possibly overflowing `dest`. |
| `strcpy(char *dest, char *src)` | Copies contents of `src` to `dest` without checking bounds. |
| `vsprintf(char *str, char *fmt, va_list ap)` | Similar to `sprintf`, but uses a `va_list` for arguments. |

---

### **Shellcode**
- **Code supplied by an attacker**, often placed inside the **overflowed buffer**.
- **Traditionally used to execute a shell** (command-line interpreter).

#### **Characteristics**
- **Machine code**: Specific to the **processor** and **operating system**.
- **Position-independent**: Cannot contain absolute addresses, as **attackers don't know exact memory locations**.
- **Required assembly language skills** (though modern tools automate exploit creation).

#### **Metasploit Project**
- A framework providing **tools for penetration testing and exploit research**.

---

### **Example: Shellcode Execution in C**
```c
int main(int argc, char *argv[]) {
    char *sh;
    char *args[2];
    sh = "/bin/sh";
    args[0] = sh;
    args[1] = NULL;
    execve(sh, args, NULL);
}
````

- **Executes a shell (`/bin/sh`) when run**.

---

### **Equivalent Position-Independent x86 Assembly Code**

```assembly
nop
nop       // end of nop sled
jmp find  // jump to end of code

cont:
    pop %esi       // pop address of sh off stack into %esi
    xor %eax, %eax // zero contents of EAX
    mov %al, 0x7(%esi)  // copy zero byte to end of string sh (%esi)
    lea (%esi), %ebx    // load address of sh (%esi) into %ebx
    mov %ebx, 0x8(%esi) // save address of sh in args[0] (%esi+8)
    mov %eax, 0xc(%esi) // copy zero to args[1] (%esi+c)
    mov $0xb, %al       // copy execve syscall number (11) to AL
    mov %esi, %ebx      // copy address of sh (%esi) to %ebx
    lea 0x8(%esi), %ecx // copy address of args (%esi+8) to %ecx
    lea 0xc(%esi), %edx // copy address of args[1] (%esi+c) to %edx
    int $0x80           // software interrupt to execute syscall

find:
    call cont  // call cont which saves next address on stack

sh: 
    .string "/bin/sh "  // string constant
args:
    .long 0  // space used for args array
    .long 0  // args[1] and also NULL for env array
```

---

### **Hexadecimal Representation of Compiled x86 Shellcode**

```hex
90 90 eb 1a 5e 31 c0 88 46 07 8d 1e 89 5e 08 89
46 0c b0 0b 89 f3 8d 4e 08 8d 56 0c cd 80 e8 e1
ff ff ff 2f 62 69 6e 2f 73 68 20 20 20 20 20 20
```

---

### **Shellcode Restrictions**

- **Must be position-independent** (no absolute memory addresses).
- **Specific to processor architecture** and **operating system**.
- **Targets specific software and OS versions**.
- **Traditionally required assembly knowledge**, but modern tools automate exploit creation.

### **Stack Overflow Variants**
#### **Target Programs**
- **Trusted system utilities**  
- **Network service daemons**  
- **Commonly used library code**  

#### **Shellcode Functions**
- **Launch a remote shell** when connected to the target.  
- **Create a reverse shell** that connects back to the attacker.  
- **Use local exploits** to establish a shell.  
- **Flush firewall rules** that block other attacks.  
- **Break out of a chroot jail**, gaining full system access.  

#### **Network-Based Attacks**
- **Network daemons** listen for connections and spawn **child processes**.  
- If a **child process** uses unsafe buffer handling, it can be **exploited**.  
- Example: **Morris Worm (1988)** exploited `gets()` in the **fingerd** daemon.  

#### **File-Based Attacks**
- **Target document processing libraries** (e.g., GIF/JPEG decoders).  
- Attackers inject malicious data into **files** instead of direct inputs.  
- Example: A **corrupted image file** can trigger a buffer overflow.  
- Attack files can be **spread via email, web pages, or messaging apps**.  
- **Typical goal**: Open a **network connection** back to the attacker.  

---

### **30 Cybersecurity Search Tools**
| #  | Tool | Purpose |
|----|------|---------|
| 1  | **Dehashed** | View leaked credentials. |
| 2  | **SecurityTrails** | Extensive DNS data. |
| 3  | **DorkSearch** | Fast Google dorking. |
| 4  | **ExploitDB** | Archive of various exploits. |
| 5  | **ZoomEye** | Gather information about targets. |
| 6  | **Pulsedive** | Search for threat intelligence. |
| 7  | **GrayHatWarfare** | Search public S3 buckets. |
| 8  | **PolySwarm** | Scan files and URLs for threats. |
| 9  | **Fofa** | Search for various threat intelligence. |
| 10 | **LeakIX** | Search publicly indexed information. |
| 11 | **DNSDumpster** | Search for DNS records quickly. |
| 12 | **FullHunt** | Search and discover attack surfaces. |
| 13 | **AlienVault** | Extensive threat intelligence feed. |
| 14 | **ONYPHE** | Collect cyber-threat intelligence data. |
| 15 | **Grep App** | Search across a half-million git repos. |
| 16 | **URL Scan** | Free service to scan and analyze websites. |
| 17 | **Vulners** | Search vulnerabilities in a large database. |
| 18 | **WayBackMachine** | View content from deleted websites. |
| 19 | **Shodan** | Search for internet-connected devices. |
| 20 | **Netlas** | Search and monitor internet-connected assets. |
| 21 | **CRT.sh** | Search for certificates logged by CT. |
| 22 | **Wigle** | Database of wireless networks with statistics. |
| 23 | **PublicWWW** | Marketing and affiliate research. |
| 24 | **Binary Edge** | Scans the internet for threat intelligence. |
| 25 | **GreyNoise** | Search for internet-connected devices. |
| 26 | **Hunter** | Search for email addresses of a website. |
| 27 | **Censys** | Assess attack surfaces for connected devices. |
| 28 | **IntelligenceX** | Search Tor, I2P, leaks, domains, emails. |
| 29 | **Packet Storm Security** | Browse latest vulnerabilities/exploits. |
| 30 | **SearchCode** | Search 75B lines of code from 40M projects. |
### **Buffer Overflow Defenses**
#### **Two Broad Defense Approaches**
1. **Compile-Time Defenses** – Harden new programs to resist attacks.  
2. **Run-Time Defenses** – Detect and abort attacks in existing programs.  

- **Compile-Time Defenses** prevent or detect buffer overflows at the time of compilation.  
- **Run-Time Defenses** are crucial due to the large base of vulnerable software, allowing protection via OS updates.  

---

### **Compile-Time Defenses**
#### **1. Programming Language Approach**
- Use a **modern high-level language** to prevent buffer overflow attacks.  
- The compiler enforces **range checks** and **permissible operations** on variables.  

##### **Disadvantages**  
- **Additional execution overhead** due to run-time checks.  
- **Higher resource usage** for flexibility and safety.  
- **Limited low-level access**, making it unsuitable for writing device drivers.  

#### **2. Safe Coding Techniques**
- **C prioritizes** space efficiency and performance **over type safety**.  
- Assumes **programmers will write safe code**, leading to vulnerabilities.  
- Requires **manual code inspection and rewriting** of unsafe code.  
- Example: **OpenBSD project**  
  - Audited OS, standard libraries, and utilities.  
  - Resulted in **one of the safest** operating systems in widespread use.  

### **Compile-Time Defenses**
#### **1. Language Extensions & Safe Libraries**
- **Dynamically allocated memory** is problematic since size info is unavailable at compile time.  
- Requires **library extensions** and recompilation of programs.  
- Issues with **third-party applications** due to compatibility.  
- Unsafe **C standard library functions** are replaced with safer versions (e.g., **Libsafe**).  
  - Implemented as a **dynamic library** that loads before standard libraries.  

#### **2. Stack Protection**
- **Adds function entry/exit code** to check for stack corruption.  
- **Random Canary Values:**  
  - Must be **unpredictable** and **different across systems**.  
- **Stackshield & Return Address Defender (RAD):**  
  - **GCC extensions** adding entry/exit code.  
  - Function **entry saves return address** in a safe memory region.  
  - Function **exit verifies return address**; aborts program if altered.  

---

### **Run-Time Defenses**
#### **1. Executable Address Space Protection**
- Uses **virtual memory support** to make memory regions **non-executable**.  
- Requires **Memory Management Unit (MMU) support**.  
- Common in **SPARC/Solaris**, newer in **x86 Linux/Unix/Windows**.  
##### **Issues**  
- **Executable stack support** requires special provisions.  

#### **2. Address Space Randomization**
- **Randomizes key memory locations**:  
  - **Stack, heap, global data** (random shift per process).  
  - **Heap buffers** and **standard library function locations** randomized.  
- **Large address ranges** reduce performance impact.  

#### **3. Guard Pages**
- **Placed between critical memory regions**, flagged as **illegal** in MMU.  
- **Access attempts trigger process abort**.  
- **Extended approach:** Guard pages **between stack frames and heap buffers**.  
  - **Increased execution time** due to high page mapping overhead.  

---

### **Input Size & Buffer Overflow**
- **Programmers assume maximum input size**, leading to unconfirmed buffer sizes.  
- **Buffer overflow occurs when input exceeds allocated space**.  
- **Testing limitations:**  
  - Test cases **often fail to include large enough inputs**.  
  - Safe coding treats **all input as potentially dangerous**.  

### **Interpretation of Program Input**
- Input can be **binary or text**, requiring correct **encoding interpretation**.  
- **Multiple character sets** increase complexity.  
- **Failure to validate input** may lead to vulnerabilities.  
- **Example: Heartbleed OpenSSL Bug (2014)**  
  - Exploited a failure to **validate binary input values**, exposing sensitive data.  

### **Stack Smashing Prevention**
#### **1. Non-Executable Stack (Preferred)**
- **Use NX (No-Execute) bit** (if supported by hardware).  
- **Prevents execution of injected shellcode** in the stack.  
- **Limitations:** Some programs **execute code on the stack** (e.g., Java).  

#### **2. Use Safe Programming Languages**
- **Languages like Java, C#** prevent buffer overflows.  
- **Compiler enforces** memory safety.  

#### **3. Use Safer C Functions**
- Replace **unsafe functions** with safer alternatives:  
  - **`strncpy` instead of `strcpy`**  
  - **`snprintf` instead of `sprintf`**  
- Helps **reduce risk**, though not a complete solution.  

### **Stack Smashing Prevention: Canary**
- **Canary-based protection** adds a random value before return addresses on the stack.  
- **Types of Canary Values:**
  - **Fixed constant** (e.g., `0x000aff0d`).  
  - **Randomized per execution** (more secure).  
- **Run-time stack check**: Canary is checked before function return.  
- **If modified, program aborts** (prevents buffer overflow exploits).  

### **Microsoft's Canary Protection (`/GS` Flag)**
- **Microsoft C++ compiler** includes buffer security check using `/GS` flag.  
- **Canary (Security Cookie)** placed on stack to detect overwrites.  
- **Issue:** If the canary is detected as modified, the program checks a **user-supplied handler**.  
- **Potential exploit:** Attackers may be able to **control the handler**, making `/GS` bypassable.  

### **Buffer Overflow: A Persistent Threat**
- **"Attack of the decade"** (1990s, 2000s, and beyond).  
- **Preventative Measures:**
  - Use **safe programming languages/functions** (e.g., Java, C#).  
  - Educate developers on **secure coding practices**.  
  - Utilize **static analysis tools** to detect vulnerabilities.  
- **Challenges:**
  - **Legacy code** contains unsafe practices.  
  - **Poor software development** continues to introduce vulnerabilities.  

### **Buffer Overflow Countermeasures**
- **Staying within bounds:**
  - **Validate input lengths** before writing to buffers.  
  - **Ensure array indices** remain within valid limits.  
  - **Check boundary conditions** to prevent off-by-one errors.  
- **Restrict input:**
  - Limit input to **valid characters and sizes**.  
- **Limit program privileges:**  
  - **Least privilege principle** minimizes damage if overflow is exploited.  
- **Use language protections:**  
  - Many **modern languages prevent overflows** through built-in checks.  
- **Use automated analysis tools:**  
  - **Static analyzers** help detect vulnerable code patterns.  
- **Canary values:**  
  - **Detect stack modifications** and terminate execution when tampered.  

### **Incomplete Mediation**
- **Definition:** Occurs when software fails to properly validate or process input before using it.  
- **Example:**  
  - `strcpy(buffer, argv[1])` → If `len(buffer) < len(argv[1])`, a **buffer overflow** occurs.  
  - **Solution:** Validate `argv[1]` length before copying.  

### **Input Validation**
- **Example: Web Form Data Manipulation**
  - **Client-side validation:** `http://www.things.com/orders/final&custID=112&total=205`  
  - **If server doesn’t validate:** Attacker modifies total:  
    `http://www.things.com/orders/final&custID=112&total=25`  
  - **Lesson:** **Always validate input on the server**, not just the client.  

### **Incomplete Mediation in the Linux Kernel**
- **Linux Kernel Issues:**
  - Open-source but still contains **buffer overflows** due to incomplete mediation.  
  - Even well-written, high-quality code can have **subtle mediation errors**.  
  - Tools exist to detect these issues, but attackers can use them too!  

### **Key Defensive Practices**
- **Validate all input** to prevent unexpected data manipulation.  
- **Guard against user modifications** by restricting sensitive data access.  

---

### **Time-of-Check to Time-of-Use (TOCTTOU)**
- **Definition:** A security flaw where there is a **delay between checking and using data**, allowing an attacker to modify it.  
- **Example:**  
  - A program **checks file permissions**, but before using the file, an attacker **switches it** with a malicious one.  
![[Pasted image 20250303235439.png]]
### **Security Implications**
- **Results in:**
  - **Confidentiality failure** (unauthorized access).  
  - **Integrity failure** (tampered data).  
- **Main problem:** **Checking one action but performing another** due to the time lag.  

### **Time-of-Check to Time-of-Use Countermeasures**
1. **Protect critical parameters** during loss of control.  
2. **Maintain serial integrity:** No interruptions between validation and execution.  
3. **Copy request data** to a secure memory location before validation.  
4. **Seal request data** to detect modifications.  
5. **Follow reference monitor principles:**  
   - Ensure access control decisions and their results **cannot be modified by the program being checked**.  

### **Undocumented Access Points**
- **Definition:** Hidden entry points left in software during development/testing.
- **Causes:**
  - Programmers forget to remove them before release.
  - Programmers intentionally leave them for maintenance.
  - Assumption that no one will find them (false belief).  

#### **Backdoors (Trapdoors)**
- **Undocumented entry points = Security risk**  
- Can **grant unauthorized access** with **elevated privileges**.  
- Secrets don’t last long—**attackers will eventually find them**.

#### **Protection Against Undocumented Entry**
- **Rigorous code reviews** to identify hidden backdoors.  
- **Strict software development policies** to prevent hidden access points.  
- **Security-aware programming**—developers must understand the risks.  

---

### **Off-by-One Error**
- **Definition:** A programming mistake where an index is off by one.  
- **Examples:**
  - **Loop condition mistakes:** `for (i = 0; i <= n; i++)` instead of `i < n`.  
  - **Array size miscalculations:** Using an array `A[0]...A[n]` without realizing it has `n+1` elements.  
  - **String manipulations causing unexpected length changes:**  
    - Example: Converting `…` into `...` (ellipsis to three dots).  

![[Pasted image 20250303235416.png]]
#### **Issues Caused by Off-by-One Errors**
- **Data corruption** if memory overflows into unintended areas.  
- **Intermittent bugs** that appear only with large data inputs.  

#### **Prevention**
- **Always validate array bounds** before accessing elements.  
- **Ensure loops exit correctly** (`i < n` vs. `i <= n`).  
- **Account for format conversions** that might increase string length.  

---

### **Integer Overflow**
- **Definition:** When a computation exceeds the maximum integer storage limit.  
- **Happens because:**
  - Storage is **finite** (e.g., 8-bit, 16-bit, 32-bit integers).  
  - Signed vs. unsigned numbers have different ranges.  
![[Pasted image 20250303235406.png]]
#### **Effects**
- **Hardware exception/fault condition:** Triggers error-handling routines.  
- **Silent truncation:** Excess digits are lost, leading to incorrect results.  

#### **Challenges in Detection**
- **Overflow occurs only after computation**, making prevention difficult.  
- **Example:** Using an **8-bit unsigned integer** (`0 to 255`), adding `147 + 108` overflows the range.  

#### **Prevention**
- **Use compiler-generated checks** (some compilers detect overflow).  
- **Manually check before arithmetic operations** (e.g., verify operands before addition).  
- **Use larger data types (e.g., 64-bit integers)** if necessary.  

### **Unterminated Null-Terminated String**
- **Definition:** A string in C that **relies on `\0` (null byte)** to mark its end.
- **Common issue:** If the **null byte is accidentally removed or overwritten**, the program **keeps reading memory** until another `\0` is found.

![[Pasted image 20250303235354.png]]
#### **Causes & Exploitation**
- **Accidental cause:**  
  - Overwriting part of a string **removes the null terminator**.
  - Functions handling strings **fail to enforce termination**.
- **Intentional attack:**  
  - Attackers inject **overly long strings** to corrupt memory.
  - Buffer overflows **allow arbitrary code execution**.

#### **Consequences**
- **Memory over-read:** Application **reads unintended memory**.
- **Data leakage:** Potential exposure of **sensitive memory contents**.
- **Buffer overflow:** If string functions **do not enforce size limits**, stack/heap corruption can occur.

---

### **Parameter Length, Type, and Number**
- **Definition:** Incorrect handling of function parameters leads to security issues.
- **Common issues:**
  - **Too many parameters:** Function expects `n` parameters but receives `n+1`.
  - **Incorrect data type/size:** Function expects an `int` but gets a `long`.
  - **Excessively long input strings:** May cause **buffer overflows**.

#### **Mitigation Strategies**
- **Validate function parameters** before processing.
- **Enforce strict data types** (e.g., use `size_t` for size-related variables).
- **Restrict input length** to prevent memory corruption.

---

### **Unsafe Utility Programs in C**
- **Risk:** Standard C library functions **lack built-in bounds checking**.
- **Example:**
  - `strcpy(dest, src)` copies **without checking length**, risking buffer overflow.
  - Safer alternative: `strncpy(dest, src, max)`, which **limits copied characters**.

#### **Better Alternatives**
- **Use safer functions:**  
  - `strncpy()` instead of `strcpy()`.  
  - `strncat()` instead of `strcat()`.  
  - `sprintf_s()` instead of `sprintf()`.  
- **Prefer modern memory-safe languages** (Python, Rust).  
- **Implement manual bounds checking** when using C.  

### **Race Conditions**
- **Definition:** A vulnerability where **the timing of concurrent operations** affects the program’s behavior.
- **Security Requirement:** Security processes should be **atomic** (i.e., should occur **all at once**).
- **How attacks occur:**  
  - The process **occurs in stages**, allowing an attacker to **intervene between steps**.
  - Common attack scenario: **Modify data between an authorization check and an action execution**.

---

### **mkdir Race Condition**
#### **Normal Operation**
1. **Allocate space** for the new directory.  
2. **Transfer ownership** to the user.

![[Pasted image 20250303235334.png]]
#### **Attack Scenario**
1. **Allocate space** for a new directory (`mkdir`).  
2. **Create a symbolic link** pointing to a critical file (e.g., `/etc/passwd`).  
3. **Transfer ownership** (ownership mistakenly given to the attacker).
![[Pasted image 20250303235322.png]]
- **Key issue:** The attacker exploits a small **time gap** between **step 1** (allocation) and **step 3** (ownership transfer).
- **Effect:** The attacker **gains control of critical system files**.

---

### **Why Race Conditions Are Dangerous**
- **Common but hard to exploit** – Timing must be precise.
- **Potentially more common than buffer overflows**.
- **Can allow privilege escalation**, unauthorized file access, or arbitrary code execution.

---

### **Mitigation Strategies**
- **Make security-critical processes atomic** (i.e., ensure they happen **as a single unit**).
- **Use synchronization mechanisms** (e.g., **locks, mutexes, and semaphores**).
- **Apply the principle of least privilege** – Minimize access rights.
- **Avoid using temporary files with predictable names** – Use **secure random filenames** instead.
- **Implement input validation** to **detect unauthorized changes** before execution.

### **Malware**
- **Definition:** Malicious programs designed to **cause harm, steal data, or disrupt systems**.
- **Categories of Malware:**
  - **Virus** – Self-replicating program that attaches to other programs.
  - **Worm** – Self-replicating program that spreads through networks.
  - **Trojan Horse** – Appears legitimate but has hidden malicious functions.

---

### **Types of Malware & Characteristics**

| **Code Type**          | **Characteristics** |
|------------------------|--------------------|
| **Virus**             | Self-replicating, infects other programs. |
| **Trojan Horse**      | Contains hidden, unexpected malicious functionality. |
| **Worm**             | Spreads copies of itself over a network, often reducing performance. |
| **Rabbit**            | Rapid self-replication to **exhaust system resources**. |
| **Logic Bomb**        | Triggers an action when a specific condition is met. |
| **Time Bomb**         | Triggers an action at a predetermined time. |
| **Dropper**           | Transfers and installs other malicious code (e.g., virus, Trojan). |
| **Hostile Mobile Code** | Semi-autonomous malicious agent transmitted online. |
| **Script Attack**     | Malicious JavaScript or ActiveX code embedded in web pages. |

---

### **Advanced Malware Variants**
| **Code Type**           | **Characteristics** |
|-------------------------|--------------------|
| **RAT (Remote Access Trojan)** | Grants remote control over an infected machine. |
| **Spyware**             | Covertly collects and transmits user data. |
| **Bot**                | Semi-autonomous agent controlled remotely. |
| **Zombie**             | Infected computer under remote control. |
| **Browser Hijacker**    | Modifies browser settings, redirects traffic. |
| **Rootkit**            | Installed in privileged OS areas, making detection difficult. |
| **Trapdoor / Backdoor** | Allows unauthorized access, bypassing authentication. |
| **Tool / Toolkit**      | Identifies system vulnerabilities but is not inherently malicious. |
| **Scareware**          | Fake security warnings designed to trick users. |

---

### **Key Takeaways**
- Malware can be **self-propagating (viruses, worms, bots)** or require **user execution (Trojans, droppers, scareware)**.
- Some malware focuses on **system compromise (rootkits, backdoors)**, while others aim at **exhausting resources (rabbits, botnets)**.
- **Defense strategies:** Use **antivirus software, firewalls, behavior monitoring, and secure coding practices**.

### **Harm from Malicious Code**
#### **Harm to Users and Systems**
- **Data Theft & Modification**:
  - Stealing sensitive information (**passwords, financial data**).
  - Modifying system information (**Windows registry, system settings**).
  - Encrypting or deleting files.

- **System Manipulation**:
  - Sending emails to user contacts (spreading infection).
  - Attaching to critical system files.
  - Hiding copies in multiple locations for persistence.

#### **Harm to the World**
- **Mass Infections**:
  - Malware spreads exponentially, infecting millions.
  - Infected systems become **staging areas** for further attacks.

---

### **Transmission & Propagation**
- **Common Infection Methods**:
  - **Setup & Installer Programs** – Malware bundled with legitimate software.
  - **Email Attachments** – Infected executable or document files.
  - **Autorun** – Executed automatically from USB or CD/DVD.
  - **Non-malicious Programs**:
    - **Appended viruses** – Attach to program end.
    - **Surrounding viruses** – Wrap around existing code.

---

### **Malware Activation**
- **One-time Execution**:
  - **Boot Sector Viruses** – Infects storage device boot sector.
  - **Memory-Resident Viruses** – Stays active in system memory.
  - **Application Files & Code Libraries** – Embedded within software.

---

### **Virus Effects & Methods**
| **Virus Effect**            | **How It Works** |
|-----------------------------|-----------------|
| **Attach to Executable Programs** | Modifies file directory or writes to an executable. |
| **Attach to Data or Control Files** | Modifies directory, rewrites/appends data. |
| **Remain in Memory** | Modifies interrupt handler table, loads into memory. |
| **Infect Disks** | Intercepts OS calls, modifies system files. |
| **Conceal Itself** | Intercepts system calls, hides files. |
| **Spread Infection** | Infects **boot sector, system programs, or executable files**. |
| **Prevent Deactivation** | Reinfects system after removal attempts. |

---

### **Virus Detection**
- **Virus scanners detect infections using:**
  - **Signatures** – Known string patterns in files & memory.
  - **Execution Patterns** – Detects unusual program behavior.
  - **Storage Patterns** – Analyzes file structure for anomalies.

- **Detection Challenges**:
  - Traditional scanners detect **only 45%** of infections.
  - Malware evolves faster than **signature updates**.
  - **Behavior-based analysis** is needed for advanced threats.

### **Virus Signatures**
- A **signature** is a unique **string of bits** or **hash value** found in malware.
- Example: **0x23956a58bd910345**
- Scanners search for these patterns in files.
- **Issues**:
  - Same signature may appear in non-malicious files.
  - Low probability, but software is not random, making detection likely.
![[Pasted image 20250303235254.png]]

---

### **Malware Detection Methods**
1. **Signature Detection**
   - **How it works**: Compares files with known virus signatures.
   - **Advantages**:
     - Effective against known malware.
     - Minimal impact on users/admins.
   - **Disadvantages**:
     - Large signature files slow scanning.
     - Requires frequent updates.
     - Cannot detect unknown malware.
     - Cannot detect certain new malware types.

2. **Change Detection**
   - **How it works**: Monitors file integrity by hashing and comparing.
   - **Advantages**:
     - No false negatives.
     - Can detect unknown malware.
   - **Disadvantages**:
     - Frequent false positives.
     - High admin burden.
     - Requires additional signature-based validation.

3. **Anomaly Detection**
   - **How it works**: Monitors system behavior for unusual activities.
   - **Advantages**:
     - Can detect **unknown malware**.
   - **Disadvantages**:
     - Hard to define **normal** behavior.
     - Malware can mimic normal behavior.
     - Needs to be combined with other methods.

---

### **Countermeasures**
#### **For Users**
- Download software **only from trusted sources**.
- **Test** new software in **isolated environments**.
- Open email attachments **only if verified**.
- Treat **all websites as potential threats**.
- **Maintain regular backups**.

#### **For Developers**
- **Software Engineering Practices**:
  - **Information Hiding** – Describe functionality, not implementation.
  - **Modularity** – Use low coupling, high cohesion.
  - **Mutual Suspicion** – Assume all components are potentially unsafe.
  - **Confinement** – Limit malware impact to a small area.
  - **Simplicity** – Reduce complexity for better security.
  - **Genetic Diversity** – Avoid uniformity to prevent widespread attacks.

- **Code Testing**:
  - **Unit Testing**
  - **Integration Testing**
  - **Function Testing**
  - **Performance Testing**
  - **Acceptance Testing (QA)**
  - **Installation Testing**
  - **Regression Testing** – Ensures updates don’t introduce new issues.
  - **Penetration Testing** – Simulates attacks to find vulnerabilities.

---

### **Security-Specific Countermeasures**
#### **Design Principles for Security**
- **Least Privilege** – Users/processes get only required access.
- **Economy of Mechanism** – Keep security designs simple.
- **Open Design** – No reliance on secrecy.
- **Complete Mediation** – Verify all access requests.
- **Permission-Based Access** – Explicit permissions required.
- **Separation of Privilege** – Independent privileges for different tasks.
- **Least Common Mechanism** – Minimize shared mechanisms.
- **Ease of Use** – Secure systems should be user-friendly.

#### **Additional Security Measures**
- **Penetration Testing** – Identifies security weaknesses.
- **Proofs of Program Correctness** – Ensures software behaves as intended.
- **Validation & Defensive Programming** – Anticipate and handle failures.
- **Trustworthy Computing Initiative** – Train developers in security best practices.

---

### **Ineffective Countermeasures**
- **Penetrate-and-Patch** – Quick fixes miss systemic issues.
- **Security by Obscurity** – Hiding security mechanisms is ineffective.

---

### **Summary**
- **Buffer Overflow Attacks** exploit **code-data overlap** to modify execution.
- **Software vulnerabilities** include **off-by-one errors, race conditions, and incomplete mediation**.
- **Malware impacts** depend on **infection method and payload**.
- **Developers must integrate security techniques** into coding and testing.

### Made by Yashank