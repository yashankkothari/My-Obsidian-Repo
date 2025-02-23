## 5.1 Testing Concepts: Purpose of Software Testing, Testing Principles, Goals of Testing, Testing aspects: Requirements, Test Scenarios, Test cases, Test scripts/procedures

### Purpose of Software Testing
- **Identify Discrepancies**: Testing analyzes a system to detect differences between required and observed behavior.
- **Planned & Systematic Approach**: Testing activities can be pre-planned and conducted methodically.

### Principles of Testing

1. **Traceability to Requirements**  
   - Tests should be linked to customer requirements.
   - Testing **detects errors** but does not guarantee an error-free system.

2. **Exhaustive Testing is Impossible**  
   - Testing all possible input combinations is impractical.
   - Focus on **spot tests** and manage efforts effectively.

3. **Plan Tests Early**  
   - Testing strategies should be developed early in the software lifecycle.

4. **Early and Regular Testing**  
   - Early detection of errors simplifies correction.

5. **Error Accumulation**  
   - Errors tend to cluster; finding one error may indicate more in the same area.
   - Testing must adapt to this behavior.

6. **Fading Effectiveness**  
   - Repeated test cases may lose effectiveness over time.
   - Regularly update and revise test cases to discover new errors.

7. **Context-Dependent Testing**  
   - Each system is unique and requires tailored testing approaches.

8. **False Conclusion of No Errors**  
   - Finding no errors does not mean the system is usable or meets user expectations.
   - User involvement and prototyping are crucial.

9. **Pareto Principle**  
   - Often, 80% of defects are found in 20% of the code.
   - roughly 80% of consequences come from 20% of causes

10. **Testing from Small to Large**  
    - Begin with **unit testing** and progressively move to system-level testing.

11. **Independent Testing**  
    - To avoid bias, testing should ideally be performed by an **independent third party**.

### Goals of Testing

1. **Validation Testing**  
   - **Objective**: Show that the software meets its requirements for both developer and customer.
   - **Approach**: Use test cases reflecting expected system behavior to ensure correct functionality.

2. **Defect Testing (Verification)**  
   - **Objective**: Identify incorrect, undesirable, or non-conforming behavior in the software.
   - **Approach**: Design test cases specifically to uncover defects.

### Testing Concepts

- **Test Component**: A part of the system isolated for testing.
- **Fault (Bug/Defect)**: A design or coding mistake causing abnormal component behavior.
- **Erroneous State**: An indication of a fault during system execution.
- **Failure**: A deviation between expected and actual behavior triggered by erroneous states.

### Requirements of Testing

1. **Testability**  
   - **Definition**: Ease with which a software program can be tested.
   - **Metrics**: Quantifiable measures used to assess testability.

2. **Operability**  
   - **Definition**: The better a system functions, the more efficiently it can be tested.
   - **Insight**: Fewer bugs mean less overhead for analysis and reporting.

3. **Observability**  
   - **Principle**: "What you see is what you test."
   - **Key Points**:
     - Distinct outputs are generated for each input.
     - System states and variables are visible during execution.
     - Logs or transaction histories provide visibility into past states.
     - Incorrect outputs are easily identified.
     - Self-testing mechanisms detect and report internal errors.

4. **Controllability**  
   - **Principle**: "Better control allows for more effective and automated testing."
   - **Key Points**:
     - Possible outputs are generated through input combinations.
     - Code is executable for various inputs.
     - Test engineers can directly control software and hardware states.
     - Consistent and structured input/output formats facilitate automation.

5. **Decomposability**  
   - **Principle**: "Isolating testing scopes allows quicker identification and retesting of problems."
   - **Key Points**:
     - The system is modularized.
     - Independent testing of software modules is possible.

6. **Simplicity**  
   - **Principle**: "Less complexity leads to faster testing."
   - **Key Points**:
     - Functional simplicity (minimum necessary features).
     - Structural simplicity (modular architecture).
     - Code simplicity (adherence to coding standards).

7. **Stability**  
   - **Principle**: "Fewer changes result in fewer disruptions to testing."
   - **Key Points**:
     - Software changes are infrequent and controlled.
     - Existing tests remain valid after changes.
     - The software recovers well from failures.

