[[Module 1 SE PDF]]

## 1.1 Software life cycle models: Waterfall, RAD, Spiral, Agile process

### Q. What is Software and engineering
• Software is more than just a program code. A program is an executable code, which serves some computational purpose. Software is considered to be collection of executable programming code, associated libraries and documentations. Software, when made for a specific requirement is called software product. 

• Engineering on the other hand, is all about developing products, using well-defined, scientific principles and methods.

### Q. What is Software engineering
• Software engineering is the establishment and use of sound engineering principles in order to obtain economically software that is reliable and works efficiently on real machines
• Software engineering is an engineering branch associated with development of software product using well-defined scientific principles, methods and procedures. The outcome of software engineering is an efficient and reliable software product.
• The application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software; that is, the application of engineering to software.

### Q. Layers of Software engineering

![[{C242298C-29EF-4EB5-BA75-6943EAFEBB62}.png]]

**• Quality** 
− Software Engineering rests on solid quality foundation. − Quality assurance leads to more effective approach for software development.

**• Process**
− Holds technology and time for development of software. 
– Provides the glue that holds the layers together; enables rational and timely development; provides a framework for effective delivery of technology; forms the basis for management; provides the context for technical methods, work products, milestones, quality measures, and change management

**• Methods** 
− Provide the technical "how to" for building software; rely on a set of basic principles; encompass a broad array of tasks; include modeling activities

**• Tools** 
− Provide automated or semi-automated support for the process and methods. 
− Tools can also be integrated so that they can also be used for other system software development

### Prescriptive Process Model

• Prescriptive process models advocate an **orderly approach** to software engineering.

• Defines a distinct **set of activities, actions, tasks, milestones, and work products** that are required to engineer high-quality software. 

• The activities may be **linear, incremental, or evolutionary.** 

• Software process models prescribe a **workflow** in which the software development process elements are interrelated to one another.

### Generic Process Framework/SDLC 
Below are the basic process for an SDLC framework

**• Communication** 
– Involves communication among the customer and other stake holders; encompasses requirements gathering.
– All possible requirements of the system to be developed are captured in this phase and documented in a requirement specification doc. 

**• Planning**
– Establishes a plan for software engineering work; addresses technical tasks, resources, work products, and work schedule 

**• Modeling (Analyze, Design)** 
– Encompasses the creation of models to better understand the requirements and the design. 
– The requirement specifications are studied in this phase and system design is prepared. System Design helps in specifying hardware and system requirements and also helps in defining overall system architecture. 

**• Construction (Code, Test)** 
– Combines code generation and testing to uncover errors. 
– With inputs from system design, the system is first developed in small programs called units and integrated. Each unit is developed and tested for its functionality which is referred to as Unit Testing. 
– Post integration the entire system is tested for any faults and failures. 

**• Deployment** 
– Involves delivery of software to the customer for evaluation and feedback

### Waterfall Model

• **Oldest software lifecycle model** and best understood by upper management.
• Used **when requirements are well understood** and **risk is low.** 
• Work flow is in a **linear** (i.e., sequential) fashion. 
• Used often with **well-defined adaptations** or enhancements to current software. 
• Requirements are **very well documented**, clear and fixed. 
• Product definition is **stable.** 
• Technology is understood and is **not dynamic.** 
• There are **no ambiguous** requirements. 
• The project is **short.**

![[{4B696838-765B-418C-B574-36577D473167}.png]]

#### Advantages
• Simple and **easy to understand** and use.
• **Easy to manage** due to the rigidity of the model – each phase has specific deliverables and a review process.
• Phases are processed and completed **one at a time.** 
• Works well for **smaller projects** where requirements are very well understood.
• Clearly defined stages. 
• Process and results are **well documented.**

#### Disadvantages
• No working software is produced until late during the life cycle. 
• **Doesn't support iteration**, so changes can cause confusion.
• Difficult for customers to state all requirements explicitly and up front 
• Requires customer patience because a working version of the program doesn't occur until the final phase. 
• **High amounts of risk and uncertainty.** 

### RAD Rapid Application Development

