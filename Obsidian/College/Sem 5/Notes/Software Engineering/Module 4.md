## 4.1 Packages and interfaces: Distinguishing between classes/interfaces, Exposing class and package interfaces


## 4.2 Mapping model to code , Mapping Object Model to Database Schema

### Mapping Models to Code

#### Transformation Objectives
- A **transformation** aims to enhance a specific aspect of the model (e.g., **modularity**) while preserving other attributes (e.g., **functionality**).

### Transformation Activities

1. **Optimization**:
   - Focuses on enhancing the **performance** of the system model.
   - **Examples**:
     - **Reducing multiplicities** to simplify relations.
     - **Adding redundant associations** to improve efficiency.
     - **Adding derived attributes** to speed up object access.

2. **Realizing Associations**:
   - Maps associations in the model to specific **code constructs**.
   - **Example**: Using **references** or **collections** for representing associations in code.

3. **Mapping Contracts to Exceptions**:
   - Describes the behavior of operations when **contracts** are broken.
   - Includes **raising exceptions** upon detecting violations.

4. **Mapping Class Models to a Storage Schema**:
   - Chooses a **persistent storage strategy** (e.g., DBMS, flat files).
   - Maps the class model to a **storage schema**, like a **relational database**.

### Types of Transformations

1. **Model Transformations**:
   - Applied to an **object model**, resulting in a transformed model.
   - Helps the model comply with all requirements, potentially **adding, removing, or renaming** classes, operations, and attributes.

![[Pasted image 20241117011748.png]]

2. **Refactoring**:
   - Improves the **readability** and **modifiability** of source code without altering system behavior.
   - Performed in **small incremental steps** with testing.
   - **Examples**:

- **Pull Up Field**: Moves a common field (e.g., `email`) from subclasses to a superclass.

![[Pasted image 20241117012409.png]]
![[Pasted image 20241117012339.png]]
   
- **Pull Up Constructor Body**: Moves initialization code from subclasses to a superclass.

![[Pasted image 20241117012421.png]]
![[Pasted image 20241117012344.png]]

- **Pull Up Method**: Moves methods manipulating a field from subclasses to a superclass.
![[Pasted image 20241117012514.png]]
![[Pasted image 20241117012517.png]]

3. **Forward Engineering**:
   - Generates **source code** from model elements, such as class declarations or database schemas.
   - Maintains a close **correspondence** between the design model and the source code to minimize errors.

![[Pasted image 20241117012736.png]]

4. **Reverse Engineering**:
   - Recreates a model from existing **source code**, useful when the model is lost or out of sync.
   - Acts as an **inverse** of forward engineering.

### Transformation Principles
1. **Single Criterion**: Each transformation should address a specific aspect (e.g., performance).
2. **Local Changes**: The transformation should modify only a few elements at a time.
3. **Isolation**: Each transformation must be applied separately from others.
4. **Validation**: Every transformation must be followed by a validation step to verify its correctness.

### Mapping Associations to Code

1. **Unidirectional One-to-One Associations**: Implemented using a single reference in one class.

![[Pasted image 20241117012759.png]]

2. **Bidirectional One-to-One Associations**: Represented by references in both associated classes.

![[Pasted image 20241117012812.png]]

3. **One-to-Many Associations**: Implemented using collections in the "one" class.

![[Pasted image 20241117012823.png]]


4. **Many-to-Many Associations**: Managed using collections in both classes, often with a linking class.

![[Pasted image 20241117012832.png]]

### Mapping Contracts to Exceptions

1. **Checking Preconditions**:
   - Verified at the start of the method.
   - Raises exceptions if conditions are not met.

2. **Checking Postconditions**:
   - Verified at the end of the method.
   - Ensures the expected state is achieved, raising exceptions if violated.

3. **Checking Invariants**:
   - Validates consistency across multiple method executions, typically alongside postconditions.

4. **Handling Inheritance**:
   - Encapsulates precondition and postcondition checks into separate methods for easy inheritance handling.

### Challenges with Checking Contracts

1. **Coding Effort**:
   - The code for checking conditions can be more complex than the primary implementation logic.

2. **Increased Opportunities for Defects**:
   - The checking code itself may introduce bugs, increasing the need for testing.

3. **Performance Drawbacks**:
   - Systematically checking all contracts can **slow down** the code, potentially affecting response time and throughput goals.

![[Pasted image 20241117012942.png]]
![[Pasted image 20241117012948.png]]
## 4.3 Component and deployment diagrams: Describing Dependencies

### Component Diagram

