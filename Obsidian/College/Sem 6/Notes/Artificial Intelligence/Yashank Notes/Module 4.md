![[Pasted image 20250304231501.png]]

### **Knowledge-Based Agents**  

#### **Definition**  
- **Humans** possess knowledge that enables reasoning and decision-making.  
- Intelligence is achieved **not** through **pure reflexes** but through **reasoning on internal knowledge**.  
- **Knowledge-Based Agents (KBAs)** in AI follow this principle.  

#### **Key Characteristics**  
A **Knowledge-Based Agent** can:  
- **Maintain** an internal knowledge state.  
- **Reason** over its stored knowledge.  
- **Update** its knowledge based on new observations.  
- **Take actions** based on logical deductions.  
- **Represent** the world formally and act **intelligently**.  

#### **Example: Automated Air Conditioner**  
- **Knowledge Level:** Knows that it must **adjust temperature based on the weather**.  
- **Implementation Level:** The **actual adjustment process** based on sensed temperature.  

#### **Components of a Knowledge-Based Agent**  
1. **Knowledge Base (KB):** Stores facts and rules about the world.  
2. **Inference System:** Derives new knowledge from existing knowledge to make decisions.  

#### **Capabilities of a Knowledge-Based Agent**  
- **Represent states, actions, and knowledge** logically.  
- **Incorporate new percepts** (sensory inputs).  
- **Update its internal knowledge** dynamically.  
- **Deduce the best course of action** based on reasoning.  

### **Inference System**  

#### **Definition**  
- **Inference** refers to the process of **deriving new knowledge** from existing knowledge.  
- A **sentence** represents a **proposition about the world**.  

#### **Functions of an Inference System**  
An inference system allows an agent to:  
- **Add** new sentences to the **Knowledge Base (KB)**.  
- **Apply logical rules** to derive new conclusions.  
- **Generate new facts** to **update the KB** dynamically.  

#### **Types of Inference Rules**  
1. **Forward Chaining** (**FACT → GOAL**)  
   - Starts with known **facts** and applies inference rules to **reach a goal**.  
   - Used in **data-driven reasoning**.  
   - Example: If "It is raining" and "Rain makes roads wet," we infer **"Roads are wet"**.  

2. **Backward Chaining** (**GOAL → FACT**)  
   - Starts with a **goal** and works **backwards** to determine if known **facts** support it.  
   - Used in **goal-driven reasoning**.  
   - Example: To prove "Roads are wet," check if "It is raining" and "Rain makes roads wet."  

![[Pasted image 20250304231658.png]]

### **Operations Performed by a Knowledge-Based Agent (KBA)**  

A Knowledge-Based Agent (KBA) performs three key operations to exhibit intelligent behavior:  

#### **1. TELL**  
- **Purpose:** Updates the **Knowledge Base (KB)** with new information perceived from the environment.  
- **Function:** Ensures the KB remains **accurate and up-to-date**.  
- **Example:** If a **robotic vacuum** detects dust, it **TELLs** the KB, "Room is dirty."  

#### **2. ASK**  
- **Purpose:** Queries the KB to determine the **best action** to take.  
- **Function:** Uses **reasoning** to analyze:  
  - **Current state** of the world.  
  - **Expected outcomes** of different action sequences.  
- **Example:** The vacuum **ASKs** whether it should **start cleaning** based on the room's condition.  

#### **3. PERFORM**  
- **Purpose:** Executes the **action** determined by reasoning.  
- **Function:** The agent **acts** based on the decision made in the **ASK** step.  
- **Example:** If the KB **suggests cleaning**, the vacuum **PERFORMs** the cleaning task.  

![[Pasted image 20250304231759.png]]
![[Pasted image 20250304231811.png]]

### **Functions in a Knowledge-Based Agent (KBA)**  

A Knowledge-Based Agent (KBA) utilizes specific functions to process perceptions and determine actions efficiently.

#### **1. MAKE-PERCEPT-SENTENCE()**  
- **Purpose:** Creates a **sentence** describing what the agent perceives from the environment at a given time.  
- **Example:** If a weather bot detects rain, it returns:  
  - `"It is raining outside."`  

#### **2. MAKE-ACTION-QUERY()**  
- **Purpose:** Forms a **query** asking what action the agent should take based on its knowledge.  
- **Example:**  
  - `"Should I take an umbrella?"`  

#### **3. MAKE-ACTION-SENTENCE()**  
- **Purpose:** Returns a **sentence** confirming the selected action and its execution.  
- **Example:** If the agent decides to take an umbrella, it returns:  
  - `"Taking an umbrella and stepping outside."`  

> **Note:** The inference mechanisms that determine logical reasoning are encapsulated within the **TELL** and **ASK** operations.

![[Pasted image 20250304231841.png]]

### **Wumpus World Problem**  

The **Wumpus World** is a structured **cave environment** used to illustrate the functionality of **Knowledge-Based Agents (KBA)** in AI.  
![[Pasted image 20250304231935.png]]
#### **1. Environment Description**  
- **The Cave:** Composed of interconnected rooms through passageways.  
- **Dangers:**  
  - The **Wumpus**: A deadly creature that **eats the agent** if they enter its room.  
  - **Bottomless Pits**: Falling into them results in **instant loss**, except for the Wumpus, which is too big to fall.  
- **Objectives:**  
  - The agent must **find and grab gold** while **avoiding hazards**.  
  - The agent has **one arrow** that can kill the Wumpus.  

#### **2. Sensory Perceptions for Navigation**  
To navigate safely, the agent **perceives environmental clues**:  
- **Stench:** Rooms **adjacent** to the Wumpus contain a **bad smell**.  
- **Breeze:** Rooms **adjacent** to a Pit have a **breeze**, warning the agent of a nearby danger.  
- **Glitter:** A room **containing gold** emits a **glitter**, indicating treasure.  
- **Scream:** If the agent successfully shoots the **Wumpus**, a loud **scream** is heard throughout the cave. **The Wumpus can be killed by the agent if the agent is facing towards it**, and Wumpus will emit a horrible scream which can be heard anywhere in the cave 

#### **3. Importance in AI**  
- Demonstrates how a **Knowledge-Based Agent** can use **logical inference** and **decision-making** in **partially observable** environments.  
- Highlights the **use of knowledge representation** and **reasoning** in artificial intelligence.  

### **Assumptions in Wumpus World**
- **Grid:** The environment is a **4×4 grid**, with tiles numbered **(1,1) to (4,4)**.
- **Agent’s Start Position:** The agent **always starts** at **(1,1)**, with **prior knowledge** of the environment structure but **not the specific locations** of hazards or the goal.
- **Randomized Elements:**
  - **Wumpus:** Placed randomly in **one tile** (except (1,1)), **unknown** to the agent.
  - **Gold:** Placed randomly in **one tile** (except (1,1)), **unknown** to the agent.
  - **Pits:** Each tile (except (1,1)) has a **20% probability** of containing a **pit**.
- **Hazards:**
  - If the agent **steps into the Wumpus’s tile**, it is **eaten**.
  - If the agent **falls into a pit**, it is **trapped**.

### **PEAS Description**
#### **Performance Measure**
- **+1000** → Climbing **out of the cave with gold**.
- **–1000** → **Falling into a pit** or **being eaten by the Wumpus**.
- **–1** → **For each action taken** (to encourage efficiency).
- **–10** → **For shooting the arrow** (to discourage unnecessary shooting).
- The game **ends** when the **agent dies** or **escapes** the cave.

#### **Environment**
- **A 4×4 grid** of interconnected rooms.
- The **agent always starts at (1,1)**, **facing right**.
- **Gold and Wumpus locations** are chosen randomly, **uniformly distributed**.
- Each tile (except the start) **has a 0.2 probability** of being a pit.

#### **Actuators (Agent's Actions)**
- **Left Turn (90°)** → Rotate **left**.
- **Right Turn (90°)** → Rotate **right**.
- **Move Forward** → Move **one step** in the current direction.
- **Grab** → Pick up **gold**.
- **Release** → Drop **gold**.
- **Shoot** → Fire an **arrow** (to kill the Wumpus if aligned).

#### **Sensors in Wumpus World**
The agent has **five** sensors, each providing **binary (1-bit) information**:

1. **Stench** → **Detects the Wumpus**  
   - The agent **perceives a stench** in the **tile containing the Wumpus** and the **adjacent tiles (not diagonal)**.

2. **Breeze** → **Detects a Pit**  
   - The agent **perceives a breeze** in the tiles **adjacent (not diagonal) to a pit**.

3. **Glitter** → **Detects Gold**  
   - The agent **perceives glitter** when **standing on the gold's tile**.

4. **Bump** → **Detects Walls**  
   - The agent **perceives a bump** when **walking into a wall**.

5. **Scream** → **Detects Wumpus Death**  
   - If the **Wumpus is killed**, it **emits a scream**, which can be **heard anywhere in the cave**.

![[Pasted image 20250304232241.png]]

### **Moves Allowed in Wumpus World**
The agent can perform the following moves:
- **L (Left), R (Right), U (Up), D (Down)**
- **G (Grab)** → Used when the agent finds gold.

![[Pasted image 20250304232348.png]]
### **Agent's Movement & Inference**
1. **Start at (1,1)**
   - Perceives **Stench at (1,2)** → Wumpus might be nearby.
   - Perceives **Breeze at (2,1)** → Pit is nearby.