8. **Understandability**  
   - **Principle**: "Better understanding leads to smarter testing."
   - **Key Points**:
     - Clear understanding of design and dependencies.
     - Changes are well-communicated.
     - Accessible, organized, detailed, and accurate technical documentation.

### Test Case

A **test case** is a set of conditions or variables under which a tester determines if the system under test satisfies requirements or works correctly. The process of developing test cases also helps identify issues in the application's requirements or design.

### Attributes of a Test Case

1. **Name**  
   - **Purpose**: Distinguishes between different test cases.
   - **Example**: For testing a use case like `Deposit()`, the test case name could be `Test_Deposit`.

2. **Location**  
   - **Purpose**: Describes where the test case can be found.
   - **Details**: Can include the path name or URL to the test program and its inputs.

3. **Input (Data)**  
   - **Purpose**: Defines the set of input data or commands entered by the tester.
   - **Details**: Includes test data or links to data used while conducting the test.

4. **Expected Behavior (Oracle)**  
   - **Purpose**: Describes the expected outcome for the test case.
   - **Details**: This attribute ensures that the system's behavior aligns with the expected results.

5. **Log**  
   - **Purpose**: A set of time-stamped correlations between the observed behavior and the expected behavior during various test runs.
   - **Details**: The log helps track the results of the test case execution.

## 5.2 Strategies for Software Testing, Testing Activities: Planning Verification and Validation, Software Inspections, FTR

### Strategies for Software Testing

Software testing is a set of activities that can be planned in advance and conducted systematically. A number of software testing strategies provide software developers with a template for testing and have the following generic characteristics:

1. **Testing Begins at the Component Level and Works Outward Toward Integration**  
   Testing starts with the individual components and progresses outward toward the integration of the entire computer-based system. This allows for more focused and isolated testing at the early stages.

2. **Different Testing Techniques Are Appropriate at Different Points in Time**  
   Various testing techniques are suitable at different stages of the software development lifecycle. Early phases may require unit testing, while later stages may need integration or system testing.

3. **Testing Is Conducted by the Developer or an Independent Test Group**  
   For smaller projects, testing is typically conducted by the software developer. However, for larger projects, an independent test group is employed to ensure objectivity and comprehensive test coverage.

4. **Testing and Debugging Are Different Activities but Should Be Accommodated Together**  
   While testing is designed to find errors, debugging aims to fix those errors. Although these are distinct activities, the testing strategy must allow for debugging as part of the overall process to correct issues found during testing.

5. **A Testing Strategy Must Include Both Low-Level and High-Level Tests**  
   A comprehensive testing strategy should cater to both low-level tests, which focus on individual components, and high-level tests, which verify the functioning of integrated systems or software applications.

6. **A Strategy Must Provide Guidance for Practitioners and Milestones for Managers**  
   The testing strategy should offer clear instructions for practitioners on how to execute tests and meet specific testing objectives. Additionally, it should include milestone markers for managers to track the progress of the testing process.

---

### Strategic Issues to Consider

1. **Specify Product Requirements in a Quantifiable Manner Before Testing Commences**  
   It is essential to specify product requirements clearly and quantifiably long before testing begins. This will help avoid ambiguity during the testing phase and will assist in determining measurable testing objectives.  
   - **Objective of Testing**: The primary goal of testing is to find errors, but it also aims to assess other important quality characteristics of the product.

2. **State Testing Objectives Explicitly**  
   Specific objectives of testing should be clearly stated in measurable terms. This includes:
   - **Test Effectiveness**: How well the test identifies defects.
   - **Test Coverage**: The extent to which the software is tested.
   - **Defect Cost**: The cost to find and fix defects.
   - **Frequency of Occurrence**: How often defects are found.
   - **Work Hours**: The number of hours spent on testing.

3. **Understand the Users of the Software and Develop a Profile for Each User Category**  
   A thorough understanding of the users and their needs helps in creating use cases that describe the interactions each user will have with the system. This enables the testing process to focus on actual use cases, making it more relevant and efficient by reducing unnecessary testing effort.

4. **Develop a Testing Plan that Emphasizes Rapid Cycle Testing**  
   Rapid cycle testing emphasizes quick feedback and shorter test iterations, allowing for more timely identification of defects. The goal is to perform testing in a more efficient, cost-effective manner while achieving the best possible results.  
   - The feedback generated from rapid cycles can be used to control quality levels and adjust the testing strategies accordingly.