- **Definition**:
  - A **Component Diagram** displays the components, provided and required interfaces, ports, and their relationships.
  - It **does not describe system functionality** but outlines the components used to implement those functionalities.
  - It can be viewed as a **static implementation** representation of a system.

#### Purpose
- The main purpose of a Component Diagram is to **show the structural relationships** between the components of a system.

#### Key Concepts
1. **Assembly Connector**:
   - Bridges a component’s **required interface** (e.g., Component 1) with the **provided interface** of another component (e.g., Component 2).
   - Allows one component to **provide services** required by another component.
![[Pasted image 20241117010636.png]]

2. **Port**:
   - Represented by a **square** along the edge of a system or component.
   - Ports help **expose required and provided interfaces** of a component, enabling interaction between components.
![[Pasted image 20241117010526.png]]

3. **Inner Structure**:
   - A component's **inner structure** may be composed of other sub-components.
![[Pasted image 20241117010536.png]]
#### Example
- **Online Shopping UML Component Diagram**:
  - An example of a component diagram for an online shopping system includes three related subsystems:
    - **WebStore**
    - **Warehouses**
    - **Accounting**

![[Pasted image 20241117010657.png]]

### Deployment Diagram

- **Definition**:
  - A **Deployment Diagram** shows the allocation of artifacts to nodes in the physical design of a system.
  - It consists of a graph of nodes connected by communication associations to represent the **physical configuration** of software and hardware.

#### Essential Elements of a Deployment Diagram

1. **Artifacts**:
   - An **artifact** is a physical item that implements a part of the software design.
   - It can be a **source file**, document, or any other item related to the code.
   - **Notation**: Represented by a class rectangle with the name of the artifact and the label `<<artifact>>`.

2. **Nodes**:
   - A **node** is a computational resource containing **memory and processing** capabilities, where artifacts are deployed for execution.
   - **Notation**: Represented by a three-dimensional cube.
   - Nodes represent **hardware entities**, not software components.

3. **Connections**:
   - Nodes communicate via **messages and signals** through a **communication path** indicated by a solid line.
   - Communication paths are usually **bidirectional**; for unidirectional paths, an arrow may be added to indicate the direction.
   - Each communication path can have an optional **keyword label** (e.g., `«http»`, `«TCP/IP»`) that provides information about the connection.
   - **Multiplicity** may be specified for each node connected via a communication path, indicating the number of instances involved.

![[Pasted image 20241117011204.png]]
![[Pasted image 20241117011208.png]]
![[Pasted image 20241117011213.png]]



## 4.4 Managing and controlling Changes, Managing and controlling version

### Version Control

- **Version control** combines procedures and tools to manage different versions of configuration objects created during the software process.
- A **version control system** provides four major capabilities:
  1. **Project Database**: Stores all relevant configuration objects.
  2. **Version Management**: Stores all versions of a configuration object.
  3. **Make Facility**: Enables the construction of a specific version of the software.
  4. **Version and Change Control**: Often includes an **issue tracking** (or **bug tracking**) capability.

#### Change Sets in Version Control
- Many version control systems establish a **change set**:
  - A change set is a collection of all changes required to create a specific version of the software.
  - **Named change sets** can be identified for an application or system.
  - To construct a specific version of the software, specify the relevant change sets (by name).

#### Modeling Approach for Building New Versions
- The approach for creating new software versions includes:
  1. **Template for Building Versions**: Defines the structure and components needed.
  2. **Construction Rules**: Guidelines for assembling the version.
  3. **Verification Rules**: Criteria to verify the correctness of the version.

### Change Control

- **Too Much Change Control**:
  - Excessive change control can create bottlenecks and issues.
  - In large software projects, **uncontrolled change** can quickly lead to chaos.
- For large projects, change control uses a combination of **human procedures** and **automated tools** to manage changes effectively.

#### Key Elements of Change Control
1. **Engineering Change Order (ECO)**:
   - A formal document that defines the requested changes and tracks their implementation.

2. **Access Control**:
   - Governs which software engineers have the **authority** to access and modify specific configuration objects.

3. **Synchronization Control**:
   - Ensures that **parallel changes** made by different team members do not **overwrite** one another.

#### Types of Change Control
- **Informal Change Control**:
  - The developer makes changes directly within the project without needing prior approval.

- **Project-Level Change Control**:
  - The developer must get **approval** from the project manager before making any changes.

- **Formal Change Control**:
  - Instituted when the software product is **released** to customers, requiring strict adherence to change management procedures.
  
![[Pasted image 20241117010103.png]]




## 4.5 Categories of Risks, Nature Of Risk, Types of Risk, Risk Identification, Risk Assessment, Risk planning and control, Risk management, Evaluating risk to schedule, PERT technique.