2. **Checking Pit Locations**
   - **(2,1) has Breeze**, so **(3,1) or (2,2) might have a Pit**.
   - Moves back to **(1,1) for safety**.

3. **Exploring (1,2)**
   - **Stench at (1,2)** → Wumpus could be at **(1,3) or (2,2)**.
   - Concludes **(2,2) is SAFE**.

4. **Moving to (2,2)**
   - Moves to **(2,3), perceives Breeze at (3,2)**.
   - Moves to **(3,2), finds pits at (3,1) & (3,3)**.
   - Moves back to **(2,2) and explores (2,3)**.

5. **Gold Found at (2,3)!**
   - Grabs the gold and returns via the same safe path.

6. **Using the Arrow**
   - Shoots at **(3,3) but no scream**, meaning no Wumpus there.
   - Shoots at **(1,3), hears a scream** → Confirms Wumpus is eliminated.

![[Pasted image 20250304232400.png]]

---

### **Wumpus World Properties**
- **Partially Observable** → The agent perceives **only adjacent rooms**.
- **Deterministic** → The outcomes are **fixed and predictable**.
- **Sequential** → The **order of actions matters** (e.g., grabbing gold before exiting).
- **Static** → The **Wumpus and Pits do not move**.
- **Discrete** → The **environment is grid-based with finite locations**.
- **Single-Agent** → Only **one agent** operates (Wumpus is **not** an agent).

### **Propositional Logic (PL)**
- **Definition**: The simplest form of logic where statements are represented as **propositions**.
- **Proposition**: A declarative statement that is either **true or false**.

#### **Examples**
- ✅ *It is Sunday.* (**True**)
- ❌ *The Sun rises from the West.* (**False**)
- ❌ *3 + 3 = 7* (**False**)
- ✅ *5 is a prime number.* (**True**)

---

### **Basic Facts about Propositional Logic**
- **Boolean Logic** → Works on **0 (False) and 1 (True)**.
- **Symbolic Representation** → Uses **variables** to denote propositions (**A, B, C, P, Q, R, etc.**).
- **Truth Value** → Propositions are **either true or false**, but **not both**.
- **Components of PL**:
  - **Objects**: Entities represented in logic.
  - **Relations/Functions**: Describe connections between objects.
  - **Logical Connectives (Operators)**: Used to connect statements.

#### **Logical Connectives**
- **Negation (¬P)** → "Not P"
- **Conjunction (P ∧ Q)** → "P and Q"
- **Disjunction (P ∨ Q)** → "P or Q"
- **Implication (P → Q)** → "If P then Q"
- **Biconditional (P ↔ Q)** → "P if and only if Q"

---

### **Special Types of Propositions**
- **Tautology** → A formula that is **always true**.
  - Example: *(P ∨ ¬P)* (Law of Excluded Middle)
- **Contradiction** → A formula that is **always false**.
  - Example: *(P ∧ ¬P)* (Contradiction)
- **Non-Propositional Statements**: 
  - **Questions**: *Where is John?*
  - **Commands**: *Close the door!*
  - **Opinions**: *I like ice cream!*

These are **not propositions** because they cannot be assigned **true or false** values.

### **Propositional Logic - Revision**

![[Pasted image 20250304232535.png]]
![[Pasted image 20250304232543.png]]
#### **1. Formal Proofs**
- **Definition**: A sequence of logical steps used to **derive conclusions** from premises using inference rules.
- **Common Inference Rules**:
  - **Modus Ponens**: If (P → Q) and P are true, then Q must be true.
  - **Modus Tollens**: If (P → Q) and ¬Q are true, then ¬P must be true.
  - **Disjunctive Syllogism**: If (P ∨ Q) and ¬P are true, then Q must be true.
  - **Hypothetical Syllogism**: If (P → Q) and (Q → R), then (P → R).

#### **2. Normal Forms**
- **Conjunctive Normal Form (CNF)**:
  - A conjunction (AND) of disjunctions (OR).
  - Example: *(P ∨ Q) ∧ (¬R ∨ S)*
- **Disjunctive Normal Form (DNF)**:
  - A disjunction (OR) of conjunctions (AND).
  - Example: *(P ∧ Q) ∨ (¬R ∧ S)*
- **Negation Normal Form (NNF)**:
  - Uses only **¬, ∧, and ∨** (no implications).
  - Example: *¬(P ∨ Q) → (¬P ∧ ¬Q)*

### **Propositional Logic - Revision**
#### **1. Logical Connectives**
- **Negation (¬P)**: The opposite of proposition P.
  - **Example**: "It is not raining." → **¬P**

- **Conjunction (P ∧ Q)**: True if **both** P and Q are true.
  - **Example**: "Rohan is intelligent and hardworking."  
    - **P** = Rohan is intelligent  
    - **Q** = Rohan is hardworking  
    - **P ∧ Q** = "Rohan is intelligent ∧ Rohan is hardworking"

- **Disjunction (P ∨ Q)**: True if **at least one** of P or Q is true.
  - **Example**: "Ritika is a doctor or an engineer."  
    - **P** = Ritika is a doctor  
    - **Q** = Ritika is an engineer  
    - **P ∨ Q** = "Ritika is a doctor ∨ Ritika is an engineer"

- **Implication (P → Q)**: "If P, then Q" (False only if P is true and Q is false).
  - **Example**: "If it is raining, then the street is wet."
    - **P** = It is raining  
    - **Q** = The street is wet  
    - **P → Q** = "If it is raining → the street is wet"

- **Biconditional (P ⇔ Q)**: True when **both P and Q are either true or false**.
  - **Example**: "If I am breathing, then I am alive."
    - **P** = I am breathing  
    - **Q** = I am alive  
    - **P ⇔ Q** = "I am breathing ⇔ I am alive"

![[Pasted image 20250304232619.png]]

### **Properties of Operators**
#### **1. Commutativity**
- **Order does not matter** for ∧ (AND) and ∨ (OR):
  - **P ∧ Q = Q ∧ P**
  - **P ∨ Q = Q ∨ P**

#### **2. Associativity**
- **Grouping does not matter** for ∧ and ∨:
  - **(P ∧ Q) ∧ R = P ∧ (Q ∧ R)**
  - **(P ∨ Q) ∨ R = P ∨ (Q ∨ R)**

#### **3. Identity Element**
- **AND with True gives P**:
  - **P ∧ True = P**
- **OR with True always results in True**:
  - **P ∨ True = True**

#### **4. Distributive Property**
- **AND distributes over OR**:
  - **P ∧ (Q ∨ R) = (P ∧ Q) ∨ (P ∧ R)**
- **OR distributes over AND**:
  - **P ∨ (Q ∧ R) = (P ∨ Q) ∧ (P ∨ R)**

#### **5. De Morgan’s Laws**
- **Negation of AND converts to OR**:
  - **¬(P ∧ Q) = (¬P) ∨ (¬Q)**
- **Negation of OR converts to AND**:
  - **¬(P ∨ Q) = (¬P) ∧ (¬Q)**

#### **6. Double Negation Elimination**
- **Two negations cancel out**:
  - **¬(¬P) = P**

### **Inference Rules**
#### **1. Modus Ponens (Law of Detachment)**
- **If P → Q is true and P is true, then Q must be true.**
- **Example:**
  - **Statement-1:** "If I am sleepy, then I go to bed." → **P → Q**
  - **Statement-2:** "I am sleepy." → **P**
  - **Conclusion:** "I go to bed." → **Q**
![[Pasted image 20250304232731.png]]
#### **2. Modus Tollens**
- **If P → Q is true and Q is false, then P must be false.**
- **Example:**
  - **Statement-1:** "If I am sleepy, then I go to bed." → **P → Q**
  - **Statement-2:** "I do not go to bed." → **¬Q**
  - **Conclusion:** "I am not sleepy." → **¬P**
![[Pasted image 20250304232736.png]]
#### **3. Hypothetical Syllogism (Transitivity)**
- **If P → Q and Q → R, then P → R.**
- **Example:**
  - **Statement-1:** "If you have my home key, then you can unlock my home." → **P → Q**
  - **Statement-2:** "If you can unlock my home, then you can take my money." → **Q → R**
  - **Conclusion:** "If you have my home key, then you can take my money." → **P → R**
![[Pasted image 20250304232741.png]]
#### **4. Disjunctive Syllogism**
- **If P ∨ Q is true and ¬P is true, then Q must be true.**
- **Example:**
  - **Statement-1:** "Today is Sunday or Monday." → **P ∨ Q**
  - **Statement-2:** "Today is not Sunday." → **¬P**
  - **Conclusion:** "Today is Monday." → **Q**
![[Pasted image 20250304232816.png]]

### **Limitations of Propositional Logic**
1. **Inability to Represent Quantifiers**
   - Propositional Logic **cannot express statements involving "all," "some," or "none."**
   - **Examples:**
     - "All the girls are intelligent."
     - "Some apples are sweet."

2. **Limited Expressive Power**
   - **PL cannot represent relationships between objects** in a structured way.
   - It does not allow reasoning about **individual properties** of objects.
   - **Examples:**
     - "Some humans are intelligent."
     - "Sachin likes cricket."

3. **Lack of Variables**
   - Propositional Logic **deals with entire statements as single entities** without breaking them into subjects and predicates.
   - It cannot capture the internal structure of sentences.