• RAD refers to a development life cycle designed to give **much faster development and higher quality systems than the traditional life cycle.**
• In RAD model the functional modules are **developed in parallel as prototypes** and are integrated to make the complete product for faster product delivery.
• RAD projects follow **iterative and incremental model** and have small teams comprising of developers, domain experts, customer representatives and other IT resources working progressively on their component or prototype.
• Since there is no detailed preplanning, it makes it easier to incorporate the changes within the development process.
• Small working teams.
• The most important aspect for this model to be successful is to make sure that the **prototypes developed are reusable.** 

![[{09FACBBC-7ABA-4148-81B2-A62A7323EFEA}.png]]

#### Advantages
• **Changing requirements** can be accommodated. 
• **Progress** can be measured. 
• **Iteration time can be short** with use of powerful RAD tools. 
• **Increases reusability** of components. 
**• Reduced** development time. 
• Encourages **customer feedback.** 
• Integration from very beginning solves a lot of integration issues.

#### Disadvantages
• Dependency on technically strong team members for identifying business requirements. 
• Only system that can be modularized can be built using RAD. 
• **Inapplicable to cheaper projects** as cost of modeling and automated code generation is very high. 
• **Requires user involvement** throughout the life cycle.
• Suitable for project requiring **shorter development times.** 
• **Management complexity** is more.

### Spiral Model

• Used when **requirements are not well understood and risks are high.**
• Inner spirals focus on identifying software requirements and project risks; may also incorporate prototyping. 
• Outer spirals take on a classical waterfall approach after requirements have been defined, but permit iterative growth of the software.
• Requires considerable expertise in risk assessment. 
• **Extends waterfall model by adding iteration** to explore /manage risk. 
• Key idea: on each iteration identify and solve the sub-problems with the highest risk.
• New product line which should be released in phases to get enough customer feedback. 
• Significant changes are expected in the product during the development cycle

![[{5F5CC088-6EEB-41BF-B84E-0C77CD314351}.png]]

![[{D4EE5AE2-35BA-42A4-9B57-19038173CD07}.png]]

#### Advantages
• **Realism**: the model accurately reflects the iterative nature of software development on projects with unclear requirements Allows for extensive use of prototypes.
• Requirements can be captured more accurately.
• Users see the system early. 
• Development can be **divided into smaller parts** and more risky parts can be developed earlier which helps better risk management. 
• **Flexible:** incorporates the advantages of the waterfall and evolutionary methods

#### Disadvantages
• Management is **more complex.** 
• End of project may not be known early.
• Not suitable for small or low risk projects and could be **expensive** for small projects. 
• **Spiral may go indefinitely.** 
• Large number of intermediate stages requires excessive documentation.

### Open Source Model

• All successful open-source software projects go through two informal phases. 
• Single individual has an idea for a program, such as an operating system (Linux), a Net browser (Firefox), or a Web server (Apache) , initial version of that program is build. 
• Software is made available to users over internet as it is free.
• Once the users start using the program second informal phase of the project begins.
• Users become co-developers, in that some users report defects and others suggest ways of fixing those defects. 
• Some users put forward ideas for extending the program, and others implement those ideas.
• As the program expands in functionality, yet other users port the program so that it can run on additional operating system/hardware combinations. 
• A key aspect is that individuals work on an open-source project in their spare time on a voluntary basis; they are not paid to participate. 
• The second informal phase of the open-source life-cycle model consists solely of post delivery maintenance.

![[{E083272E-BA2F-4A22-A71A-EB39487659CA}.png]]

### Agile Process Model

•  Agile SDLC model is a **combination of iterative and incremental process models** with focus on process adaptability and customer satisfaction by **rapid delivery of working software product**. 
•  Agile Methods break the product into **small incremental builds.** These builds are provided in iterations. **Each iteration typically lasts from about one to three weeks**. every iteration involves cross functional teams working simultaneously on various areas like planning, requirements analysis, design, coding, unit testing, and acceptance testing. 
•  **At the end of the iteration a working product is displayed to the customer and important stakeholders.** 
•  Iterative approach is taken and **working software build is delivered after each iteration**. Each build is incremental in terms of features; **the final build holds all the features required by the customer.** 
•  Agile processes must be adapted incrementally to manage unpredictability 

