## 2.1 Introduction to OO Methodologies :Booch,Rambaugh and Jacobson

### Object Oriented Process

• The Object Oriented Methodology of Building Systems takes the **objects as the basis.** 
• First the system to be developed is **observed and analyzed and the requirements are defined** as in any other method of system development. 
• Objects are identified. 
• Example: Banking System: customer is an object.
• Object Modeling is based on identifying the objects in a system and their interrelationships.
• The basic steps of system designing using Object Modeling may be listed as: 
     ✓ System Analysis 
     ✓ System Design 
    ✓ Object Design
    ✓ Implementation

### Advantages Of Object Oriented Methodology

• Object Oriented Methodology **closely represents the problem domain**. Because of this, it is easier to produce and understand designs.
• The objects in the system are **immune to requirement changes**. Therefore, allows changes more easily
• Object Oriented Methodology designs encourage **more re-use**. New applications can use the existing modules, thereby reduces the development cost and cycle time. 
• The systems designed using this approach are **closer to the real world** as the real world functioning of the system is directly mapped into the system designed using this approach

### Class and Object

• The concepts of **objects and classes** are **intrinsically linked** with each other and form the foundation of object–oriented paradigm. 
• An object is a **real-world element in an object– oriented environment** that may have a physical or a conceptual existence. 
• Object is an entity that has identity , state and behavior.
• Objects can be modeled according to the needs of the application. An object may have a physical existence, like a customer, a car, etc.; or an intangible conceptual existence, like a project, a process, etc. • A class represents a collection of objects having same characteristic properties that exhibit common behavior. 
• Creation of an object as a member of a class is called instantiation. Thus, object is an instance of a class.

### THE RAMBAUGH OMT

• The **object-modeling technique (OMT)** is an object modeling language for software modeling and designing. 
• The object modeling technique(OMT) presented by Jim Rumbaugh and his coworkers describes a method for analysis, design, and **implementation of a system using an object –oriented technique**. 
• OMT is a **fast and intuitive(easy or simple) approach** for identifying and modeling all the objects making up a system.

• The purposes of modeling according to Rambaugh are: 
    ✓  testing physical entities before building them (simulation), 
    ✓  communication with customers, 
    ✓  visualization (alternative presentation of information), and 
    ✓  reduction of complexity.

• The Rambaugh OMT has proposed three main types of models: 
**• Object model :** Main concepts are **classes and associations, with attributes and operations. Aggregation and generalization** are predefined relationships.
**• Dynamic model** : The dynamic model represents a **state/transition** view on the model. Main concepts are states, transitions between states, and events to trigger transitions. Actions can be modeled as occurring within states.
**• Functional model** : The functional model handles the **process of the model**, corresponding roughly to **data flow diagrams**. Main concepts are process, data store, data flow, and actors.

• OMT is a predecessor of the Unified Modeling Language (UML).

### THE BOOCH METHODOLOGY
• The booch methodology is a widely used **object-oriented method** that helps you **design your system using the object paradigm.** 

• It covers **analysis and design phases** of an object-oriented system.

• The analysis phase is split into steps: 
**✓ Customer's Requirements** 
**✓ Domain analysis:** The domain analysis is done by defining object classes; their attributes, inheritance, and methods. State diagrams for the objects are then established. 
✓ The analysis phase is completed with a **validation step.** 
✓ The analysis phase iterates between the customer's requirements step, the domain analysis step, and the validation step until consistency is reached.

• The design phase is **iterative.** 
• A **logic design is mapped to a physical design** like processes, performance, data types, data structures, visibility are defined. 
• A prototype is created and **tested**. The process iterates between the logical design, physical design, prototypes, and testing. 
• The Booch software engineering methodology is **sequential in the sense that the analysis phase is completed and then the design phase** is completed.

• The booch method prescribes a macro development and a micro development process. 
• **Macro process is high level process** describing activities of development team as whole. 
• **Micro process is low level process** describing technical activities of development team.
 
  •  The Booch methodology concentrates on the analysis and design phase and does not consider the implementation or the testing phase in much detail.