### **Need for More Expressive Logic**
- **First-Order Logic (FOL)** overcomes these limitations by introducing:
  - **Quantifiers** (∃ "some", ∀ "all")
  - **Relations between objects**
  - **Variables** to generalize statements

### **Knowledge Base for Wumpus World**
#### **Atomic Propositions**
- **Pit Representation:** Let $P_{i,j}$ be true if there is a Pit in room $[i, j]$.
- **Breeze Perception:** Let $B_{i,j}$ be true if the agent perceives Breeze in $[i, j]$.
- **Wumpus Representation:** Let $W_{i,j}$ be true if Wumpus is in square $[i, j]$.
- **Stench Perception:** Let $S_{i,j}$ be true if the agent perceives Stench in square $[i, j]$.
![[Pasted image 20250304233529.png]]
---

### **Rules for Wumpus World**
#### **Proving Wumpus is in (1,3)**

1. Apply **Modus Ponens** on $\neg S_{1,1}$ and Rule $R_1$, since there is no Stench in (1,1), Wumpus is not in any adjacent square.  
2. Apply **Modus Ponens** on $\neg S_{2,1}$ and Rule $R_2$, since (2,1) also has no Stench, Wumpus is not in $ (2,2) $ or $ (1,1) $.
3. Apply **Modus Ponens** on $S_{1,2}$ and Rule $R_4$, since Stench is perceived in (1,2), Wumpus must be in one of the adjacent squares: $W_{1,3} \lor W_{1,1} \lor W_{2,2} \lor W_{1,2}$.
4. Apply **Unit Resolution** on $W_{1,3} \lor W_{1,2} \lor W_{2,2} \lor W_{1,1}$ and $\neg W_{1,1}$, since Wumpus is not in (1,1), the possibilities reduce to: $W_{1,3} \lor W_{1,2} \lor W_{2,2}$.
5. Apply **Unit Resolution** on $W_{1,3} \lor W_{1,2} \lor W_{2,2}$ and $\neg W_{2,2}$, since Wumpus is not in (2,2), the possibilities reduce further to: $W_{1,3} \lor W_{1,2}$.
6. Apply **Unit Resolution** on $W_{1,3} \lor W_{1,2}$ and $\neg W_{1,2}$, since Wumpus is not in (1,2), we conclude: $W_{1,3}$.  
   **Thus, Wumpus is in (1,3)!**
![[Pasted image 20250304233548.png]]
![[Pasted image 20250304233558.png]]

### **Proving $W_{1,3}$**
1. Apply **Modus Ponens (MP)** with $\neg S_{1,1}$ and Rule $R_1$:  
   $$\neg W_{1,1} \land \neg W_{1,2} \land \neg W_{2,1}$$
2. Apply **AND-Elimination**, obtaining three sentences:  
   $$\neg W_{1,1}, \quad \neg W_{1,2}, \quad \neg W_{2,1}$$
3. Apply **MP** to $\neg S_{2,1}$ and Rule $R_2$, then apply **AND-Elimination**:  
   $$\neg W_{2,2}, \quad \neg W_{2,1}, \quad \neg W_{3,1}$$
4. Apply **MP** to $S_{1,2}$ and Rule $R_4$, obtaining:  
   $$W_{1,3} \lor W_{1,2} \lor W_{2,2} \lor W_{1,1}$$
5. Apply **Unit Resolution** on $(W_{1,3} \lor W_{1,2} \lor W_{2,2} \lor W_{1,1})$ and $\neg W_{1,1}$:  
   $$W_{1,3} \lor W_{1,2} \lor W_{2,2}$$
6. Apply **Unit Resolution** with $(W_{1,3} \lor W_{1,2} \lor W_{2,2})$ and $\neg W_{2,2}$:  
   $$W_{1,3} \lor W_{1,2}$$
7. Apply **Unit Resolution** with $(W_{1,3} \lor W_{1,2})$ and $\neg W_{1,2}$:  
   $$W_{1,3}$$  
   **Thus, $W_{1,3}$ is proven (Q.E.D.).**

![[Pasted image 20250304233707.png]]

### **Proving that Wumpus is in Room $(1,3)$**

![[Pasted image 20250304233824.png]]
#### **Step 1: Apply Modus Ponens with $\neg S_{1,1}$ and Rule $R_1$**
- Given rule: $\neg S_{1,1} \rightarrow \neg W_{1,1} \land \neg W_{1,2} \land \neg W_{2,1}$
- Given $\neg S_{1,1}$, applying **Modus Ponens (MP)**:
  $$\neg W_{1,1} \land \neg W_{1,2} \land \neg W_{2,1}$$
![[Pasted image 20250304233839.png]]
#### **Step 2: Apply AND-Elimination Rule**
- Extracting individual statements:
  $$\neg W_{1,1}, \quad \neg W_{1,2}, \quad \neg W_{2,1}$$
![[Pasted image 20250304233848.png]]
#### **Step 3: Apply Modus Ponens with $\neg S_{2,1}$ and Rule $R_2$**
- Given rule: $\neg S_{2,1} \rightarrow \neg W_{2,1} \land \neg W_{2,2} \land \neg W_{3,1}$
- Given $\neg S_{2,1}$, applying **MP**:
  $$\neg W_{2,1} \land \neg W_{2,2} \land \neg W_{3,1}$$
![[Pasted image 20250304233854.png]]
#### **Step 4: Apply AND-Elimination Rule**
- Extracting individual statements:
  $$\neg W_{2,1}, \quad \neg W_{2,2}, \quad \neg W_{3,1}$$

#### **Step 5: Apply Modus Ponens with $S_{12}$ and Rule $R_4$**
- Given rule: $S_{1,2} \rightarrow W_{1,3} \lor W_{1,2} \lor W_{2,2} \lor W_{1,1}$
- Given $S_{1,2}$, applying **MP**:
  $$W_{1,3} \lor W_{1,2} \lor W_{2,2} \lor W_{1,1}$$
![[Pasted image 20250304233901.png]]
#### **Step 6: Apply Unit Resolution on $W_{1,3} \lor W_{1,2} \lor W_{2,2} \lor W_{1,1}$ and $\neg W_{1,1}$**
- Since $\neg W_{1,1}$, resolving:
  $$W_{1,3} \lor W_{1,2} \lor W_{2,2}$$
![[Pasted image 20250304234003.png]]
#### **Step 7: Apply Unit Resolution on $W_{1,3} \lor W_{1,2} \lor W_{2,2}$ and $\neg W_{2,2}$**
- Since $\neg W_{2,2}$, resolving:
  $$W_{1,3} \lor W_{1,2}$$
![[Pasted image 20250304234012.png]]
#### **Step 8: Apply Unit Resolution on $W_{1,3} \lor W_{1,2}$ and $\neg W_{1,2}$**
- Since $\neg W_{1,2}$, resolving:
  $$W_{1,3}$$
![[Pasted image 20250304234020.png]]

Thus, **Wumpus is in room (1,3) (Q.E.D.).**

### **First-Order Logic (FOL)**
#### **Example 1: Parrots are green**
- $$\forall X \quad Parrot(X) \rightarrow Green(X)$$

#### **Example 2: All kids like toys**
- $$\forall X \quad Kid(X) \rightarrow Likes(X, Toys)$$

#### **Example 3: Some kids like toys**
- $$\exists X \quad Kid(X) \land Likes(X, Toys)$$

### **Quantifiers in FOL**
- **Universal Quantifier ($\forall$ X)** → Statement applies to all objects.
- **Existential Quantifier ($\exists$ X)** → Statement applies to at least one object.

### **First-Order Logic in AI**
- **Used for Knowledge Representation in AI**  
- **Extension of Propositional Logic**  
- **Represents natural language statements concisely**  
- **Also known as Predicate Logic or First-Order Predicate Logic**  

### **Key Components of FOL**
- **Objects:** People, numbers, colors, wars, theories, squares, pits, wumpus, etc.
- **Relations:**
  - Unary: $Red(X)$, $Round(X)$, $Adjacent(A, B)$  
  - N-ary: $SisterOf(A, B)$, $BrotherOf(A, B)$, $HasColor(A, Red)$, etc.
- **Functions:**  
  - $FatherOf(A)$, $BestFriend(A)$, $ThirdInningOf(Game)$, $EndOf(Story)$

### **Syntax of First-Order Logic (FOL)**

#### **1. Constant Symbols**
- Represent specific individuals in the domain.  
  **Examples:**  
  - $$Divya, 3$$  

#### **2. Function Symbols**
- Map individuals to other individuals.  
  **Examples:**  
  - $$FatherOf(Divya) = John$$  
  - $$ColorOf(Sky) = Blue$$  

#### **3. Predicate Symbols**
- Map individuals to truth values (True/False).  
  **Examples:**  
  - $$Greater(5,3)$$  
  - $$Green(Grass)$$  
  - $$Color(Grass, Green)$$  

---

### **Other Syntax Components**
#### **4. Variable Symbols**
- Represent generic entities.  
  **Examples:**  
  - $$x, y$$  

#### **5. Logical Connectives** (Same as Propositional Logic)
- **Negation:** $$\neg P$$  
- **Conjunction:** $$P \land Q$$  
- **Disjunction:** $$P \lor Q$$  
- **Implication:** $$P \Rightarrow Q$$  
- **Biconditional:** $$P \Leftrightarrow Q$$  

#### **6. Quantifiers**
- **Universal Quantifier ($\forall$)** → "For all"  
  **Example:** $$\forall x \quad Human(x) \rightarrow Mortal(x)$$  