![[{E1F395DC-09A7-432B-96D6-1775FD1D7023}.png]]

![[Pasted image 20240920015812.png]]

#### Advantages
• Is a **very realistic approach** to software development. 
• **Promotes teamwork** and cross training. 
• Functionality can be developed rapidly and demonstrated. 
• Suitable for fixed or changing requirements. 
• Delivers early partial working solutions. 
• Good model for environments that change steadily.
• **Easy to manage.** 
• Little or **no planning** required. 
• **Highest priority** is to satisfy the **customer.**

#### Disadvantages
• In case of some software deliverables, especially the large ones, it is **difficult to assess the effort required at the beginning of the software development life cycle.** 
• For Designing and Documentation, agile methodology pays less importance. 
• The **project can easily get taken off track** if the customer representative is not clear what final outcome that they want. 
• For Agile methodology, experience resource will be needed.

### Agile Process Models

• Extreme Programming (XP) 
• Adaptive Software Development (ASD) 
• Dynamic Systems Development Method (DSDM) 
• Scrum 
• Crystal 
• Feature Driven Development (FDD) 
• Agile Modeling (AM)

#### Extreme Programming (XP) 
- XP is based on **object-oriented practices** and a set of defined rules.  
- **Agile adaptation** is incremental to handle unpredictability effectively.

##### XP Planning  
- Begins with the creation of **user stories**.  
- The Agile team **evaluates** and **assigns a cost** to each story.  
- Stories are **grouped** to form deliverable increments.  
- The team **commits to a delivery date** for the first increment.  
- **Project velocity** (speed of work) from the first increment is used to set subsequent delivery dates.

##### XP Design
- Follows the **KISS principle** (Keep It Simple, Stupid).  
- Utilizes **CRC (Class Responsibility Collaborator) cards** for solving complex design problems.  
- Suggests **spike solutions** (design prototypes) for difficult problems.  
- Encourages **refactoring** (continuous improvement of the code structure).

##### XP Coding 
- Unit tests are constructed **before coding** begins.  
- Promotes **pair programming** (two developers work on the same code).

##### XP Testing
- **Daily execution of unit tests** to ensure code integrity.  
- **Acceptance tests** are defined by the customer and used to validate visible functionality.

#### Adaptive Software Development (ASD)

Here’s a more concise, exam-friendly framing of Adaptive Software Development (ASD):


**Adaptive Software Development (ASD) Overview**  
- A **technique for building complex systems** through self-organization, where independent agents collaborate to solve problems beyond the capability of any individual.  
- Focuses on **self-organizing teams**, interpersonal collaboration, and continuous learning.  
- **Adaptable to change** in turbulent environments, allowing software to evolve with minimal planning.

**Distinguishing Features of ASD**  
1. **Mission-Driven**: Activities are aligned with the overall project mission.  
2. **Component-Based**: Focus on delivering **working software** instead of task-oriented development.  
3. **Iterative**: Redoing development in cycles, improving with each iteration.  
4. **Time-Boxed**: Projects have **fixed delivery times**.  
5. **Change-Tolerant**: Embraces change as a competitive advantage.  
6. **Risk-Driven**: High-risk items are addressed early in the development process.

**ASD Phases**  
1. **Speculation**:  
   - Project is initiated with a **customer mission statement**, delivery dates, and initial requirements.  
   - **Adaptive cycle planning** to accommodate changing requirements.  
2. **Collaboration**:  
   - Requires teamwork, often through **joint application development** for requirements gathering.  
3. **Learning**:  
   - Components are implemented and tested; feedback is gathered from **focus groups** and formal reviews.  
   - **Postmortem analysis** helps improve future cycles.


This format highlights the essential aspects of ASD in a straightforward, memorable way for exams.

![[{3A20A4DB-0520-40D3-B35F-95642E2D8A5E}.png]]

#### Dynamic Systems Development Method (DSDM) 
• Provides a framework for building and maintaining systems which meet tight time constraints using incremental prototyping in a controlled environment. 
• Uses Pareto principle (80% of project can be delivered in 20% required to deliver the entire project) 
• Each increment only delivers enough functionality to move to the next increment. 
• Uses time boxes to fix time and resources to determine how much functionality will be delivered in each increment