### JACOBSON OOSE
• Object-Oriented Software Engineering (OOSE) is a software design technique that is used in software design in object-oriented programming. 
• OOSE is the first object-oriented design methodology that employs use cases in software design. 
• It includes requirements, an analysis, a design, an implementation and a testing model.

## 2.2 Requirements Engineering Tasks, Requirement Elicitation Techniques, Software Requirements: Functional, Non- Functional

### Requirement Elicitation (Gathering)

• A requirement is a **feature** that the system must have or a **constraint** that it must satisfy to be **accepted by the client**. 
• **Requirements engineering** aims at **defining the requirements of the system under construction**. 
• Requirements engineering includes **two main activities**: 
     ✓ requirements elicitation: specification of system that client understands. 
     ✓ Analysis: analysis model that developers can interpret.

• **Requirements elicitation** is about **communication** among developers and users to define a new system. 
• **Failure to communicate** and understand each others - **system fails** 
• **Errors** introduced during requirements elicitation are **expensive to correct**, as they are **usually discovered late in the process**, often as late as delivery.

• **Requirements elicitation methods aim at improving communication** among developers, clients, and users. 
• **Requirement Specification**: The client, the developers, and the users **identify a problem area** and **define a system that addresses the problem**.

### Requirements Elicitation Activities
1. Identifying actors: developers identify the different types of users the future system will support. 

2. Identifying scenarios: 
   ✓   developers observe users and develop a set of detailed scenarios (concrete examples of future systems) for typical functionality provided by the future system. 
   ✓   Scenarios used for understanding application domain in detail.

3. Identifying use cases: 
   ✓   Once developers and users agree on a set of scenarios. 
   ✓   Set of use cases are derived from scenarios that represent future systems. 
   ✓   Use cases are abstractions describing all possible cases of the system

4. Refining use cases: 
   ✓   requirements specification is complete by detailing each use case. 
   ✓   describing the behavior of the system in the presence of errors and exceptional conditions.

5. Identifying relationships among use cases: 
   ✓    identify dependencies among use cases. 
   ✓   Consolidate(combine) the use case model by factoring out common functionality.

• Identifying nonfunctional requirements: 
   ✓   developers, users, and clients agree on aspects that are visible to the user, but not directly related to functionality. 
   ✓   These include constraints on the performance of the system, its documentation, the resources it consumes, its security, and its quality.

**• Questionnaires**: Asking the end user a list of pre- selected questions 
**• Task Analysis:** Observing end users in their operational environment 
**• Scenarios:** Describe the use of the system as a series of interactions between a concrete end user and the system 
**• Use cases:** Abstractions that describe a class of scenarios.

### Functional Requirements
• **Functional requirements** describe the **interactions between the system and its environment independent of its implementation**. 
• Does not focus on implementation details. 
• Example: SatWatch, a watch that resets itself without user intervention

### Non-Functional Requirements
• **Nonfunctional requirements** describe aspects of the system that are **not directly related to the functional behavior** of the system. 
• Usability to performance - **non functional requirements**

#### Non-Functional Requirements (Types)
1. Usability is the ease with which a user can learn to operate or use system. 
   • Usability requirements: online help or user level documentation , manual etc. 
   • Clients can set usability issues for developer for example – color scheme for GUI

2. Reliability is the ability of a system or component to perform its required functions under stated conditions for a specified period of time.
   • Reliability is replaced with dependability which includes other features like robustness and safety
   
3. Performance requirements are concerned with quantifiable attributes of the system such as:
   •   Response Time 
   •   Throughput 
   •   Availability
   •   Accuracy
   
4. Supportability requirements are concerned with the ease of changes to the system after deployment. 
   ✓ **Adaptability**: the ability to change the system to deal with **additional application domain concepts.** 
   ✓ **Maintainability:** the ability to **change the system** to deal with new technology or to **fix defects**. 
   ✓ **Internationalization**: the ability to **change the system** to deal with **additional international conventions**, such as languages, units, and number formats