- **Existential Quantifier ($\exists$)** → "There exists at least one"  
  **Example:** $$\exists x \quad Loves(x, Music)$$  
![[Pasted image 20250304234448.png]]

### **Atomic Sentences**
- **Definition:** Basic sentences in First-Order Logic (FOL).
- **Structure:** Formed using a predicate symbol followed by a sequence of terms.
- **Representation:**  
  $$\text{Predicate}(term_1, term_2, ..., term_n)$$
- **Example:**  
  - "Ravi and Ajay are brothers" → $$Brothers(Ravi, Ajay)$$  

---

### **Complex Sentences**
- **Definition:** Formed by combining atomic sentences using logical connectives.
- **Components of FOL Statements:**  
  - **Subject:** The main entity of the statement.  
  - **Predicate:** Defines a relation binding two terms together.  

**Example:**  
- Consider the statement: *"x is an integer."*  
  - **Subject:** $$x$$  
  - **Predicate:** "is an integer."  
  - **FOL Representation:** $$Integer(x)$$  
![[Pasted image 20250304234540.png]]

### **Quantifiers in First-Order Logic (FOL)**

#### **1. Universal Quantifier ( ∀ )**
- **Meaning:** Represents statements that apply to *all* individuals in a domain.
- **Common phrases:**  
  - "For all x"  
  - "For each x"  
  - "For every x"  
- **Example:**  
  $$\forall x\ (Man(x) \rightarrow Drinks(x, Coffee))$$  
  - **Interpretation:** "For all x, if x is a man, then x drinks coffee."

---

#### **2. Existential Quantifier ( ∃ )**
- **Meaning:** Represents statements that apply to *at least one* individual.
- **Common phrases:**  
  - "There exists an x"  
  - "For some x"  
  - "At least one x"  
- **Example:**  
  $$\exists x\ (Kid(x) \wedge Intelligent(x))$$  
  - **Interpretation:** "There exists some x such that x is a kid and x is intelligent."

![[Pasted image 20250304234736.png]]
![[Pasted image 20250304234746.png]]

### **Points to Remember**
- **Universal Quantifier ( ∀ )** → Main connective: **Implication ( → )**  
- **Existential Quantifier ( ∃ )** → Main connective: **And ( ∧ )**

---

### **Properties of Quantifiers**
- **Universal Quantifier:** $$\forall x\forall y \equiv \forall y\forall x$$  
- **Existential Quantifier:** $$\exists x\exists y \equiv \exists y\exists x$$  
- **Mixed Quantifiers:** $$\exists x\forall y \not\equiv \forall y\exists x$$  

---

### **Examples of FOL using Quantifiers**

#### **1. All birds fly**
- **Predicate:** $$Fly(Bird)$$  
- **FOL Representation:** $$\forall x (Bird(x) \rightarrow Fly(x))$$  

#### **2. Every man respects his parent**
- **Predicate:** $$Respect(x, y)$$ where $$x = Man$$, $$y = Parent$$  
- **FOL Representation:** $$\forall x (Man(x) \rightarrow Respects(x, Parent))$$  

#### **3. Some boys play cricket**
- **Predicate:** $$Play(x, y)$$ where $$x = Boys$$, $$y = Cricket$$  
- **FOL Representation:** $$\exists x (Boys(x) \wedge Play(x, Cricket))$$  

---

### **More Examples**
1. **All students are smart:**  
   $$\forall x (Student(x) \rightarrow Smart(x))$$  
2. **There exists a student:**  
   $$\exists x\ Student(x)$$  
3. **There exists a smart student:**  
   $$\exists x (Student(x) \wedge Smart(x))$$  
4. **Every student loves some student:**  
   $$\forall x (Student(x) \rightarrow \exists y (Student(y) \wedge Loves(x,y)))$$  
5. **Bill is a student:**  
   $$Student(Bill)$$  
6. **Bill takes either Analysis or Geometry (but not both):**  
   $$Takes(Bill, Analysis) \iff \neg Takes(Bill, Geometry)$$  
7. **Bill takes Analysis or Geometry (or both):**  
   $$Takes(Bill, Analysis) \vee Takes(Bill, Geometry)$$  
8. **Bill takes Analysis and Geometry:**  
   $$Takes(Bill, Analysis) \wedge Takes(Bill, Geometry)$$  
9. **Bill does not take Analysis:**  
   $$\neg Takes(Bill, Analysis)$$  
10. **No student loves Bill:**  
   $$\neg \exists x (Student(x) \wedge Loves(x, Bill))$$  
11. **Bill has at least one sister:**  
   $$\exists x\ SisterOf(x, Bill)$$  
12. **Bill has no sister:**  
   $$\neg \exists x\ SisterOf(x, Bill)$$  
### **Knowledge Engineering**
- **Definition:** Process of creating a knowledge-based system by acquiring, structuring, and representing domain knowledge.

#### **Examples of Knowledge Engineering Applications**
- **Automated Teaching:** Capturing knowledge from teachers and subject matter experts (SMEs) for subjects like biology and computer science.
- **Medical Decision Support:** Oncologists choosing the best treatment based on medical journals, textbooks, and drug databases.

---

### **Knowledge Engineering in First-Order Logic (FOL)**

#### **Steps to Develop a Knowledge Base**
1. **Identify the Problem or Task**  
   - Define the **range of questions** to be answered.  
   - Determine **available facts** in the domain.  
   - Establish **connections between problems and solutions**.

2. **Assemble the Relevant Knowledge**  
   - Conduct **knowledge acquisition** from experts and sources.  
   - Understand **the domain's scope** and working principles.

3. **Decide on a Vocabulary**  
   - Define a **set of predicates, functions, and constants**.  
   - Choose a **representation format** for the knowledge base.  
   - **Ontology:** Specification of the meanings of symbols in the system (conceptualization).

4. **Encode General Knowledge**  
   - Formulate **domain-specific axioms** and rules.  

5. **Encode the Problem Instance**  
   - Represent **specific cases** using the general domain knowledge.

6. **Pose Queries**  
   - Apply **inference rules** to derive new facts.

7. **Debug the Knowledge Base**  
   - Verify and **correct errors** in the knowledge representation.

---
This structured process ensures effective **knowledge representation** and inference in FOL-based AI systems.

1. **Lucy is a professor:**  
    $$ Professor(Lucy) $$
    
2. **All professors are people:**  
    $$\forall x \, (Professor(x) \rightarrow Person(x))$$
    
3. **John is the dean:**  
    $$Dean(John)$$
    
4. **Deans are professors:**  
    $$\forall x \, (Dean(x) \rightarrow Professor(x))$$
    
5. **All professors consider the dean a friend or don’t know him:**  
    $$\forall x \, (Professor(x) \rightarrow (Friend(x, Dean) \vee \neg Knows(x, Dean)))$$
    
6. **Everyone is a friend of someone:**  
    $$\forall x \, \exists y \, Friend(x, y)$$
    
7. **People only criticize people that are not their friends:**  
    $$\forall x, y \, (Person(x) \wedge Person(y) \wedge Criticizes(x, y) \rightarrow \neg Friend(x, y))$$
    
8. **Lucy criticized John:**  
    $$Criticizes(Lucy, John)$$

![[Pasted image 20250304235308.png]]

![[Pasted image 20250304235319.png]]

### 1. Identify the Task
- **Main Task**: Does the circuit add properly? (Circuit verification)

### 2. Assemble the Relevant Knowledge
- The circuit is composed of **wires** and **gates**. 
- Types of gates used:
  - **AND**
  - **OR**
  - **XOR**
  - **NOT**
- **Irrelevant** aspects for verification: Size, shape, color, cost of gates.

### 3. Decide on a Vocabulary
- **Gate(X1)**: A gate instance (e.g., XOR, AND).
- **Terminal(x)**: A terminal in the circuit.
- **Type(X1)**: The type of gate (e.g., XOR).
- **Circuit(C1)**: The overall circuit.
- **Signal(t)**: The signal value at terminal **t**.
- **In(1, X1)**: The first input terminal at gate **X1**.

### 4. Encode General Knowledge of the Domain
- **Connected Terminals**: If two terminals are connected, they have the same signal.
  $$
  ∀t1, t2 (Connected(t1, t2) → Signal(t1) = Signal(t2))
  $$
- The signal at any terminal is either 1 or 0:
  $$
  ∀t (Signal(t) = 1 ∨ Signal(t) = 0)
  $$
- **Bidirectional Connection**: If **t1** is connected to **t2**, then **t2** is connected to **t1**.
  $$
  ∀t1, t2 (Connected(t1, t2) → Connected(t2, t1))
  $$
- **OR Gate Behavior**: An OR gate outputs 1 if any of its inputs is 1.
  $$
  ∀g (Type(g) = OR → Signal(Out(1, g)) = 1 ⇔ ∃n Signal(In(n, g)) = 1)
  $$
- **AND Gate Behavior**: An AND gate outputs 0 if any of its inputs is 0.
  $$
  ∀g (Type(g) = AND → Signal(Out(1, g)) = 0 ⇔ ∃n Signal(In(n, g)) = 0)
  $$
- **XOR Gate Behavior**: An XOR gate outputs 1 if its inputs differ.
  $$
  ∀g (Type(g) = XOR → Signal(Out(1, g)) = 1 ⇔ Signal(In(1, g)) ≠ Signal(In(2, g)))
  $$