5. **Build Robust Software That Is Designed to Test Itself**  
   Software should be designed to identify and diagnose specific errors automatically. This reduces the need for manual intervention during testing and helps ensure a higher quality product.  
   - The design should accommodate automated testing, regression testing, and the ability to test core functions.

6. **Use Effective Technical Reviews as a Filter Prior to Testing**  
   Technical reviews are an excellent way to uncover errors early in the development process, often preventing the need for extensive testing later. By identifying and addressing issues early, reviews can reduce the overall effort required for testing.  
   - Reviews can also help catch errors that automated tests or manual testing might overlook.

7. **Develop a Continuous Improvement Approach for the Testing Process**  
   The testing process should be measured and tracked to ensure that it continues to improve over time. Metrics collected during testing should be used as part of a statistical process control approach, which helps improve the quality of both the testing and the software being tested.

---

### Verification and Validation

**Verification** refers to the activities that ensure the software correctly implements a specific function or algorithm. It ensures that the software is built according to the design specifications.  
**Validation**, on the other hand, refers to activities that ensure the software meets customer requirements and is traceable to those requirements. Validation checks if the right product is being built.

These two processes encompass a wide array of Software Quality Assurance (SQA) activities, such as:
- Formal technical reviews
- Quality and configuration audits
- Performance monitoring
- Feasibility studies
- Documentation and algorithm reviews
- Development, qualification, and installation testing

Verification and validation principles help define quality assurance standards and error detection mechanisms in the software development process.

---

### Formal Technical Reviews (FTR)

**Formal Technical Review (FTR)** is a software quality control activity performed by software engineers (and others) to ensure quality in the software development process. The objectives of FTRs include:

1. **Uncovering Errors**: Identify errors in function, logic, or implementation in any representation of the software.
2. **Verifying Requirements**: Ensure the software meets its specified requirements.
3. **Compliance with Standards**: Ensure the software adheres to predefined standards.
4. **Uniform Development**: Achieve consistent software development across the team.
5. **Making Projects Manageable**: Increase the manageability of projects by having a structured review process.

The FTR process involves a series of review types, including walkthroughs and inspections, and is typically conducted as a meeting with all involved parties present. Proper planning and control are essential for successful reviews.

---

### Conducting FTR

- **The Review Meeting**: Typically involves 3-5 people, including the review leader, all reviewers, and the producer. Preparation should take no more than two hours per person, and the meeting duration should be under two hours.

- **Roles and Responsibilities**: During the review, one person will act as the recorder, taking notes on issues and findings. The producer presents the material for review, and the team discusses potential issues.

---

### Review Reporting and Record Keeping

- **Recording Issues**: During the FTR, the recorder documents all raised issues, which are then listed in the review report. The report includes:
  - What was reviewed
  - Who reviewed it
  - Findings and conclusions

- **Follow-up Actions**: At the end of the review, the attendees must decide whether to accept the product without modification, reject it due to severe errors, or accept it with minor revisions.

---

### FTR Guidelines

1. **Review the Product, Not the Producer**: The focus of the review should be on the product, not the individual who developed it.
2. **Set an Agenda and Maintain It**: The review should stay on schedule, with a clear agenda.
3. **Limit Debate and Rebuttal**: When issues are raised, there should not be extended debates or rebuttals; instead, focus on the issue at hand.
4. **Enunciate Problem Areas, Don’t Solve All Problems**: Reviews should identify issues but not attempt to solve every problem within the session.
5. **Take Written Notes**: The recorder should take detailed notes, often on a wallboard, to ensure that priorities and wording can be reviewed by other team members.
6. **Limit the Number of Participants**: Keep the number of people involved to a necessary minimum for efficient review.
7. **Develop a Checklist for Each Product**: A checklist helps structure the review and ensures that all important issues are covered.
8. **Allocate Resources and Schedule Time for FTRs**: Reviews should be planned as part of the software process and not treated as last-minute tasks.
9. **Provide Training for All Reviewers**: Ensure that all reviewers are properly trained to contribute effectively to the review process.