**DSDM- distinguishing features**
• Active user Involvement is Imperative 
• Teams Must be Empowered to Make Decisions
• Focus on Frequent Delivery 
• Fitness for Business is Criterion for Accepted Deliverables 
• Iterative and Incremental Development is Mandatory 
• All Changes During Development Must Be Reversible 
• Requirements are Baselined at High-Level- to limit the degree of freedom to which requirements can be altered during the development process, some high-level requirements need to be established. 
• Testing is Integrated Throughout the Lifecycle 
• Collaborative and Co-operative Approach-encouraging collaboration of technical staff and business staff in a project is mandatory during DSDM projects, because co-operation is crucial to succeed in a DSDM project.

![[Pasted image 20240920022916.png]]
**DSDM life cycle activities**
• Feasibility study—establishes the basic business requirements and constraints associated with the application to be built and then assesses whether the application is a viable candidate for the DSDM process. 

• Business study—establishes the functional and information requirements that will allow the application to provide business value

• Functional model iteration 
✓ produces a set of incremental prototypes that demonstrate functionality for the customer. 
✓ Additional requirements 

• Design and build iteration—revisits prototypes built during functional model iteration to ensure that each has been engineered in a manner that will enable it to provide operational business value for end users

• Implementation—places the latest software increment (an “operationalized” prototype) into the operational environment.
#### Scrum 
**Scrum Principles** 
• Scrum's goal is facilitating the self-organization of the team so that it can adapt to 
✓ the specifics of the project and 
✓ their changes over time 

• Scrum is an agile software development process model based on multiple small teams working in an intensive and interdependent manner. 
• Process must be adaptable to both technical and business challenges to ensure best product produced. 
• Process yields frequent increments that can be inspected, adjusted, tested, documented and built on
• Development work is partitioned into “packets”
• Testing and documentation are on-going as the product is constructed. 
• Work occurs in “sprints” and is derived from a “backlog” of existing requirements.

**• Backlog** 
✓prioritized list of project requirements. 
✓Items can be added to the backlog. 
✓Updates priorities. 
• Sprints 
✓ consist of work units that are required to achieve a requirement defined in the backlog that must be fit into a predefined time-box.

**• Sprint** 
✓ Changes are not allowed during sprint. 
✓ Allows team members to work in short and stable environment.
• Scrum meetings 
✓ are short (typically 15 minutes) meetings held daily by the Scrum team to check the progress of ongoing work.

**• Demos**
✓ deliver the software increment to the customer so that functionality that has been implemented can be demonstrated and evaluated by the customer. 
✓ May not contain all planned functions but delivery within time-box.

•  Scrum process patterns enable a software team to work successfully in a world where the elimination of uncertainty is impossible.

![[Pasted image 20240920023357.png]]
#### Crystal 
• Crystal is meant to be a family of methods for different project sizes and criticalities. 
• The Crystal methodology is one of the most lightweight, adaptable approaches to software development. 
• Crystal is actually comprised of a family of agile methodologies, whose unique characteristics are driven by several factors such as team size, system criticality, and project priorities.
• Key characteristics of Crystal include teamwork, communication, and simplicity, as well as reflection to frequently adjust and improve the process. 
• primary goal of delivering useful, working software and a secondary goal of setting up for the next game

![[Pasted image 20240920023618.png]]
#### Feature Driven Development (FDD) 
• FDD—distinguishing features 
• Emphasis is on defining “features” 
• a feature “is a client-valued function that can be implemented in two weeks or less.” 
• A feature is a small, client-valued function expressed in the form action, result, object. 
• A features list is created and “plan by feature” is conducted 
• Design and construction merge in FDD
• Emphasizes collaboration among team members 

• Manages problem and project complexity using feature- based decomposition followed integration of software increments. 
• Technical communication using verbal, graphical, and textual means. 
• Software quality encouraged by using incremental development, design and code inspections, SQA audits, metric collection, and use of patterns (analysis, design, construction)