- **NOT Gate Behavior**: A NOT gate inverts its input.
  $$
  ∀g (Type(g) = NOT → Signal(Out(1, g)) ≠ Signal(In(1, g)))
  $$

### 5. Encode the Specific Problem Instance
- **Gate Types**:
  - **XOR**: `Type(X1) = XOR`, `Type(X2) = XOR`
  - **AND**: `Type(A1) = AND`, `Type(A2) = AND`
  - **OR**: `Type(O1) = OR`
- **Connections**:
  - `Connected(Out(1, X1), In(1, X2))`
  - `Connected(In(1, C1), In(1, X1))`
  - `Connected(Out(1, X1), In(2, A2))`
  - `Connected(In(1, C1), In(1, A1))`
  - `Connected(Out(1, A2), In(1, O1))`
  - `Connected(In(2, C1), In(2, X1))`
  - `Connected(Out(1, A1), In(2, O1))`
  - `Connected(In(2, C1), In(2, A1))`
  - `Connected(Out(1, X2), Out(1, C1))`
  - `Connected(In(3, C1), In(2, X2))`
  - `Connected(Out(1, O1), Out(2, C1))`
  - `Connected(In(3, C1), In(1, A2))`

### 6. Pose Queries to the Inference Procedure
- **Query**: What are the possible sets of values of all the terminals for the adder circuit?
  $$
  ∃i1, i2, i3, o1, o2 (Signal(In(1, C_1)) = i1 ∧ Signal(In(2, C1)) = i2 ∧ Signal(In(3, C1)) = i3 ∧ Signal(Out(1, C1)) = o1 ∧ Signal(Out(2, C1)) = o2)
  $$

### 7. Debug the Knowledge Base
- **Check for errors**: Ensure all connections, gates, and logic rules are correctly defined and ensure no contradictions in the problem instance.


### Inference in First-Order Logic

Inference in **First-Order Logic** is used to deduce new facts or sentences from existing sentences.

---

### Few Terminologies

#### Substitution
- **Substitution** replaces **variables** with **constants**.
- For example, if we write **F[a/x]**, it refers to substituting the constant "a" in place of the variable "x".
  
- **Examples**:
  - `SUBT({ X / 49 }, Perfect_Square(X)) → Perfect_Square(49)`
  - `SUBT({ X / 49, Y / 7 }, Divide(X, Y)) → Divide(49, 7)`

#### Equality
- **Equality** in **First-Order Logic (FOL)** doesn't only use predicates and terms for making atomic sentences but also uses the concept of equality.
- We can use **equality symbols** to specify that two terms refer to the **same object**.
  
- **Examples**:
  - `Brother(John) = Smith` (John and Smith are the same person).
  - `￢(x = y)` which is equivalent to `x ≠ y` (x is not equal to y).

### FOL Inference Rules for Quantifiers

In **First-Order Logic (FOL)**, we also have inference rules similar to propositional logic. Here are some basic inference rules:

---

#### 1. Universal Generalization (UG)
- **Universal Generalization** allows us to infer a universally quantified statement from a particular instance.
  
  **Example**:  
  If we know that **P(c)**: "A byte contains 8 bits,"  
  we can infer that **∀x P(x)**: "All bytes contain 8 bits."

---

#### 2. Universal Instantiation (UI) (Elimination)
- **Universal Instantiation** allows us to infer that a particular instance satisfies the universally quantified statement.

  **Example**:  
  Given **∀x P(x)**: "Every person likes ice cream," we can infer that **P(c)**: "John likes ice cream."

---

#### 3. Existential Instantiation (Elimination) - Only Once
- **Existential Instantiation** allows us to instantiate an existentially quantified statement by choosing a constant.
  
  **Example**:  
  If we have **∃x P(x)**: "There exists a person who likes ice cream," we can instantiate it with a specific person, say **P(a)**: "John likes ice cream."  
  This can only be done once for each existential statement.
![[Pasted image 20250304235956.png]]

---

#### 4. Existential Introduction
- **Existential Introduction** allows us to infer an existentially quantified statement based on a particular instance.
  
  **Example**:  
  If we know that **P(c)**: "John likes ice cream," we can infer **∃x P(x)**: "There exists someone who likes ice cream."
![[Pasted image 20250305000005.png]]


### Universal Generalization (UG)
- **Universal Generalization** is a valid inference rule that states if the premise **P(c)** is true for any arbitrary element **c** in the universe of discourse, then we can conclude **∀x P(x)**.  
- This rule is used when we want to show that every element has a similar property.

#### Example:
**Premise**: "All kings who are greedy are evil."  
**FOL**:  
$$∀x \, (king(x) ∧ greedy(x) → Evil(x))$$

- **Universal Instantiation (UI)**:  
If we instantiate for specific instances:
  - **King(John) ∧ Greedy(John) → Evil(John)**
  - **King(Richard) ∧ Greedy(Richard) → Evil(Richard)**
  - **King(Father(John)) ∧ Greedy(Father(John)) → Evil(Father(John))**

---

### Universal Instantiation (UI) (Elimination)
- **Universal Instantiation (UI)**, also known as universal elimination, is a valid inference rule in FOL.  
  - This rule can be applied multiple times to add new sentences to the knowledge base.
  - The new knowledge base is logically equivalent to the previous one.

- **How it works**:  
  - From **∀x P(x)**, we can infer any sentence **P(c)** by substituting a constant **c** for the variable **x**.

#### Example 3:  
**Premise**:  
$$∃x \, (Crown(x) ∧ OnHead(x, John))$$  

- We can infer:  
$$Crown(K) ∧ OnHead(K, John)$$  

  Where **K** is a new constant, also known as a **Skolem constant**.

- **Existential Instantiation** is a special case of the Skolemization process.

---

### Existential Instantiation (EI) (Elimination)
- **Existential Instantiation** (also called **Existential Elimination**) is a valid inference rule in FOL.
  - It can only be applied **once** to replace an existential sentence.
  - The new knowledge base is **not logically equivalent** to the old knowledge base, but it will be **satisfiable** if the old KB was satisfiable.

- **How it works**:  
  - From **∃x P(x)**, we infer **P(c)** where **c** is a new constant symbol.

#### Example 4:
**Premise**: "Priyanka got good marks in English."  
We can infer:  
"Someone got good marks in English."

---

### Existential Generalization (EG) (Introduction)
- **Existential Generalization** (also called **Existential Introduction**) is a valid inference rule in FOL.
  - It states that if there is some element **c** in the universe of discourse with a property **P**, then we can infer that **∃x P(x)**, meaning that "there exists something in the universe that has property P."

![[Pasted image 20250305000108.png]]

### Unification in First-Order Logic

**Unification** is the process of making two different logical atomic expressions identical by finding a substitution. It involves making expressions look identical via substitution, and unification depends on this substitution process.

- **Unification** takes two literals as input and makes them identical using substitution.

#### Example:
Given two expressions:  
$$ P(x, f(y)) $$  
$$ P(a, f(g(z))) $$  
We can unify them by applying the following substitutions:  
$$ x = a; \, y = g(z) $$  
Thus, the unification is represented as:  
$$ Unification[ a/x, g(z)/y ] $$

---

### Example: Find the MGU for Unify{King(x), King(John)}
1. Let:  
   $$ L1 = King(x), L2 = King(John) $$  
2. Substitution $$ θ = {John/x} $$ is a unifier for these atoms.
3. Applying the substitution results in both expressions becoming identical.

---

### Conditions for Unification
- **Predicate symbol**: The predicate symbols must be the same. If the atoms or expressions have different predicate symbols, they can never be unified.
- **Number of Arguments**: The number of arguments in both expressions must be identical.
- **Variables**: Unification will fail if there are two similar variables present in the same expression.

---

### Algorithm for Unification: `Unify(L1, L2)`

1. **Step 1**: If **L1** or **L2** is a variable or constant, then:
   - a) If **L1** or **L2** are identical, return NIL.
   - b) Else, if **L1** is a variable:
     - i. If **L1** occurs in **L2**, return FAILURE.
     - ii. Else, return { (L2 / L1) } (substitution).
   - c) Else, if **L2** is a variable:
     - i. If **L2** occurs in **L1**, return FAILURE.
     - ii. Else, return { (L1 / L2) }.
   - d) Else, return FAILURE.

2. **Step 2**: If the initial predicate symbols in **L1** and **L2** are not the same, return FAILURE.

3. **Step 3**: If **L1** and **L2** have a different number of arguments, return FAILURE.

4. **Step 4**: Set the substitution set **SUBST** to NIL.

5. **Step 5**: For **i = 1** to the number of elements in **L1**:
   - a) Call the **Unify** function with the **ith** element of **L1** and the **ith** element of **L2**, and put the result into **S**.
   - b) If **S** = failure, return FAILURE.
   - c) If **S ≠ NIL**, then:
     - i. Apply **S** to the remainder of both **L1** and **L2**.
     - ii. Append **S** to **SUBST**.

6. **Step 6**: Return **SUBST**.

---

### Example 4: Unify{prime(11), prime(y)}
- **L1** = prime(11), **L2** = prime(y)
  - Initial substitution:  
    $$ θ = {11/y} $$  
  - After substitution:  
    $$ {prime(11), prime(11)} $$  
  - The unification is successful.  
  - **Unifier**: $$ {11/y} $$

---