## 5.3 Levels of Testing : unit testing, integration testing, regression testing, product testing, acceptance testing and White-Box Testing

### Levels of Testing (Unit Testing)

#### 1. Unit Testing
- **Unit Testing** tests individual components of a software application.
- Focuses on **functional correctness** of standalone modules.
- Tests important **control paths** to uncover errors within the module's boundary.

![[Pasted image 20241117170432.png]]
![[Pasted image 20241117170441.png]]

#### 2. Scope and Focus
- **Limited scope**: Errors uncovered are constrained by the unit's scope.
- Focuses on **internal processing logic** and **data structures**.
- Can be conducted **in parallel** for multiple components.

#### 3. Key Tests in Unit Testing
- Tests the **module interface** to ensure correct data flow.
- **Independent paths** through the control structure are tested to ensure execution of all statements.
- **Boundary conditions** are tested to restrict or limit processing.
- All **error-handling paths** are tested.

#### 4. Data Flow Testing
- **Data flow** across component interfaces is tested first.
- Test cases designed to uncover errors in **computation**, **comparison**, and **data flow**.
- **Boundary testing** is critical for identifying errors at maximum or minimum values.

#### 5. Drivers and Stubs
- **Drivers** simulate high-level modules during testing.
![[Pasted image 20241117170515.png]]
- **Stubs** simulate low-level modules during testing.
![[Pasted image 20241117170532.png]]

- Both **drivers** and **stubs** represent testing overhead and are not included in the final product.
- Unit testing is simplified by designing components with **high cohesion**.

---

### Levels of Testing (Integration Testing)

#### 1. Purpose
- Integration testing aims to uncover errors in the interaction between modules.
- **Data loss** can occur across interfaces.
- A **component's failure** can negatively affect others.
- Sub-functions may not produce the desired outcome when combined.
- Global data structures can cause issues during integration.

#### 2. Incremental Integration
- **Incremental integration** builds and tests the program in small parts, simplifying error isolation.
- More complete testing of **interfaces**.
- **Top-down** and **bottom-up** integration strategies.

#### 3. Top-Down Integration
- **Top-Down** integration tests from the top level, progressively adding lower-level units.
- **Depth-first integration**: Integrates components along major control paths.
- **Breadth-first integration**: Integrates components across the structure horizontally.
![[Pasted image 20241117170547.png]]
#### 4. Steps in Top-Down Integration
1. Main control module is used as a **test driver**; stubs replace subordinate components.
2. **Subordinate stubs** are replaced with actual components incrementally.
3. Tests are conducted for each integrated component.
4. **Regression testing** ensures no new errors are introduced.

#### 5. Bottom-Up Integration
- **Bottom-Up** integration tests lower-level units first, progressively adding upper-level units.
- No need for **stubs** since lower-level components are tested first.
- The program is complete only when the last module is integrated.
![[Pasted image 20241117170552.png]]
#### 6. Steps in Bottom-Up Integration
1. Low-level components are grouped into **clusters** for testing.
2. A **driver** coordinates test case input and output.
3. The cluster is tested.
4. Drivers are removed, and clusters are combined upward.

---

### Levels of Testing (Regression Testing)

#### 1. Purpose
- Ensures changes (enhancements or fixes) do not negatively affect the software.
- **New data flow paths**, **I/O**, or **control logic** may introduce issues.

#### 2. Process
- Re-execution of previously conducted tests to check for unintended side effects.
- Identifies if **error corrections** introduce new errors.

#### 3. Regression Test Suite
- Contains three types of test cases:
  1. Representative tests covering all software functions.
  2. Tests focusing on functions likely affected by changes.
  3. Tests targeting the components that have been changed.

#### 4. Conducting Regression Testing
- Regression testing can be manual or automated using **playback capture tools**.

---

### Levels of Testing (Acceptance Testing)

#### 1. Purpose
- Verifies that the software meets **requirement specifications**.
- Evaluates if the system meets **business requirements** for delivery to end users.

#### 2. Types of Acceptance Tests
- **Benchmark tests** simulate typical operating conditions.
- **Competitor testing** compares the new system with an existing one.
- **Shadow testing** compares the new system's output to the legacy system's output.