• **Develop overall model** (contains set of classes depicting business model of application to be built)
• **Build features list** (features extracted from domain model, features are categorized and prioritized, work is broken up into two week chunks)
• **Plan by feature** (features assessed based on priority, effort, technical issues, schedule dependencies) • • **Design by feature** (classes relevant to feature are choosen, class and method prologs are written, preliminary design detail developed, owner assigned to each class, owner responsible for maintaining design document for his or her own work packages) 
• **Build by feature** (class owner translates design into source code and performs unit testing, integration performed by chief programmer)

![[Pasted image 20240920024040.png]]
#### Agile Modeling (AM)
 • Agile Modeling (AM) is a practice-based methodology for effective modeling and documentation of software-based systems.

**• Modeling principles** 
**• Model with a purpose:** A developer who uses AM should have a specific goal in mind before creating the model. 
**• Use multiple models:**
✓ There are many different models and notations that can be used to describe software. 
✓ Only a small subset is essential for most projects. 

**• Travel light.** As software engineering work proceeds, keep only those models that will provide long-term value for designing various applications. 

• **Content is more important than representation**. Modeling should impart information to its intended audience. 
• **Know the models and the tools you use to create them**. Understand the strengths and weaknesses of each model and the tools that are used to create it. 
• **Adapt locally**. The modeling approach should be adapted to the needs of the agile team.

## 1.2 Understanding software process, Process metric, CMM Levels

### What is a Process?

• A **system of operations** in producing something; a series of actions, changes, or functions that achieve an end or a result. 
• A **sequence of steps** performed for a given purpose. 
• Process measurement measures the efficacy of a software process indirectly. 
– That is, we derive a set of metrics based on the outcomes that can be derived from the process. 
– Outcomes include 
     • measures of errors uncovered before release of the software 
     • defects delivered to and reported by end-users 
     • work products delivered (productivity) 
     • human effort expended 
     • calendar time expended 
     • schedule conformance 
     • other measures.

### What is a Software Process?

• A **set of activities, methods, practices, and transformations** that people use to **develop and maintain software** and the associated products (e.g., project plans, design documents, code, test cases, and user manuals) is a software process. 
• As an **organization matures**, the **software process becomes better defined** and **more consistently implemented**  throughout the organization. 
• Software process maturity is the extent (degree) to which a specific process is explicitly defined, managed, measured, controlled, and effective. 
• Software process metrics can provide **significant benefit** as an organization works to **improve its overall level of process maturity**.

### Process Metrics

• **Time taken** for a particular process to be completed. 
✓ This can be total time devoted to the process , calendar time , time spent on process by engineers etc. 

• The **resources required** for a particular for particular process. 
✓ Resources might include efforts in person-days , travel costs , or computer resources. 

• The **number of occurrences** of a particular event. 
✓ Events might be monitored include the number of **defects discovered** during code inspection , **number of requirement changes** requested , **average number of lines of code modified** in response to requirement change 

• **Reuse data** 
✓ The number of components produced and their degree of reusability. 

**• Quality-related**
✓focus on quality of work products and deliverables

### Immature Software Organizations

• Software processes are generally improvised 
• If a process is specified, it is not rigorously followed or enforced 
• The software organization is reactionary 
• Managers only focus on solving immediate (crisis) problems
• Schedules and budgets are routinely exceeded because they are not based on realistic estimates
• When hard deadlines are imposed, product functionality and quality are often compromised 
• There is no basis for judging process quality or for solving product or process problems 
• Activities such as reviews and testing are curtailed or eliminated when projects fall behind schedule

### Capability Maturity Model (SW-CMM)

• CMMI (Capability Maturity Model Integration) is a proven industry framework to improve product quality and development efficiency for both hardware and software. 
• CMMI, staged, uses 5 levels to describe the maturity of the organization. 
• Each maturity level has an associated set of process area and generic goals. 
• The maturity levels are measured by the achievement of the specific and generic goals that apply to each predefined set of process areas.'

### Capability - Maturity

• A **maturity level** is a well-defined evolutionary plateau toward achieving a mature software process. Each maturity level provides a layer in the foundation for continuous process improvement. 