### Example 6: Unify{knows(Richard, x), knows(Richard, John)}
- **L1** = knows(Richard, x), **L2** = knows(Richard, John)
  - Initial substitution:  
    $$ θ = {John/x} $$  
  - After substitution:  
    $$ {knows(Richard, John), knows(Richard, John)} $$  
  - The unification is successful.  
  - **Unifier**: $$ {John/x} $$

### Resolution in First-Order Logic

**Resolution** is a theorem proving technique that proceeds by building refutation proofs, i.e., proofs by contradictions. It was invented by Mathematician John Alan Robinson in the year 1965.

- **Purpose**: Used to prove conclusions from given statements by deriving a contradiction.
- **Key Concept**: **Unification** is crucial in proofs by resolution.
- **Working**: Resolution operates on the **Conjunctive Normal Form (CNF)** or **Clausal Form**. For example,  
  $$ P \rightarrow Q $$ is logically equivalent to $$ \neg P \vee Q $$.
  - **Clause**: A disjunction of literals (an atomic sentence) is called a clause, and it is also known as a unit clause.

---

### The Resolution Inference Rule

The **resolution rule** for first-order logic is a lifted version of the propositional rule. It resolves two clauses if they contain complementary literals, and these literals are assumed to be standardized apart, so they share no variables.

- **Complementary literals**: Literals that are negations of each other.
  - For example: **l₁** = **P(x)** and **l₂** = **¬P(x)**.
- This rule is also known as the **binary resolution rule** because it resolves exactly two literals.

#### Example:
Given the two clauses:  
- Clause 1: $$ P(x) \vee Q(x) $$  
- Clause 2: $$ \neg P(x) \vee R(x) $$

The complementary literals **P(x)** and **¬P(x)** can be resolved, leading to:  
$$ Q(x) \vee R(x) $$

---

### Another Example

Consider two clauses:  
- Clause 1: $$ A \vee B $$  
- Clause 2: $$ \neg A \vee C $$

Since **A** and **¬A** are complementary literals, the resolution results in:  
$$ B \vee C $$

Thus, we have resolved the two clauses by applying the resolution rule.

![[Pasted image 20250305000247.png]]

### Another Example of Resolution

We can resolve the two clauses given below:

- Clause 1: $$ \text{Animal}(g(x)) \vee \text{Loves}(f(x), x) $$
- Clause 2: $$ \neg \text{Loves}(a, b) \vee \neg \text{Kills}(a, b) $$

Where the complementary literals are:
- $$ \text{Loves}(f(x), x) \text{ and } \neg \text{Loves}(a, b) $$

#### Resolution Process:

1. **Complementary Literals**: The literals **Loves(f(x), x)** and **¬Loves(a, b)** are complementary because **Loves** is negated in the second clause.

2. **Resolution**: After applying the resolution rule, we combine the remaining parts of the two clauses while removing the complementary literals.

   - Clause 1: $$ \text{Animal}(g(x)) \vee \text{Loves}(f(x), x) $$
   - Clause 2: $$ \neg \text{Loves}(a, b) \vee \neg \text{Kills}(a, b) $$

   After resolving **Loves(f(x), x)** and **¬Loves(a, b)**, the result is:

   - $$ \text{Animal}(g(x)) \vee \neg \text{Kills}(f(x), x) $$

Thus, the resolved clause is:

$$ \text{Animal}(g(x)) \vee \neg \text{Kills}(f(x), x) $$

This is the final result of resolving the two clauses.

### Steps for Resolution:

1. **Conversion of Facts into First-Order Logic (FOL)**:
   - Convert all given facts into FOL.

2. **Convert FOL Statements into Conjunctive Normal Form (CNF)**:
   - Express FOL statements as a conjunction of disjunctions (CNF).

3. **Negate the Statement to Prove (Proof by Contradiction)**:
   - Negate the goal and add it to the knowledge base for contradiction.

4. **Draw Resolution Graph (Unification)**:
   - Apply the resolution rule using unification to resolve complementary literals.

---

### Simple Example

**Given facts**:

- If it is sunny and warm, you will enjoy.
- If it is raining, you will get wet.
- It is a warm day.
- It is raining.
- It is sunny.

**Goal**: You will enjoy.

#### Step 1: Convert Facts to FOL:

- If it is sunny and warm, you will enjoy:  
  $$ \text{sunny}(x) \land \text{warm}(x) \rightarrow \text{enjoy}(x) $$

- If it is raining, you will get wet:  
  $$ \text{raining}(x) \rightarrow \text{wet}(x) $$

- It is a warm day:  
  $$ \text{warm}(today) $$

- It is raining:  
  $$ \text{raining}(today) $$

- It is sunny:  
  $$ \text{sunny}(today) $$

#### Step 2: Convert to CNF:

- $$ \neg \text{sunny}(x) \vee \neg \text{warm}(x) \vee \text{enjoy}(x) $$  
  (From the first fact)

- $$ \neg \text{raining}(x) \vee \text{wet}(x) $$  
  (From the second fact)

#### Step 3: Negate the Goal:

The goal is $$ \text{enjoy}(today) $$, so the negation will be:  
$$ \neg \text{enjoy}(today) $$

#### Step 4: Resolution Graph:

Now, we apply the resolution process step by step:

1. **Clause 1**: $$ \neg \text{sunny}(today) \vee \neg \text{warm}(today) \vee \text{enjoy}(today) $$  
2. **Clause 2**: $$ \neg \text{raining}(today) \vee \text{wet}(today) $$  
3. **Clause 3**: $$ \neg \text{enjoy}(today) $$  
4. **Clause 4**: $$ \text{sunny}(today) $$  
5. **Clause 5**: $$ \text{warm}(today) $$  

We resolve the clauses:

- From Clause 1 and Clause 4, we get:  
  $$ \neg \text{warm}(today) \vee \text{enjoy}(today) $$

- From Clause 3 and the result above, we get:  
  $$ \neg \text{warm}(today) $$

- From Clause 2 and Clause 5, we get:  
  $$ \neg \text{raining}(today) \vee \text{wet}(today) $$  

Thus, we have no contradictions, and the goal **"You will enjoy"** is confirmed.

---

### Example: Prove by Resolution

**Knowledge Base**:

- The humidity is high or the sky is cloudy.
- If the sky is cloudy, it will rain.
- If the humidity is high, it is hot.
- It is not hot.

**Goal**: It will rain.

#### Step 1: Convert to FOL:

- Let:
  - **P**: Humidity is high.
  - **Q**: Sky is cloudy.
  - **R**: It will rain.
  - **S**: It is hot.

- Represent as:
  - $$ P \vee Q $$  
  (The humidity is high or the sky is cloudy)
  - $$ Q \rightarrow R $$  
  (If the sky is cloudy, it will rain)
  - $$ P \rightarrow S $$  
  (If the humidity is high, it is hot)
  - $$ \neg S $$  
  (It is not hot)

#### Step 2: Convert to CNF:

- $$ P \vee Q $$  
  (From the first fact)

- $$ \neg Q \vee R $$  
  (From the second fact, converted to CNF)

- $$ \neg P \vee S $$  
  (From the third fact, converted to CNF)

- $$ \neg S $$  
  (From the fourth fact)

#### Step 3: Negate the Goal:

The goal is $$ R $$ (It will rain), so negate it:  
$$ \neg R $$

#### Step 4: Apply Resolution:

1. **Clause 1**: $$ P \vee Q $$  
2. **Clause 2**: $$ \neg Q \vee R $$  
3. **Clause 3**: $$ \neg P \vee S $$  
4. **Clause 4**: $$ \neg S $$  
5. **Clause 5**: $$ \neg R $$  

We apply resolution:

- From Clause 2 and Clause 5, resolve on **R**:  
  $$ \neg Q $$

- From Clause 1 and the result above, resolve on **Q**:  
  $$ P $$

- From Clause 3 and the result above, resolve on **P**:  
  $$ S $$

- From Clause 4 and the result above, resolve on **S**:  
  (Contradiction!)

The contradiction shows that the negation of the goal leads to an inconsistency, so the goal **"It will rain"** is true.

![[Pasted image 20250305000533.png]]

### Statement Derivation

The given statement about Divya's activities leads to the following derivable statements:

1. **Divya purchased a purse**.
2. **Last evening, Divya wasn’t home**.
3. **There’s a mall named City Mall**.
4. **City Mall was open last evening**.
5. **City Mall has at least one shop that sells purses**.
6. **There was a discount sale on purses**.
7. **Divya has at least one new dress**.
8. **Divya didn’t have a red purse before**.
9. **There was at least one woman at the mall last evening**.
10. **There was at least one woman named Divya at the mall last evening**.
11. **Divya doesn’t mind carrying a purse**.

These statements are derivable due to the richness of the knowledge base and assumptions we can make based on the given fact.

---

### Goal: Prove "Gita likes almond"

#### Given Facts:

1. $$ \forall x \: (food(x) \rightarrow likes(Gita, x)) $$  
   (Gita likes all kinds of food)

2. $$ food(Mango) \land food(chapati) $$  
   (Mango and chapati are food)

3. $$ eats(Gita, almonds) \land alive(Gita) $$  
   (Gita eats almonds and is alive)

4. $$ \forall x \forall y \: (eats(x, y) \land \neg killed(x) \rightarrow food(y)) $$  
   (Anything eaten by anyone and is still alive is food)