#### 3. After Acceptance Testing
- The client reports unmet requirements.
- **Dialog between developers and clients** may lead to changes, initiating another iteration of the software life-cycle.

---

### Levels of Testing (White Box Testing)

#### 1. Overview
- **White Box Testing** (also called Clear Box, Glass Box, or Code-Based Testing) involves testing with knowledge of the system's **internal structure/design**.

#### 2. White Box Testing Goals
- Derive test cases to:
  1. Exercise all **independent paths** in a module.
  2. Test all **logical decisions** for both true and false outcomes.
  3. Execute all **loops** at boundaries and within operational limits.
  4. Validate internal **data structures**.

#### 3. Basis Path Testing
- A technique for testing based on **complexities**, **execution paths**, and **procedural design**.
- Ensures all program statements are executed.

#### 4. Flow Graph Notation
- **Flow graph nodes** represent procedural statements.
- **Edges** represent control flow, similar to flowchart arrows.
- **Regions** bounded by edges and nodes; **predicate nodes** contain conditions.
- **Cyclomatic complexity** measures logical complexity using flow graphs.
![[Pasted image 20241117170606.png]]
#### 5. Cyclomatic Complexity
- A metric to quantify the **logical complexity** of a program.
- Calculated by:
  1. Number of **regions** in the flow graph.
  2. Formula: \( V(G) = E - N + 2 \), where \( E \) is the number of edges and \( N \) is the number of nodes.
  3. \( V(G) = P + 1 \), where \( P \) is the number of **predicate nodes**.

![[Pasted image 20241117170647.png]]
#### 6. White Box Test Design Process
1. **Draw a flow graph** based on the design or code.
2. **Determine cyclomatic complexity** of the flow graph.
3. Identify a set of **linearly independent paths** based on the complexity.
4. Prepare and execute test cases to cover all identified paths.

#### 7. Using a Graph Matrix
- **Graph matrix** assists in basis path testing, helping derive test cases.

## 5.4 Black-Box Testing: Test Case Design Criteria, Requirement Based Testing, Boundary Value Analysis, Equivalence Partitioning

### Levels of Testing (Black Box Testing)

#### 1. **Definition**  
- Black-box testing, also called **behavioral testing**, focuses on the **functional requirements** of the software without considering the internal code structure.

#### 2. **Objective**  
- The goal is to **exercise all functional requirements** for a program by testing its inputs and expected outputs.

#### 3. **Error Categories**  
- **Incorrect or missing functions**  
- **Interface errors**  
- **Errors in data structures or external database access**  
- **Behavior or performance errors**  
- **Initialization and termination errors**

#### 4. **Complementary to White-Box Testing**  
- Black-box testing is **not an alternative** to white-box testing but a **complementary approach**.  
- It helps uncover a **different class of errors** than those found through white-box testing.

#### 5. **Criteria for Testing**  
- Identifying **classes of errors** and **additional test cases** to ensure reasonable testing coverage.

---

### Graph-Based Testing Methods

#### 1. **Definition**  
- Graph-based testing involves understanding the **objects** in software and the **relationships** connecting them.
![[Pasted image 20241117170941.png]]

Example - 
![[Pasted image 20241117170954.png]]
#### 2. **Process**  
- Testing begins by creating a **graph** of important objects and their relationships.  
- Tests are defined to ensure that all objects have the expected relationships and errors are uncovered.

#### 3. **Behavioral Testing Methods Using Graphs**  
- **Transaction Flow Modeling**: For example, airline reservation systems with validation using **data flow diagrams**.  
- **Finite State Modeling**: Defines different user-observable states of the software, such as order verification during an inventory look-up, represented using **state transition diagrams**.  
- **Data Flow Modeling**: Models transformations occurring to translate one data object into another.  
- **Timing Modeling**: Specifies execution times as the program executes by defining **sequential connections between objects**.

---

### Equivalence Partitioning

#### 1. **Definition**  
- **Equivalence partitioning** divides input and/or output data into **partitions** from which test cases are derived.  
- These partitions are generally based on the **requirements specification** for input.

#### 2. **Error Detection**  
- The technique helps uncover **classes of errors**.  
- An **equivalence class** represents a set of **valid or invalid states** for input conditions.