• A **capability level** is a well-defined evolutionary plateau describing the organization's capability relative to a process area. A capability level consists of related specific and generic practices for a process area that can improve the organization's processes associated with that process area. Each level is a layer in the foundation for continuous process improvement. 

### Five Levels of Software Process Maturity
![[Pasted image 20240920025408.png]]

![[Pasted image 20240920025446.png]]

### Characteristics of Each Level

**• Initial Level (Level 1)** 
– Characterized as ad-hoc, and occasionally even chaotic processes. 
– Few processes are defined, and success depends on individual effort. 
– Maturity level 1 organizations often produce products and services that work; however, they frequently exceed the budget and schedule of their projects. 
– Maturity level 1 organizations are characterized by a tendency to over commit, abandon processes in the time of crisis, and not be able to repeat their past successes.

**• Managed Level (level 2)** 
• At maturity level 2, an organization has achieved all the specific and generic goals of the maturity level 2 process areas. 
• The process discipline reflected by maturity level 2 helps to ensure that existing practices are retained during times of stress. When these practices are in place, projects are performed and managed according to their documented plans. 
• At maturity level 2, requirements, processes, work products, and services are managed. The status of the work products and the delivery of services are visible to management at defined points. 
• The work products and services satisfy their specified requirements, standards, and objectives. 

**• Defined (Level 3)**
– The software process for both management and engineering activities is documented, standardized, and integrated into a standard software process for the organization.
– All projects use an approved, tailored version of the organization's standard software process for developing and maintaining software. 
– A critical distinction between maturity level 2 and maturity level 3 is the scope of standards, process descriptions, and procedures. 
– At maturity level 2, the standards, process descriptions, and procedures may be quite different in each specific instance of the process (for example, on a particular project).
• At maturity level 3, the standards, process descriptions, and procedures for a project are tailored from the organization's set of standard processes to suit a particular project or organizational unit.
• The organization's set of standard processes includes the processes addressed at maturity level 2 and maturity level 3. 
• Another critical distinction is that at maturity level 3, processes are typically described in more detail and more rigorously than at maturity level 2

**• Quantitatively Managed (Level 4)**
✓  At maturity level 4, an organization has achieved all the specific goals of the process areas assigned to maturity levels 2, 3, and 4 and the generic goals assigned to maturity levels 2 and 3. 
✓  At maturity level 4 Sub processes are selected that significantly contribute to overall process performance. These selected sub processes are controlled using statistical and other quantitative techniques.
✓  Quantitative objectives for quality and process performance are established and used as criteria in managing processes. 
✓  Quantitative objectives are based on the needs of the customer, end users, organization, and process implementers.
✓  detailed measures of process performance are collected and statistically analyzed. 
✓  Special causes of process variation are identified and, where appropriate, the sources of special causes are corrected to prevent future occurrences. 
✓  A critical distinction between maturity level 3 and maturity level 4 is the predictability of process performance. 
✓  At maturity level 4, the performance of processes is controlled using statistical and other quantitative techniques, and is quantitatively predictable. At maturity level 3, processes are only qualitatively predictable.

**• Optimizing (Level 5)**
✓ At maturity level 5, an organization has achieved all the specific goals of the process areas assigned to maturity levels 2, 3, 4, and 5 and the generic goals assigned to maturity levels 2 and 3. 
✓ Maturity level 5 focuses on continually improving process performance through both incremental and innovative technological improvements. 
✓ At maturity level 4, processes are concerned with addressing special causes. 
✓ At maturity level 5, processes are concerned with addressing common causes.

### CMMI- Capability Levels
**• Level 0 (Incomplete)** 
Process area is either not formed or does not achieve goals and objectives defined by CMMI. 

**• Level 1(Performed)** 
✓ All specific goals of CMMI satisfied. 
✓ Work tasks completed for defined work. 

**• Level 2 (Managed)** 
✓ Level 1 criteria satisfied.
✓ Work done on process area conforms to organization’s defined policy
✓ Availability of adequate resources. 
✓ Stakeholders are actively involved. 
✓ All work tasks are evaluated and adhere to CMMI standards.

**Level 3 (Defined)** 
✓ All level 2 criteria satisfied. 
✓ Processes are tailored from organization’s set of standard guidelines. 