5. $$ \forall x \: (\neg killed(x) \rightarrow alive(x)) $$  
   (If someone is not killed, they are alive)

6. $$ \forall x \: (alive(x) \rightarrow \neg killed(x)) $$  
   (If someone is alive, they are not killed)

---

#### Convert Facts to CNF:

1. $$ \neg food(x) \vee likes(Gita, x) $$  
   (From Fact 1)

2. $$ food(Mango) \land food(chapati) $$  
   (From Fact 2)

3. $$ eats(Gita, almonds) \land alive(Gita) $$  
   (From Fact 3)

4. $$ \neg eats(x, y) \vee killed(x) \vee food(y) $$  
   (From Fact 4)

5. $$ \neg killed(x) \vee alive(x) $$  
   (From Fact 5)

6. $$ \neg alive(x) \vee \neg killed(x) $$  
   (From Fact 6)

---

#### Apply Resolution:

1. **Clause 1**: $$ \neg food(x) \vee likes(Gita, x) $$  
2. **Clause 2**: $$ food(Mango) $$  
3. **Clause 3**: $$ food(chapati) $$  
4. **Clause 4**: $$ eats(Gita, almonds) $$  
5. **Clause 5**: $$ alive(Gita) $$  

From Fact 4, applying resolution:

- **Clause 4** and **Clause 3**: Resolve on **food(y)** to get:
  $$ \neg eats(Gita, y) \vee killed(Gita) $$

By applying the assumption that Gita eats almonds, we infer that **almonds** is food based on the rules, which leads us to conclude that:

- **Gita likes almond**.

Thus, **Goal** is proven: **Gita likes almond**.

![[Pasted image 20250305000640.png]]
![[Pasted image 20250305000646.png]]
![[Pasted image 20250305000654.png]]
![[Pasted image 20250305000709.png]]

![[Pasted image 20250305000716.png]]
![[Pasted image 20250305000725.png]]
![[Pasted image 20250305000735.png]]
![[Pasted image 20250305000744.png]]
![[Pasted image 20250305000753.png]]

### Skolemization Process

In this step, we aim to eliminate the **existential quantifier (∃)** by using **Skolemization**. Skolemization involves replacing the existential quantifier with a specific function or constant. However, since the given problem does not contain any existential quantifiers, the statements will remain the same during this step.

#### Steps:

1. **Skolemization** typically applies when we have a statement of the form:
   $$ \exists x \: P(x) $$  
   This can be replaced by a function or constant like:
   $$ P(f(y)) $$  
   where **f(y)** is a Skolem function.

2. In our case, the statements provided do not have any existential quantifiers to eliminate. Therefore, no changes are made, and all statements will remain as they are.

![[Pasted image 20250305001340.png]]
![[Pasted image 20250305001347.png]]
![[Pasted image 20250305001357.png]]
![[Pasted image 20250305001407.png]]
![[Pasted image 20250305001417.png]]

### Knowledge Base and Proof

We need to prove that **Colonel West is a criminal** based on the given knowledge base. The proof will use **Resolution** and the **rules** provided in the knowledge base.

#### Given Knowledge Base:

1. **Crime Law**:
   $$ \forall x \: \forall y \: \forall z \: \left( \text{American}(x) \land \text{Weapon}(y) \land \text{Hostile}(z) \land \text{Sells}(x, y, z) \right) \rightarrow \text{Criminal}(x) $$

2. **Nono has some missiles**:
   $$ \exists x \: \left( \text{Owns}(Nono, x) \land \text{Missile}(x) \right) $$
   $$ \text{Owns}(Nono, M1) \land \text{Missile}(M1) $$

3. **All of Nono's missiles were sold to it by Colonel West**:
   $$ \forall x \: \left( \text{Missile}(x) \land \text{Owns}(Nono, x) \right) \rightarrow \text{Sells}(West, x, Nono) $$

4. **Missiles are weapons**:
   $$ \forall x \: \left( \text{Missile}(x) \rightarrow \text{Weapon}(x) \right) $$

5. **Enemies of America are hostile**:
   $$ \forall x \: \left( \text{Enemy}(x, America) \rightarrow \text{Hostile}(x) \right) $$

6. **Colonel West is American**:
   $$ \text{American}(West) $$

7. **Nono is an enemy of America**:
   $$ \text{Enemy}(Nono, America) $$

#### Goal:
We need to prove that Colonel West is a criminal. To do this, we need to show that:
$$ \neg \text{Criminal}(West) $$

This will be proven by showing that the conditions for being a criminal hold true for Colonel West.

---

### Step-by-Step Resolution:

#### Step 1: Convert the statements into Conjunctive Normal Form (CNF)
- **Crime Law**:
  $$ \neg \text{American}(x) \lor \neg \text{Weapon}(y) \lor \neg \text{Hostile}(z) \lor \neg \text{Sells}(x, y, z) \lor \text{Criminal}(x) $$

- **Missiles owned by Nono**:
  $$ \text{Owns}(Nono, M1) \land \text{Missile}(M1) $$

- **Missiles sold by Colonel West**:
  $$ \text{Missile}(M1) \land \text{Owns}(Nono, M1) \rightarrow \text{Sells}(West, M1, Nono) $$

  This can be rewritten as:
  $$ \neg \text{Missile}(M1) \lor \neg \text{Owns}(Nono, M1) \lor \text{Sells}(West, M1, Nono) $$

- **Missiles are weapons**:
  $$ \neg \text{Missile}(M1) \lor \text{Weapon}(M1) $$

- **Enemies of America are hostile**:
  $$ \neg \text{Enemy}(Nono, America) \lor \text{Hostile}(Nono) $$

- **Colonel West is American**:
  $$ \text{American}(West) $$

- **Nono is an enemy of America**:
  $$ \text{Enemy}(Nono, America) $$

#### Step 2: Apply Resolution
We apply **Resolution** to derive the conclusion.

1. **Step 1: Prove Hostility of Nono**  
   $$ \text{Enemy}(Nono, America) \rightarrow \text{Hostile}(Nono) $$  
   Using the statement "Nono is an enemy of America", we can conclude:
   $$ \text{Hostile}(Nono) $$

2. **Step 2: Prove Weaponization of Missiles**  
   $$ \text{Missile}(M1) \rightarrow \text{Weapon}(M1) $$  
   From the fact that Nono owns missiles, we have:
   $$ \text{Weapon}(M1) $$

3. **Step 3: Prove Criminality of Colonel West**  
   Now, apply the crime law:
   $$ \text{American}(West) \land \text{Weapon}(M1) \land \text{Hostile}(Nono) \land \text{Sells}(West, M1, Nono) \rightarrow \text{Criminal}(West) $$  
   Since we know Colonel West is American and Nono is hostile, we must check if West sold the missiles.

4. **Step 4: Prove Sale of Missiles**  
   From "Missiles sold by Colonel West", we get:
   $$ \text{Sells}(West, M1, Nono) $$

5. **Step 5: Conclusion**  
   Given all the facts, we can now conclude:
   $$ \text{Criminal}(West) $$

Thus, by applying the resolution process to the knowledge base, we have proven that Colonel West is indeed a criminal.

### Final Conclusion:
We have shown that Colonel West **is a criminal**, as all the conditions for the crime law hold true based on the provided knowledge base.

### Steps for Resolution:

To prove that **Colonel West is a criminal**, we will follow the steps of **Resolution** using the provided knowledge base.

1. Conversion of facts into first-order logic. 
2. Convert FOL statements into CNF 
3. Negate the statement which needs to prove (proof by contradiction) 
4. Draw resolution graph (unification).

![[Pasted image 20250305001657.png]]
![[Pasted image 20250305001703.png]]
![[Pasted image 20250305001711.png]]
![[Pasted image 20250305001720.png]]

### Forward Chaining and Backward Chaining Inference Engine

#### Inference Engine
An **Inference Engine** is a component of an intelligent system in **Artificial Intelligence (AI)** that applies logical rules to the knowledge base to infer new information from known facts. The **first inference engine** was part of the **expert system**.

The inference engine generally proceeds in two modes:
- **Forward Chaining**
- **Backward Chaining**

#### Forward Chaining

- **Forward Deduction / Forward Reasoning**:  
  A reasoning process that starts with **atomic sentences** (facts) in the knowledge base and applies inference rules (such as **Modus Ponens**) in the forward direction to extract more data until a goal is reached.

- **Process**:  
  - Starts from known facts.
  - Triggers all rules whose **premises** are satisfied.
  - Adds the **conclusion** of those rules to the known facts.
  - Repeats the process until the goal is achieved.

#### Properties of Forward-Chaining
- **Bottom-up Approach**:  
  The reasoning begins from known facts and works upwards to achieve the desired goal.

- **Data-driven**:  
  It’s a **data-driven** approach, meaning we use the available data to work our way toward the goal state.

- **Application**:  
  - Used in **expert systems** like **CLIPS** (C Language Integrated Production System), **business systems**, and **production rule systems**.

#### Example of Forward Chaining:
If you have the following facts:
- **Fact 1**: "It is sunny."
- **Fact 2**: "If it is sunny, you will enjoy."

Using forward chaining, we start from the facts and apply the rule to infer that:
- "You will enjoy" (because "It is sunny" triggers the rule).
![[Pasted image 20250305001757.png]]
![[Pasted image 20250305001805.png]]
![[Pasted image 20250305001812.png]]
![[Pasted image 20250305001819.png]]
![[Pasted image 20250305001828.png]]