#### Additional Non-functional Requirements
**• Implementation requirements** 
✓constraints on the **implementation** of the system. 
✓specific tools, programming languages, or hardware platforms. 

**• Interface requirements** 
✓are constraints **imposed by external systems** 
✓interchange formats

**• Operations requirements** 
✓are constraints on the **administration** and **management** of the system. 

**• Packaging requirements** 
✓ are constraints on the **actual delivery** of the system 
✓Installation media for software setting

**• Legal requirements** 
✓are concerned with licensing, regulation, and certification issues. 

**• Quality requirements**


## 2.3  Requirements Characteristics, Requirement qualities, Requirement Specification, Requirement Traceability, System Analysis Model Generation, Documentation : Use Case Diagram, Activity Diagram

### Requirement Characteristics

• Requirements are continuously validated with the client and the user. 
• Requirement validation involves checking that the specification is complete, consistent, unambiguous, and correct.

1. **Completeness:** It is complete if all possible **scenarios through the system are described**, including **exceptional behavior**.
   • Complete—All **features of interest** are **described** by requirements. 
   • **Example of incompleteness**: Satwatch’s limitation of state boundary. 
   • **Solution**: addition of the boundary feature.

2. **Consistent:** The requirements specification is consistent if it **does not contradict itself**. 
   • **Consistent**—No two requirements of the specification contradict each other. 
   • **Example of inconsistency**: Software fault and upgrading mechanisms for new versions. 
   • **Solution:** Revise one of the conflicting requirements

3. **Unambiguous** — The requirements specification is unambiguous if **exactly one system is defined**. 
   • A requirement **cannot be interpreted in two mutually exclusive (either) ways**. 
   • **Example of ambiguity**: time zones and political boundaries. Does SatWatch deal with daylight saving time or not? 
   • **Solution**: add a requirement that SatWatch should deal with daylight saving time.

4. **Correct**: represents accurately the system that the client needs and that the developers intend to build. 
   • Correct—The requirements **describe the features of the system and environment of interest** to the client and the developer, but do **not describe other unintended features**.

### Requirement Specification

• Three more **desirable properties** (qualities) of a requirements specification are that it be **realistic, verifiable, and traceable**. 

• **Realistic:** if the system can be **implemented within constraints**. 
• **Verifiable**: if once the system is built, **repeatable tests** designed to demonstrate that the system **fulfills the requirements** specification.
• **Traceability**: if each requirement can be traced throughout the **software development to its system functions**, and vice-versa.
  • Traceability includes also the **ability to track** the dependencies among requirements, system functions, and the intermediate designs.

### Use Case Diagrams
• Identifying Actors 
   ✓ Actors represent external entities that interact with the system. 
   ✓ An actor can be human or an external system.

• **Give meaningful business relevant names for actors**. 
• **Primary actors should be to the left side of the diagram** –highlight the important roles in the system. 
• **Actors model roles (not positions)** – In a hotel both the front office executive and shift manager can make reservations. “Reservation Agent” actor name to highlight the role. 
• **External systems are actors** – If your use case is send email and if interacts with the email management software then the software is an actor to that particular use case. 
• **Actors don’t interact with other actors** 
• **Place inheriting actors below the parent actor**

• Once the **actors are identified**, the next step in the requirements elicitation activity is to **determine the functionality that will be accessible to each actor.** 
• **Use cases are external (user) view of a system** 
• **Intended for modeling dialogue between user and system**

**• Identifying Scenarios** 
• A scenario is a **narrative description** of what people do and experience as they try to make use of computer systems and applications. 
• Scenario is **description of the system from single actor’s or user’s point of view.** 
• Scenarios may be **defined for current , future , evaluation or training phases** of the software development process.

 **Identifying Use Cases** 
 ✓ Use cases represent what the actors want your system to do for them. 
 ✓ A use case represents a complete flow of events through the system. 
 ✓ A Use Case captures some actor-visible function 
    -Achieves some discrete (business-level) goal for that actor 
    -May be read, write, or read-modify-write in nature