#### 3. **Guidelines for Equivalence Classes**  
1. If an input condition specifies a **range**, define one **valid** and two **invalid** equivalence classes.  
2. If an input condition requires a **specific value**, define one **valid** and two **invalid** equivalence classes.  
3. If an input condition specifies a **member of a set**, define one **valid** and one **invalid** equivalence class.  
4. If an input condition is **Boolean**, define one **valid** and one **invalid** class.

#### 4. **Test Case Selection**  
- Test cases are selected so that the **largest number of attributes** of an equivalence class are exercised at once (e.g., testing a bank’s interest rates based on account balance).

![[Pasted image 20241117171025.png]]

---

### Boundary Value Analysis (BVA)

#### 1. **Definition**  
- **BVA** focuses on the fact that **more errors occur at the boundaries** of input domains than in the center.  
- It leads to test cases that exercise the **boundary values** of the input domain.

#### 2. **Process**  
- Test cases are designed to select values at the **edges** of the equivalence class (i.e., boundary values).

#### 3. **BVA for Output Domain**  
- BVA can also derive test cases from the **output domain** (e.g., comparing temperature and pressure data or testing internal program data structures).

#### 4. **Guidelines for BVA**  
- If an input condition specifies a **range** bounded by values **a** and **b**, test cases should be designed with values **a** and **b** and just above and below **a** and **b**.  
- If an input condition specifies a set of **values**, design test cases for the **maximum** and **minimum** values.



## 5.5 Object Oriented Testing: Review of OOA and OOD models, class testing, integration testing, validation testing

### Review of OOA and OOD Models

#### 1. **Importance**  
- The construction of object-oriented software begins with creating **requirements (analysis)** and **design models**.  
- Reviewing OOA and OOD models is crucial as the same semantic constructs are used across various levels of the software product.

---

### Problems to Avoid in Analysis (OOA Models)

#### 1. **Unnecessary Special Subclasses**  
- Avoid creating special subclasses to accommodate **invalid attributes**.

#### 2. **Misinterpretation of Class Definitions**  
- Incorrect or extraneous class relationships may arise from **misinterpretation** of class definitions.

#### 3. **Improper Behavior Characterization**  
- Mischaracterizing the behavior of the system or its classes to accommodate **extraneous attributes**.

---

### Problems to Avoid in Design (OOD Models)

#### 1. **Improper Class Allocation**  
- Improper allocation of the class to **subsystems** or tasks during the system design phase.

#### 2. **Unnecessary Procedural Design**  
- Creating unnecessary procedural designs for operations addressing **extraneous attributes**.

#### 3. **Incorrect Messaging Model**  
- The messaging model will be **incorrect** if the design isn’t properly reviewed.

---

### Key Aspects of OOA and OOD Models

#### 1. **System Structure and Behavior**  
- OOA and OOD models provide substantial information about the **structure** and **behavior** of the system.  
- Models should be **rigorously reviewed** before code generation to ensure accuracy.

#### 2. **Correctness**  
- **Syntactic correctness**: Ensures proper use of **modeling symbols**.  
- **Semantic correctness**: The model should accurately reflect the real world.

---

### Consistency of Object-Oriented Models

#### 1. **Consistency Evaluation**  
- Consistency is judged by examining **relationships** among entities in the model.

#### 2. **Class Responsibility Collaboration (CRC) Model**  
- The **CRC model** is used to measure consistency by examining the relationships between classes and their responsibilities.

---

### Steps to Evaluate Class Model

#### 1. **Revisit CRC Model and Object-Relationship Model**  
- Review the requirements for each class and its relationships.

#### 2. **Inspect Each CRC Index Card**  
- Check if delegated responsibilities align with the collaborator's definition.

#### 3. **Ensure Reasonable Connections**  
- Invert the connection to verify that each collaborator is receiving requests from a **reasonable source**.

#### 4. **Class Validity and Responsibility Grouping**  
- Ensure classes are valid and that responsibilities are properly grouped among classes.

#### 5. **Combine Widely Requested Responsibilities**  
- Determine whether frequently requested responsibilities should be combined into a **single responsibility**.

---

### Object-Oriented Testing Strategies

#### 1. **Unit Testing in the OO Context**