### Problem Statement 

"As per the law, it is a crime for an American to sell weapons to hostile nations. Country A, an enemy of America, has some missiles, and all the missiles were sold to it by Robert, who is an American citizen." 

**Prove**: "Robert is a Criminal."

![[Pasted image 20250305001921.png]]
![[Pasted image 20250305001931.png]]
![[Pasted image 20250305001956.png]]
![[Pasted image 20250305002007.png]]
![[Pasted image 20250305002016.png]]
![[Pasted image 20250305002023.png]]
![[Pasted image 20250305002048.png]]
![[Pasted image 20250305002221.png]]

![[Pasted image 20250305002241.png]]
![[Pasted image 20250305002254.png]]
![[Pasted image 20250305002302.png]]
![[Pasted image 20250305002311.png]]
![[Pasted image 20250305002319.png]]

### **Backward Chaining Approach**

Backward-chaining is also known as a backward deduction or backward reasoning method when using an inference engine. A backward chaining algorithm is a form of reasoning, **which starts with the goal and works backward, chaining through rules to find known facts that support the goal.**

![[Pasted image 20250305002450.png]]
![[Pasted image 20250305002503.png]]
![[Pasted image 20250305002516.png]]
![[Pasted image 20250305002523.png]]
![[Pasted image 20250305002531.png]]
![[Pasted image 20250305002542.png]]
![[Pasted image 20250305002556.png]]
![[Pasted image 20250305002610.png]]

# May not be in ISE
### **Answer Set Programming (ASP) for Grocery Delivery System**

A **grocery delivery system** like **BigBasket** needs efficient **procurement and delivery plans** considering **uncertainties** like **supply chain disruptions, demand fluctuations, and workforce availability** during a lockdown. 

---

### **1. Problem Formulation in ASP**
- **Facts**: Represent known data (e.g., available goods, customer demands).
- **Rules**: Define dependencies and conditions (e.g., a delivery is possible only if stock is available).
- **Constraints**: Prevent infeasible solutions (e.g., a delivery cannot happen if no delivery staff is available).

---

### **2. Key Plans for Procurement and Delivery**

#### **A. Procurement Plans**
1. **Stock Forecasting**  
   - Use demand history to predict stock requirements.
   - Prioritize essentials like vegetables, dairy, and medicines.

2. **Supplier Coordination**  
   - Maintain multiple suppliers for redundancy.
   - Implement **dynamic supplier switching** in case of shortages.

3. **Warehouse Management**  
   - Optimize inventory placement for quick access.
   - Implement **FIFO (First-In-First-Out) strategy** to reduce waste.

4. **Emergency Restocking**  
   - Maintain buffer stock for high-demand items.
   - Enable quick procurement from **local markets if primary suppliers fail**.

---

#### **B. Delivery Plans**
1. **Time-Slot Based Deliveries**  
   - Customers book delivery slots to manage workload efficiently.
   - Prioritize early slots for **senior citizens and emergency requests**.

2. **Dynamic Route Optimization**  
   - Adjust delivery routes based on **real-time traffic and weather**.
   - Minimize delays using **AI-powered shortest path algorithms**.

3. **Workforce Scheduling**  
   - Assign delivery staff dynamically based on **availability and location**.
   - Implement **contactless deliveries** for safety.

4. **Alternative Delivery Methods**  
   - Use **drones or automated lockers** for high-risk areas.
   - Partner with **local stores** for hyper-local delivery.

---

### **3. Handling Uncertainties**
- **Supplier Delays** → Maintain **backup suppliers**.
- **High Demand Spikes** → Implement **rationing mechanisms**.
- **Workforce Shortages** → Utilize **temporary gig workers**.
- **Restricted Movement Regulations** → Seek **government permissions** for essential deliveries.

---

### **Conclusion**
Using **Answer Set Programming**, the **BigBasket delivery system** can model real-world uncertainties, generate **optimized delivery plans**, and ensure **efficient grocery distribution** even during lockdowns.

### **Uncertainty in AI and Probabilistic Reasoning**

Uncertainty is a fundamental challenge in AI where **facts and outcomes** are **not always deterministic**. 

---

### **1. Causes of Uncertainty**
- **Environmental factors**: (e.g., *Car breaks down, runs out of fuel*).
- **Random events**: (e.g., *Accidents on the bridge, plane leaves early*).
- **Lack of complete knowledge**: AI may lack full data to infer outcomes.
- **Noisy or ambiguous data**: Sensors and user inputs may be **imprecise**.

---

### **2. Limitations of Traditional Logic**
- **First-order logic (FOL)** and **Propositional logic** assume certainty:
  - Example: \( A \rightarrow B \) (If A is true, then B is true).
  - **Problem**: If A is uncertain, we **cannot infer** B.

- **Real-world example**:
  - "If it is raining, then the road is wet."
  - But if we **do not know** whether it is raining, we **cannot infer** the road's state.

- **Solution**: Use **Uncertain Reasoning / Probabilistic Reasoning**.

---

### **3. Probabilistic Reasoning**
- **Represents knowledge with degrees of certainty**.
- Instead of binary true/false, we use **probability values**.
- **Example:**
  - "There is an 80% chance that the plane leaves early."
  - "There is a 60% chance of a car breakdown."

---

### **4. Approaches to Handling Uncertainty**
#### **A. Probability Theory**
- **Bayesian Networks**: Model dependencies between variables.
- **Markov Models**: Predict future states based on past data.
- **Hidden Markov Models (HMMs)**: Used for speech recognition, weather for

### **Causes of Uncertainty in AI**
Uncertainty arises due to various real-world factors, making AI systems **less deterministic**. 

---

### **1. Leading Causes of Uncertainty**
- **Unreliable Sources**: Data obtained from **inaccurate or biased** sources.
- **Experimental Errors**: Mistakes in **data collection and analysis**.
- **Equipment Faults**: Sensor failures, hardware malfunctions.
- **Temperature Variation**: Impacts precision in **physical measurements**.
- **Climate Change**: Environmental instability affects predictions.

---

### **2. Reasons That Summarize Uncertainty**
#### **A. Laziness**
- **Defining complete rules is impractical**.
- **Example**: Instead of listing every condition affecting a patient’s health, **approximate models** are used.

#### **B. Theoretical Ignorance**
- **Lack of a complete understanding** of certain domains.
- **Example**: **Medical science** does not fully explain every disease mechanism.

#### **C. Practical Ignorance**
- **Even with complete rules, exact data may be missing**.
- **Example**: A **doctor diagnoses** a patient without all test results.

#### **D. Real-World Scenarios**
- **Weather Prediction**: "It **may** rain today."
- **Human Behavior**: "A person’s **reaction** to an event."
- **Sports Outcomes**: "Who will win a **match** between two teams?"

---

### **3. Need for Probabilistic Reasoning in AI**
- **When outcomes are unpredictable**.
- **When handling large predicate possibilities**.
- **When unknown errors occur in experiments**.

---

### **4. Methods of Probabilistic Reasoning**
#### **A. Bayes' Rule**
- Used to **update probabilities** based on **new evidence**.
- **Formula**:  
  
 $$ P(A|B) = \frac{P(B|A) P(A)}{P(B)} $$
  
- **Example**: Medical Diagnosis  
  - Given **symptom B**, calculate the **probability of disease A**.

#### **B. Bayesian Statistics**
- **Extends Bayes’ rule** for complex real-world predictions.
- Used in **AI, medical science, and finance**.

---

### **Conclusion**
Uncertainty is **unavoidable** in AI. Probabilistic reasoning methods **help infer conclusions** in **complex and uncertain environments**.

### **Probability in AI**
Probability represents **the likelihood of an uncertain event occurring**, expressed numerically between **0 and 1**.

---

### **1. Properties of Probability**
- **0 ≤ P(A) ≤ 1** → The probability of event **A** lies between **0 and 1**.
- **P(A) = 0** → Event **A is impossible**.
- **P(A) = 1** → Event **A is certain**.

![[Pasted image 20250305003239.png]]
---

### **2. Conditional Probability**
- Represents **the probability of event A occurring given that event B has already occurred**.
- **Formula**:  
  
  $$P(A | B) = \frac{P(A \cap B)}{P(B)} $$
 
  where:
  - **P(A ∩ B)** = Joint probability of A and B.
  - **P(B)** = Probability of event B (Marginal probability).

• If the probability of A is given and we need to find the probability of B,

$$P(B | A) = \frac{P(A \cap B)}{P(A)} $$


### **3. Example Problem**
#### **Problem Statement**
- **70%** of students like **English** (**P(B) = 0.7**).
- **40%** like **both English and Mathematics** (**P(A ∩ B) = 0.4**).
- Find **P(A | B)** → The probability that a student who likes English also likes Mathematics.

#### **Solution**
Using the **conditional probability formula**:

$$P(A | B) = \frac{P(A \cap B)}{P(B)}$$

![[Pasted image 20250305003414.png]]

Thus, **57% of students who like English also like Mathematics**.

---

### **4. Applications in AI**
- **Speech Recognition**: Given a sound, predict the **most likely word**.
- **Spam Detection**: Given **certain words**, predict whether **an email is spam**.
- **Medical Diagnosis**: Given **symptoms**, predict the **likelihood of a disease**.

---
### **Conclusion**
Probability, especially **conditional probability**, plays a crucial role in AI by **handling uncertainties** and **making data-driven predictions**.