• **Names begin with a verb** – An use case models an action so the name should begin with a verb. 
• **Make the name descriptive** – This is to give more information for others who are looking at the diagram. For example “Print Invoice” is better than “Print”. 
• **Highlight the logical order** – For example if you’re analyzing a bank customer typical use cases include open account, deposit and withdraw. Showing them in the logical order makes more sense. 
• **Place included use cases to the right of the invoking use case** – This is done to improve readability and add clarity. 
• **Place inheriting use case below parent use case** – Again this is done to improve the readability of the diagram.

![[{F4F7CEC4-3405-41CB-A9ED-F578E5F6C9CA}.png]]

#### Elements of Use Case Diagrams
• System function (process – automated or manual).
![[{35960F8E-D59C-457E-8280-3ACA965E7300}.png]]

![[{3AA5C942-842A-478D-8C4F-2CC6807D8907}.png]]

**There can be 5 relationship types in a use case diagram.**

• **Association** between actor and use case
• **Generalization** of an actor 
• **Extend** between two use cases 
• **Include** between two use cases 
• **Generalization** of a use case

##### Association Between Actor and Use Case
• This one is straightforward and present in every use case diagram.
✓An actor must be **associated with at least one use case**. 
✓An actor can be **associated with multiple use cases**. 
✓**Multiple** actors can be **associated with a single use case**.
![[{8AE2C6E5-05D3-4DBF-809C-3B39A96AA55F}.png]]

##### Generalization of an Actor
• Generalization of an actor means that one actor can inherit the role of an other actor.
![[{9D64B5B7-A0B5-445E-80C9-5017D583065A}.png]]

##### Extend Relationship Between Two Use Cases
• It extends the base use case and adds more functionality to the system. 
   ✓   The extending use case is dependent on the extended (base) use case. 
   ✓   The extending use case is usually optional and can be triggered conditionally. 
   ✓   The extended (base) use case must be meaningful on its own. 
   ✓   Arrow points to the base use case when using `<<extend>>` 
   ✓   Extending use case is optional
   ![[{629FBA53-F4D7-4972-BF10-2E3E2948BDC4}.png]]

##### Include Relationship Between Two Use Cases
• Include relationship show that the behavior of the included use case is part of the including (base) use case.
• The base use case is incomplete without the included use case. 
• The included use case is mandatory and not optional.
• Like a “use case subroutine”
![[{9C60A80F-575B-4436-9664-44DCE76ECBEE}.png]]

##### Generalization of a Use Case
• This is similar to the generalization of an actor. 
• This is used when there are common behavior between two use cases and also specialized behavior specific to each use case.
![[{C89BFAEB-2D23-46F1-8DA4-B9E91C8C9B02}.png]]

### Activity Diagram

• An activity diagram describes the **behavior of a system in terms of activities**. 
• **Activity diagram** is basically a **flow chart** to represent the **flow form one activity to another activity.** 
• Activity diagram: **operation of a system.** 
• This flow can be **sequential, branched or concurrent.**

**• Initial node.** 
   ✓   The filled in circle is the starting point of the diagram. 
   ✓   It is shown as filled circle.
![[{9DAEBABF-A817-40C7-9AFD-7C50DB48EE0D}.png]]

**• Activity final node.** 
   ✓   The filled circle with a border is the ending point.
   ✓   The final activity is optional.
![[{2E03C6D9-2C52-4EBC-A57F-87B1493A1193}.png]]

**• Activity**
The rounded rectangles represent activities that occur.
![[{78348234-6EEA-4D64-BAAC-E59582BFA931}.png]]

**• Flow/edge (Control Flow)** 
   ✓   The arrows on the diagram. Within the control flow an incoming arrow starts a single step of an activity; after the step is completed the flow continues along the outgoing arrow.
![[{1F567631-D7A3-4B75-B199-6C30AEE584DD}.png]]