**Level 4 (Quantitatively managed)** 
✓ All level 3 criteria satisfied. 
✓ Quantitative objectives for quality and process performance are established and used as criteria in managing process.

**Level 5 (Optimized)** 
✓ All level 4 criteria satisfied. 
✓ Process area is optimized to meet changing customer requirements and continually improve the efficiency of the software product

### CMM Structure
![[Pasted image 20240920030153.png]]

## 1.3  Planning & Estimation: Product metrics Estimation- LOC, FP, COCOMO models

### Project Planning-Estimation

• Objective of software **project planning** is to provide a **framework** that enables the manager to **make reasonable estimates of resources, cost, and schedule**. 
• Estimates should attempt to **define best-case** and **worst- case scenarios** so that project outcomes can be bounded. 
• Plan must be adapted and updated as the project proceeds.

• Project scope must be understood. 
• Elaboration (decomposition) is necessary. 
• Historical metrics are very helpful. 
• At least two different techniques should be used. 
• Uncertainty is inherent in the process.

### Product Metrics

• Product metrics of computer software provide us with a systematic way to assess quality based on a set of clearly defined rules.

• Product **metrics help in assessing efficiency, reliability, complexity, understandability and maintainability** of sot ware product.

### Product Metrics - Function Point (FP)

•The function point (FP) metric can be used effectively as a means for **measuring the functionality** delivered by a system.

• Function point metrics, **measure functionality** from the **users point of view**, that is, on the basis of what the user requests and receives in return 

**• FP metric can then be used to:** 
(1) estimate the **cost or effort** required to design code and test the software.
(2) predict the **number of errors** that will be encountered during testing. 
(3) **forecast** the number of components and/or the number of projected source lines in the implemented system. 

• Information domain values for measurement of FP: 

1. **Number of external inputs (EIs)** 
 ✓ An EI processes data or control information that comes from outside the application’s boundary. 
 ✓ Inputs should be distinguished from inquiries, which are counted separately.

  2. **Number of external outputs (EOs).** 
 ✓ An EO is an elementary process that generates data or control information sent outside the application’s boundary 
 ✓ Each external output is derived data within the application that provides information to the user. 
• external output refers to reports, screens, error messages, etc.

3. **Number of external inquiries (EQs).** 
✓ External Inquiry (EQ) is a transaction function with both input and output components that result in data retrieval. 
✓ An external inquiry is defined as an online input that results in the generation of some immediate software response in the form of an online output.

4. **Number of internal logical files (ILFs).** 
✓ Internal Logical File (ILF) is a user identifiable group of logically related data or control information that resides entirely within the application boundary. 
✓ Maintained via external inputs (EI). 

5. **Number of external interface files (EIFs).** 
✓ the data resides entirely outside the application and is maintained by another application. The external interface file is an internal logical file for another application.

#### Function Point (FP) Calculation

To compute function points (FP), the following relationship is used:

**FP = count total x [0.65 + 0.01 x Sum (Fi)]**

where count total is the sum of all FP entries

![[{6D857EF8-0D26-4D97-A7B6-90BA9FA8A7DB}.png]]
### Line Of Code (LOC)

• LOC is a software metric used to measure the size of computer program by counting number of lines in the text of program’s source code. 

• Lines used for commenting code and header files are ignored.

• LOC is typically used to predict the amount of effort that will be required to develop a program as well as to estimate programming productivity or maintainability once the software product is developed.

**• Two major types of LOC:** 
1. **Physical LOC**: count text 
2. **Logical LOC**: count number of executable statements

#### The Structure of Estimation Models

• The overall structure of such models takes the form:
E = A + B x (ev)^C
• A, B, and C are empirically derived constants, 
• E is effort in person-months, and 
• ev is the estimation variable (either LOC or FP). 

### COCOMO(Constructive Cost Model)
• COCOMO II is actually a hierarchy of estimation models that address the following areas: 

**• Application composition model**. Used during the early stages of software engineering, when prototyping of user interfaces, consideration of software and system interaction, assessment of performance, and evaluation of technology maturity are paramount. 