- **Classes and Objects**: Each class and object has **attributes** and **operations**.  
- The smallest testable unit is the **class** in object-oriented software.  
- Subclasses inherit operations from the superclass, and each subclass may behave differently, requiring testing within each subclass context.

---

#### 2. **Integration Testing in the OO Context**

##### 1. **Thread-Based Testing**
- Integrates classes required to respond to a single input or event.
- Each thread is integrated and tested individually to ensure no **side effects** occur.

##### 2. **Use-Based Testing**
- Starts with testing **independent classes**, followed by testing **dependent classes** that use the independent classes.  
- Continues until the entire system is constructed, avoiding **drivers and stubs**.

---

#### 3. **Validation Testing in the OO Context**

- Focuses on **user-visible actions** and **user-recognizable outputs**.  
- Draw upon **use cases** based on the **requirement model**.  
- Use cases help identify scenarios with high potential for **user-interaction errors**.

## 5.6 Reverse and re-engineering, types of maintenance

### Software Rejuvenation

#### 1. **Re-documentation**  
- Creation or revision of alternative representations of software at the same level of abstraction.  
- Generates: **data interface tables, call graphs**, and **component/variable cross-references**.

#### 2. **Restructuring**  
- Transformation of the system’s code without changing its behavior.

---

### Reverse Engineering

#### 1. **Definition**  
- Analyzing a system to extract information about its behavior and/or structure.  
- Also known as **Design Recovery** – recreating design abstractions from code, documentation, and domain knowledge.

#### 2. **Generates**  
- **Structure charts, entity relationship diagrams (ERDs)**, **DFDs**, and **requirements models**.

---

### Re-engineering

#### 1. **Definition**  
- Re-engineering is a rebuilding activity, typically involving cost, time, and resources. It is not completed in a few months or years.

#### 2. **Pragmatic Strategy**  
- Every organization needs a **pragmatic strategy** for software reengineering.

![[Pasted image 20241117171828.png]]

---

### Software Reengineering Process Model

#### 1. **Inventory Analysis**  
- The inventory includes information about each active application (e.g., size, age, business criticality).  
- It should be regularly revisited as the status of applications can change.

#### 2. **Document Restructuring**  
- Legacy systems often have **weak documentation**.  
- Documentation creation is time-consuming, so re-documentation focuses only on changed portions.  
- In business-critical systems, pare documentation to an **essential minimum**.

#### 3. **Reverse Engineering**  
- Disassembling existing systems to understand design and manufacturing information.  
- Tools extract **data**, **architectural**, and **procedural design** information from existing programs.

#### 4. **Code Restructuring**  
- Involves altering code structure while maintaining its original functionality.

#### 5. **Data Restructuring**  
- Focuses on improving weak data architecture.  
- Data models are defined, and existing data structures are reviewed for quality.

#### 6. **Forward Engineering**  
- Uses recovered design information to **improve overall system quality** through alterations.

---

### Reverse Engineering

#### 1. **Definition**  
- The process of recreating a design by analyzing the final product (e.g., source code).  
- The abstraction level determines the sophistication of design information extracted.

#### 2. **Interactivity and Directionality**  
- **Interactivity**: Refers to human interaction with automated tools.  
- **Directionality**: Can be one-way (maintenance activity) or two-way (for restructuring).

![[Pasted image 20241117171918.png]]

---

### Software Maintenance

#### 1. **Definition**  
- The process of changing a system after it has been delivered, involving fixing coding errors, design errors, or accommodating new requirements.

#### 2. **Three Types of Software Maintenance**

##### 1. **Fault Repairs**  
- **Coding errors** are inexpensive to correct.  
- **Design errors** are more costly as they may involve multiple components.  
- **Requirements errors** are the most expensive due to extensive system redesign.

##### 2. **Environmental Adaptation**  
- Required when aspects of the system's environment change (e.g., **hardware**, **operating system**, or support software).  
- The system must be modified to adapt to these changes.

##### 3. **Functionality Addition**  
- Occurs when system requirements change, requiring **larger changes** than fault repairs or environmental adaptation.

#### 3. **Other Maintenance Types**

- **Corrective Maintenance**: Refers to fault repair.  
- **Adaptive Maintenance**: Involves adapting the system to a new environment.  
- **Perfective Maintenance**: Focuses on improving the software by implementing new requirements.