**• Decision.** 
   ✓   **Decisions** are branches in the control flow. 
   ✓   They **denote alternatives** based on a condition of the state of an object or a set of objects. 
   ✓   Decisions are **depicted by a diamond** with one or more incoming open arrows and two or more outgoing arrows.
   ✓   The set of all outgoing edges from a decision represents the set of all possible outcomes.
   ✓   The outgoing edges are labeled with the conditions that select a branch in the control flow.
![[{B886E0A5-1F55-41D1-AEF1-167E9CE2AC15}.png]]
![[{23B59152-D5E7-4767-9CD2-90A5F1890D4B}.png]]

• Some activities occur **simultaneously or in parallel**. Such activities are called **concurrent activities**. 
• **Fork nodes** and **join nodes** represent concurrency. 
• **Fork nodes denote the splitting of the flow** of control into multiple threads. 
• Join nodes denotes the **synchronization of multiple threads** and their **merging of the flow** of control into a **single thread**.

![[{467C6C56-9AF9-47E4-B6CA-60F81F8C711D}.png]]

**• Swim Lanes** 
✓ The contents of an activity diagram may be organized into **partitions (swimlanes)** using solid vertical lines. 
✓ A swim lane (or swimlane diagram) is a **visual element** used in process flow diagrams, or flowcharts, that visually **distinguishes job sharing and responsibilities** for sub-processes of a business process.
• Order Swimlanes in a Logical Manner. 
• Apply Swim Lanes To Linear Processes. 
• Have Less Than Five Swimlanes. 
• Consider Swim areas For Complex Diagrams.
![[{912C218E-75E7-4A0C-9D9D-94488338AFFC}.png]]

![[Pasted image 20240921170327.png]]

## 2.4 Categorizing classes: entity, boundary and control ,Modeling associations and collections-Class Diagram

### Class Diagram

•  A Class Diagram is a diagram **describing the structure of a system.** 
•  shows the system's 
   ✓    classes 
   ✓    Attributes 
   ✓    operations (or methods), 
   ✓    Relationships among the classes.

**• Class: A class represents the blueprint of its objects.** 
• Attributes 
• Operations 
• Relationships 
   ✓   Associations 
   ✓   Generalization
   ✓   Realization 
   ✓   Dependency

#### Class
• Describes a set of objects having similar: 
   – Attributes (status) 
   – Operations (behavior) 
   – Relationships with other classes 

• Attributes and operations may 
– have their visibility marked: 
– "+" for public 
– "#" for protected 
– "−" for private 
– "~" for package

![[{FF5F2733-2BDC-420A-B23D-50A91E402C4C}.png]]

##### Associations
• An association between two classes **indicates that objects** at one end of an association “recognize” objects at the other end and may send messages to them. 
• Example: “An Employee works for a Company”
![[{E23E2C42-2CFD-42B1-BC73-DBDCFFE471CF}.png]]

###### Directed Association
• Refers to a directional relationship represented by a line with an arrowhead. The arrowhead depicts a container-contained directional flow.
![[{9CAD5C32-497B-468E-8076-9CCA0755BD02}.png]]

###### Reflexive Association
• A reflexive association is a relationship from one class back to itself.
![[Pasted image 20240921171151.png]]
![[{4F28A7A2-AAC4-4332-AF51-615AE2DC891D}.png]]

###### Association Class
• In modeling an association, there are times when you need to **include another class because it includes valuable information** about the relationship. 
• use an **association class that you tie to the primary association.** 
• An association class is represented like a normal class. 
• The difference is that the **association line** between the primary classes intersects a **dotted line connected** to the association class.

###### Multiplicity
• the number of objects that participate in the association.
• Multiplicity Indicators
![[{428D0178-8F87-4453-A6FB-251E84987128}.png]]

###### Basic Aggregation
• Aggregation is a special type of association used to model a **"whole to its parts"** relationship. 
• Example: Car as a whole entity and Car Wheel as part of the overall Car.
![[{4E7D7C9F-1A3D-43A6-B10D-4EF8CF18C11B}.png]]
![[{62AE30DD-7043-4843-A282-4DB89880AF58}.png]]