**• Early design stage model.** Used once requirements have been stabilized and basic software architecture has been established. 

**• Post-architecture-stage model.** Used during the construction of the software.

• Like all estimation models for software, the COCOMO II models require sizing information.

• Three different sizing options are available as part of the model hierarchy: 
    • object points
    • function points 
    • lines of source code

• **object point** is an indirect software measure that is computed using counts of the number 
(1) screens (at the user interface) 
(2) reports 
(3) components likely to be required to build the application 
• Each object instance (e.g., a screen or report) is classified into one of three complexity levels (i.e. Simple, medium, or difficult) using criteria suggested



## 1.4 Project Management activities : Planning, Scheduling and Tracking
### Why Are Projects Late?
• an **unrealistic deadline** established by someone outside the software development group 
• **changing customer requirements** that are not reflected in schedule changes 
• an honest **underestimate** of the amount of effort and/or the number of resources that will be required to do the job 
• predictable and/or unpredictable **risks that were not considered** when the project commenced 
• **technical difficulties** that could not have been foreseen in advance 
• **human difficulties** that could not have been foreseen in advance 
• **miscommunication** among project staff that results in delays 
• a failure by project management to recognize that the project is falling **behind schedule** and a **lack of action** to correct the problem

### Scheduling
• Software project scheduling is an action that **distributes estimated effort across the planned project duration** by allocating the effort to specific software engineering tasks.

#### Scheduling Principles
**• compartmentalization**—define distinct tasks
**• interdependency**—indicate task interrelationship 
**• effort validation**—be sure resources are available 
**• defined responsibilities**—people must be assigned 
**• defined outcomes**—each task must have an output 
**• defined milestones**—review for quality

**• Objective of project scheduling** tool is to enable a project manager to define work tasks , establish their dependencies , assign human resources, develop of variety of graphs and charts that aid in tracking and control of the software project.

• **Program evaluation and review technique (PERT)** and **Critical path method (CPM)** are two project scheduling methods that can be applied to software development. 

• **PERT and CPM** are driven by information from earlier projects: 
✓ Estimates effort 
✓ A decomposition of product function 
✓ Selection of appropriate process model and task set 
✓ Decomposition of tasks

• PERT and CPM are quantitative tools which allow planner to : 
✓ determine **critical path**- chain of tasks that determine duration of tasks.
✓ Most likely **time estimates** for individual tasks by applying statistical models. 
✓ **Boundary window**-time window for a particular task.

#### Schedule Tracking
– conduct **periodic project status meetings** in which each team member reports progress and problems. – evaluate the **results of all reviews conducted** throughout the software engineering process. 
– determine whether formal **project milestones** have been **accomplished** by the scheduled date.
– **compare actual start-date to planned start- date** for each project task listed in the resource table
– **meet informally** with **practitioners** to obtain their subjective **assessment** of progress to date and problems on the horizon. 
– use **earned value analysis** to assess progress quantitatively. 

### Task Network

**• Task Network:** 
✓ also called an activity network. 
✓ Graphic representation of the task flow for the project. 
✓ It is also used as a mechanism through which task sequence and project dependencies are input to an automated project scheduling tool 

### Earned Value Analysis (EVA)

• Earned value 
– is a measure of progress 
– enables us to assess the “percent of completeness” of a project using quantitative analysis rather than rely on a gut feeling 
– “provides accurate and reliable readings of performance from as early as 15 percent into the project.”

•The BCWS values for all work tasks are **summed to derive the budget a completion (BAC).**
**BAC = ∑(BCWSk)** for all tasks k

•value for **budgeted cost of work performed (BCWP)** is computed. 

BCWP = sum of the BCWS values for all work tasks that have actually been completed 

• Distinction between BCWS and BCWP

Given values for BCWS, BAC, and BCWP, important progress indicators can be computed:
![[{0EE5AB6F-D593-4B22-9119-46FBA1288C77}.png]]
![[{CEE08622-274B-4A07-9325-4031876361AA}.png]]

Actual Cost of Work Performed (ACWP)

![[{EDD7D499-F451-4E6D-938F-4E743BDC5A6A}.png]]

# Made by Yashank