###### Composition Aggregation
• A strong form of aggregation 
– The whole is the sole owner of its part.
    • The part object may belong to only one whole 
– Multiplicity on the whole side must be zero or one. 
– The life time of the part is dependent upon the whole.
![[{AB62C9BD-055B-4655-8824-B497FB500777}.png]]
![[{693C968E-411E-4502-9872-89F28482F78C}.png]]
##### Generalization
• The Generalization association **("is a")** is the **relationship** between the **base class** that is named as **“superclass” or “parent”** and the specific class that is named as **“subclass” or “child”.**
![[{41E1E655-00BC-4347-80F3-EAE729FB5FEF}.png]]

##### Realization
• A realization relationship indicates that **one class implements a behavior specified by another class** (an interface or protocol). 

• a broken line with an unfilled solid arrowhead is drawn from the class that defines the functionality to the class that implements the function.

![[{B56183F9-9909-482B-808B-6AC333C72BD5}.png]]

##### Dependency
• It means that the class at the source end of the relationship has some sort of dependency on the class at the target (arrowhead) end of the relationship.
![[{3740102B-773B-4169-B09A-F44B4A068D08}.png]]
• In UML, a dependency relationship is a relationship in which one element, the client, uses or depends on another element, the supplier. 
• a **Cart class depends on a Product class** because the Cart class uses the Product class as a parameter for an add operation. 
• Cart class is, therefore, the client, and the Product class is the supplier.
• Dependency shows that an element is dependent on another element as it fulfils its responsibilities within the system
![[{6DCEA914-154A-43B7-A23C-6A04BC1BC4A3}.png]]
![[{20332903-5A1B-494B-B9BC-E6939EB02FBB}.png]]

#### Class Diagram example
![[Pasted image 20240921173342.png]]


## 2.5 Dynamic Analysis - Identifying Interaction – Sequence and Collaboration diagrams, State chart diagram

### Sequence Diagram
• The Sequence Diagram models the **collaboration of objects based on a time sequence**. 
• Sequence diagrams represent the objects participating in the interaction horizontally and time vertically.
• Depicts sequence of actions that occur in a system 
• Useful tool to represent dynamic behavior of a system 
• 2 dimensional : 
   – Horizontal axis 
   – Vertical axis
• The focus is **less on messages** themselves and more on the **order in which messages**. 
• Sequence diagrams are good at showing which **objects communicate** with which other objects; and what messages **trigger those communications**.

#### Participants in a Sequence Diagram
• A sequence diagram is made up of a collection of participants.
• Participants – the system parts that interact each other during the sequence. 
• Classes or Objects – each class (object) in the interaction is represented by its named icon along the top of the diagram

#### Elements of Sequence Diagram
• ACTOR 
• OBJECTS 
• LIFELINES 
• MESSAGES 
• ACTIVATION-represents time an object needs to complete task

##### Class Roles or Participants or Objects:
Class roles describe the way an object will behave in context.
![[{BE8E1382-F245-4EA9-A8F0-780B6D31EF1D}.png]]

##### Activation or Execution Occurrence
• Activation or Execution Occurrence Activation boxes represent the time an object needs to complete a task. 

• When an object is busy executing a process or waiting for a reply message, use a thin gray rectangle placed vertically on its lifeline.

![[{211BCCF6-0467-4380-9F30-12664C844097}.png]]

##### Synchronous Message
• A synchronous message requires a response before the interaction can continue. 
• It's usually drawn using a line with a solid arrowhead pointing from one object to another.
![[{B448D9CD-0E61-4E6A-90F3-55BBE34ECEAA}.png]]

##### Asynchronous Message
Asynchronous messages don't need a reply for interaction to continue.
• They are drawn with an arrow connecting two lifelines; however, the arrowhead is usually open and there's no return message depicted.
![[{9A70DC71-3DB1-4F60-9709-2F689D5CC292}.png]]

##### Reply or Return Message
• A reply message is drawn with a dotted line and an open arrowhead pointing back to the original lifeline.
![[{2ABDF486-9C12-475D-8C37-E0AD2DD2BDB0}.png]]

##### Self Message
• A message an object sends to itself, usually shown as a U shaped arrow pointing back to itself.
![[{E8991ECB-8F3A-4C3E-B38B-500E2398774E}.png]]

##### Lost and Found Message
Lost: A lost message occurs whet the sender of the message is known but there is no reception of the message.
![[{DA2CC90E-5297-41B9-98BD-BE7B1F32C521}.png]]

Found: A found message indicates that although the receiver of the message is known in the current interaction fragment, the sender of the message is unknown.
![[{58D8E6C3-9440-4D75-9BE4-6F3F3D394476}.png]]

#### Breaking down a sequence diagrams

##### Actor and classes
![[{84A0426D-8D90-4EBB-BFE1-28FE5CC9D522}.png]]

##### Lifelines
![[{0E96A546-8523-4BE6-A376-CE24670D027D}.png]]

##### Rectangles
![[{0BDDBE02-5B80-406F-8BBA-02789B987E14}.png]]

##### Messages
![[{B235F288-89A7-47E5-A411-F2F8C91E810D}.png]]

##### different types of messages
![[{6FE0114F-75F0-451D-B72C-BD3A0692135F}.png]]


##### Sequence diagrams: endpoints
![[{950B510E-681E-4AA6-B77C-E69224ED2096}.png]]


### Collaboration Diagram
• **Collaboration diagram**-emphasis is on structural organization of the objects that send/receive messages.

#### Elements of a collaboration diagram
   • Object 
   • Relation/Association 
   • Messages
![[{24281CBA-0704-4102-87BC-D18B66FB4033}.png]]

#### STEPS TO DRAW COLLABORATION DIAGRAM
• Place objects as vertices in a graph 
• Add links to connect these object as arcs of graph
• Write messages on links with sequence numbers for send and receive

####  Collaboration Diagram Examples
![[{73220566-B257-474E-9F4C-DD4CAB5931E8}.png]]
![[{5780B745-BFDE-441E-969E-0E2960342742}.png]]
![[{C6712FA3-EF98-4DD9-9DAC-49A7692A02F4}.png]]

### State Chart Diagram
• A **state** in UML is a condition or **situation** an object (in a system) might find itself in during its life time. 
• A state chart diagram is normally used to **model how the state of an object changes** in its lifetime. 
• We **capture** the behavior of the subject object through modeling these various states and transitions between them.
• Thus, a state machine diagram does not necessarily model all possible states, but rather the **critical ones** only. When we say “critical” states, we mean those that act as stimuli and prompt for response in the external world.
•Initial state. This is represented as a filled circle. 
• Final state. This is represented by a filled circle inside a larger circle.
• State. These are represented by rectangles with rounded corners. 
• Transition. A transition is shown as an arrow between two states. Normally, the name of the event which causes the transition is places along side the arrow.
• A guard condition is a condition that has to be met in order to enable the transition to which it belongs:
• Guard conditions can be used to document that a certain event, depending on the condition, can lead to different transitions.

#### Elements of a state chart diagram
• Initial State
![[{1FD5FD4B-6407-4D86-B0B9-182D50746BCF}.png]]
• State
![[{FFC0AC0C-2E1C-4A32-A39D-14C6A7086954}.png]]
• Transition
![[{FFCF02E5-1B95-48E5-BD23-2008970F6A25}.png]]
• Final States
![[{79B33B81-EAA1-4F9B-B376-611DCBCF8ADB}.png]]

#### Examples
![[{2CDD4FA9-255D-4B35-A2D3-001626921D54}.png]]
![[{8B65FA0F-2609-439B-BDA6-E1691E189B31}.png]]
![[{513B6FF4-3261-4A50-8D8E-A2288BC9D9A6}.png]]

# Made by Yashank