Okay, here are your enriched and formatted notes for Module 3: Problem Solving, ready for Obsidian.

# Module 3: Problem Solving

## Module Outline & Topics

- **3.1 Problem Solving by Searching:** Problem Solving Agent, Formulating Problems, Example Problems.
    - Defining problems as state space search, production rules, Problem characteristics, issues in search program design.
- **3.2 Uninformed Search Methods:** Breadth First Search (BFS), Depth First Search (DFS), Depth Limited Search (DLS), Iterative Deepening Depth First Search (IDDFS).
- **3.3 Informed Search Methods:** Heuristics, properties of good heuristics, Greedy best-first Search, A\* Search, AO\* search.
- **3.4 Local Search Algorithms and Optimization Problems:**
    - Hill-climbing search: Hill climbing algorithm, problems and solutions in hill climbing.
    - Constraint Satisfaction Problems (CSP): Defining CSP, inferences in CSP, CSP Backtracking algorithm\*.
    - Genetic algorithms\*: The genetic algorithm process, solving problems with GA for optimization and learning, significance of genetic operators.
- **Adversarial Search:** Games, Optimal strategies, The minimax algorithm, Alpha-Beta Pruning.
- **(#Self Learning):** Online search algorithms, partially observable/imperfect information games.

---

## Solving Problems by Searching

### Core Idea

-   Searching is a fundamental technique in AI used when an agent needs to find a **sequence of actions** to achieve its goals, especially when **no single action** suffices.
    -   Think of planning a route on a map or solving a puzzle – you need multiple steps.
-   Effective problem-solving starts with precise definitions of the **PROBLEMS AND THEIR SOLUTIONS**.

### Types of Search Algorithms

1.  **Uninformed Search Algorithms:**
    -   **Definition:** These algorithms operate with **no information** about the problem beyond its basic definition (states, actions, goal test). They don't know if one state is "closer" to the goal than another.
    -   Also known as **Blind Search**.
    -   ***Simplified:*** Like searching a maze with no map or hints, just exploring systematically.
    -   Examples: BFS, DFS.

2.  **Informed Search Algorithms:**
    -   **Definition:** These algorithms utilize problem-specific **guidance** (heuristics) to direct the search towards more promising states, potentially finding solutions more efficiently.
    -   Also known as **Heuristic Search**.
    -   ***Simplified:*** Like searching a maze with a compass pointing generally towards the exit, or hints about which paths are likely dead ends.
    -   Examples: Greedy Best-First Search, A\* Search.

---

## Search Algorithm Terminologies


### Fundamental Concepts

-   **Search:** A step-by-step procedure to solve a search problem within a given **search space**.
-   **Search Problem Factors:**
    1.  **Search Space:** The set of **all possible solutions** or states that a system might encounter.
        -   *Connection:* This is the "universe" the agent explores. For the Romania map, it's all the cities.
    2.  **Start State:** The initial state from which the agent **begins the search**. (e.g., 'Arad' in the map example).
    3.  **Goal Test:** A function that checks the current state and returns true if it is a **goal state**, false otherwise. (e.g., Is the current city 'Bucharest'?).
-   **Search Tree:** A tree representation of the search problem, where nodes are states and edges are actions. It shows the explored paths from the start state.
    -   *Visualization:* Imagine branching paths from the starting city, each representing a possible driving route.
-   **Actions:** The **description of all available actions** the agent can take in a given state. (e.g., From Arad, actions are Go(Sibiu), Go(Timisoara), Go(Zerind)).
-   **Transition Model:** Represents the **description of what each action does**. It defines the resulting state after performing an action in a given state. (e.g., `Result(In(Arad), Go(Sibiu)) = In(Sibiu)`).
-   **Path Cost:** A function assigning a **numeric cost** to each path (sequence of actions). (e.g., distance traveled, time taken).
-   **Solution:** An **action sequence** that leads from the start state to a goal state.
-   **Optimal Solution:** A solution that has the **lowest path cost** among all possible solutions.

#### Mnemonics for Search Components
Remember the key components of formally defining a search problem with **"I AD G P"**:
- **I**nitial State
- **A**ctions (Possible)
- **D**escription (Transition Model)
- **G**oal Test
- **P**ath Cost Function

---

## Problem-Solving Agents

### Agent Design Philosophy

Problem-solving agents are a type of goal-based agent that decides what to do by finding sequences of actions that lead to desirable states (goals).

1.  **Goal Formulation:**
    -   The agent determines its **goal(s)** based on the **current situation** and its **performance measure**. The goal is the desired state to reach.
    -   *Example:* If the agent is a cleaning robot (performance measure: cleanliness) and it detects dirt (current situation), the goal becomes 'Clean up the dirt'.

2.  **Problem Formulation:**
    -   This is the process of **deciding what actions and states to consider** to achieve the formulated **GOAL**. This involves defining the components discussed earlier (Initial State, Actions, Transition Model, Goal Test, Path Cost).
    -   *Example:* For the route-finding problem, formulation involves identifying cities as states, driving between cities as actions, etc.

3.  **Search Process:**
    -   The agent uses a search algorithm to find a sequence of actions (a solution) that leads from the initial state to the goal state.

4.  **Execution:**
    -   Once a solution (path) is found, the agent executes the actions in the sequence.

### Agent Design Cycle: "Formulate, Search, Execute"

This cycle represents the core operation of a problem-solving agent:
1.  **Formulate:** Define the goal and the problem precisely.
2.  **Search:** Find a sequence of actions (a solution) to reach the goal.
3.  **Execute:** Perform the actions found by the search.

---

## Example Problems: Toy vs. Real-World


### Toy Problems

-   **Purpose:** Intended to **illustrate or test** various problem-solving methods. They are useful for research and teaching because they are easy to describe and analyze.
-   **Characteristics:**
    -   Have a **concise, exact description**.
    -   Can be used by different researchers to **compare the performance** of algorithms under controlled conditions.
-   **Examples:**
    -   8-puzzle, 15-puzzle (Sliding tile puzzles)
    -   8-queens problem
    -   Cryptarithmetic puzzles (e.g., SEND + MORE = MONEY)
    -   Vacuum world
    -   Missionaries and cannibals problem
    -   Simple route finding (like the Romania map)

### Real-World Problems

-   **Purpose:** Problems whose solutions people **actually care about** in practical applications.
-   **Characteristics:**
    -   Often **more difficult** and complex than toy problems.
    -   May **lack a single, agreed-upon specification** (defining the state, successor function, and costs can be challenging and involve approximations or trade-offs).
-   **Examples:**
    -   **Route finding:** Used in GPS navigation systems (e.g., Google Maps, Waze).
    -   **VLSI layout:** Designing the placement of millions of components and connections on a computer chip to optimize area, speed, and yield.
    -   **Robot navigation:** Planning paths for autonomous robots in complex environments (e.g., warehouses, planetary exploration).
    -   **Assembly sequencing:** Determining the optimal order of operations for assembling complex products (e.g., cars, electronics).
    -   **Healthcare:** Treatment planning, drug discovery (e.g., Protein Design).
    -   **Airline travel planning:** Finding optimal flight itineraries based on cost, time, connections, etc.
    -   **Network routing:** Directing data packets efficiently through computer networks.

---

## State Space Representation


### Formal Definition of a Problem

A problem can be defined formally using **five components**:

1.  **INITIAL STATE:** The state where the agent begins.
    -   *Example:* In the Romania map problem, the initial state is `In(Arad)`.
2.  **POSSIBLE ACTIONS:** A description of the actions available to the agent in a given state `s`, often denoted as `ACTIONS(s)`.
    -   *Example:* `ACTIONS(In(Arad)) = {Go(Sibiu), Go(Timisoara), Go(Zerind)}`.
3.  **TRANSITION MODEL:** A description of what each action does. It specifies the resulting state when an action `a` is taken in state `s`, often denoted as `RESULT(s, a)`.
    -   *Example:* `RESULT(In(Arad), Go(Sibiu)) = In(Sibiu)`.
    -   The set of all states reachable from the initial state by any sequence of actions defines the **State Space**.
4.  **GOAL TEST:** Determines whether a given state `s` is a goal state.
    -   Can be explicit (e.g., `s = In(Bucharest)`) or implicit (e.g., Checkmate in chess, where specific board configurations satisfy the goal).
5.  **PATH COST FUNCTION:** Assigns a numeric cost to a path (sequence of actions). Typically denoted as `c(s, a, s')` for the **step cost** of taking action `a` in state `s` to reach state `s'`, and the total path cost is the sum of step costs.
    -   *Example:* Driving distance between cities, number of moves in a puzzle.
    -   *Note:* Solution quality is often measured by the path cost function.

### Solution Definition

-   A **SOLUTION** to a problem is an **ACTION SEQUENCE** (a path) that leads from the **INITIAL STATE** to a **GOAL STATE**.
-   An **OPTIMAL SOLUTION** is a solution with the **lowest path cost** among all possible solutions.

---

## Example 1: Route Finding (Romania Map)

### Problem Statement

Currently in Arad, need to get to Bucharest by tomorrow to catch a flight. What is the State Space? Find a route.

### Problem Formulation (State Space Representation)

1.  **States:** The various cities the agent could be located in.
    -   *Note:* We simplify by ignoring lower-level details like the exact position on the road between cities, fuel levels, etc. The state is just the current city `In(City)`.
    -   *Example States:* `In(Arad)`, `In(Sibiu)`, `In(Bucharest)`.

2.  **Initial State:** `In(Arad)`.

3.  **Actions:** Drive between neighboring cities. `ACTIONS(s)` returns the set of `Go(NeighborCity)` actions available from state `s`.
    -   *Example:* `ACTIONS(In(Arad)) = {Go(Sibiu), Go(Timisoara), Go(Zerind)}`.

4.  **Transition Model:** `RESULT(s, a)` gives the state resulting from action `a` in state `s`.
    -   *Example:* `RESULT(In(Arad), Go(Sibiu)) = In(Sibiu)`.

5.  **Goal Test:** Check if the current state is `In(Bucharest)`.
    -   This is an explicit goal test. (How many states satisfy this condition? Only one: `In(Bucharest)`).

6.  **Path Cost Function:** The sum of the driving distances between cities along the path. This represents the total distance traveled.
    -   *Step Cost:* `c(s, a, s')` is the distance between the city in state `s` and the city in state `s'`. (e.g., `c(In(Arad), Go(Sibiu), In(Sibiu)) = 140`).

### Solution

-   A **solution** will be the route (sequence of cities) to travel through to get from Arad to Bucharest.
-   An **optimal solution** will be the route with the lowest total distance (path cost).

---

## Example 2: Vacuum Cleaner World

![[Pasted image 20250501234358.png]]
### Problem Description

-   The world has only two locations (A, B).
-   Each location may or may not contain dirt.
-   The agent (vacuum cleaner) can be in one location or the other.
-   There are **8 possible world states** (2 locations * 2 dirt statuses per location * 2 agent positions). 
![[Pasted image 20250501234425.png]]
-   **Actions:** `Left`, `Right`, `Suck`.
-   **Goal:** Clean up all the dirt (i.e., reach a state where both locations A and B are clean).

### Problem Formulation

1.  **States:** Determined by agent location and dirt location(s). Since there are $n$ locations, there are $n \cdot 2^n$ states. For $n=2$, there are $2 \times 2^2 = 8$ states.
    -   *State Representation:* Can be represented as `(AgentLocation, DirtStatus_A, DirtStatus_B)`. E.g., `(A, Dirty, Clean)`.

2.  **Initial State:** Any state can be designated as the initial state (e.g., State 5 in Figure 3.3 from page 17: Agent in A, A is Dirty, B is Dirty).

3.  **Actions:** `{Left, Right, Suck}`. (Larger environments might include `Up`, `Down`).

4.  **Transition Model:** Describes the effect of actions.
    -   `Left`: Moves agent left if not already in the leftmost square.
    -   `Right`: Moves agent right if not already in the rightmost square.
    -   `Suck`: Cleans the current square if it's dirty.
    -   *Note:* Actions might have no effect (e.g., moving `Left` from the leftmost square, `Sucking` in a clean square). The complete state space diagram (Figure 3.3 from page 17/19) shows all transitions.

5.  **Goal Test:** Checks whether both squares A and B are clean. States 7 and 8 in the diagram are goal states.

6.  **Path Cost Function:** Each step (action) costs 1. The path cost is the total number of steps taken.

---

## Example 3: Missionaries and Cannibals


### Problem Description

-   **Setup:** Three missionaries (M) and three cannibals (C) are on the left bank of a river.
-   **Goal:** Move everyone to the right bank.
-   **Tool:** A boat that can carry at most two people at a time.
-   **Constraint:** On *either* bank, the number of cannibals must **never** exceed the number of missionaries (if missionaries are present). If C > M on a bank, the missionaries get eaten!
-   **Constraint:** The boat cannot cross the river by itself (must have at least one person).
-   **Task:** Find a sequence of crossings (actions) to safely move everyone from the left bank to the right bank.

### Problem Formulation
![[Pasted image 20250501234507.png]]
1.  **State Space:** Represent the state as a triple **(x, y, z)** where:
    -   `x`: number of missionaries on the *original* (left) bank ($0 \le x \le 3$)
    -   `y`: number of cannibals on the *original* (left) bank ($0 \le y \le 3$)
    -   `z`: location of the boat (1 for left bank, 0 for right bank)
    -   *Constraint Check:* A state `(x, y, z)` is *invalid* (illegal) if `x > 0` and `y > x` (too many cannibals on left bank) OR if `(3-x) > 0` and `(3-y) > (3-x)` (too many cannibals on right bank).

2.  **Initial State:** `(3, 3, 1)` (All missionaries, cannibals, and the boat are on the left bank).

3.  **Actions (Successor Function):** From a state, move the boat from one bank to the other with:
    -   One missionary
    -   One cannibal
    -   Two missionaries
    -   Two cannibals
    -   One missionary and one cannibal
    -   *Note:* The resulting state must be valid (obey the C ≤ M constraint on both banks). Not all states are attainable (e.g., (0,0,1) is impossible if starting from (3,3,1)).

4.  **Goal State:** `(0, 0, 0)` (Everyone is on the right bank, boat is on the right bank).

5.  **Path Cost:** 1 unit per crossing (each trip of the boat). The goal is often just to find *any* valid sequence, but minimizing crossings is also a valid objective.

### Solution Sequence Example

*(Based on text from page 24, reformatted for clarity. L=Left Bank, R=Right Bank, B=Boat Position)*

*Initial State:* L: 3M, 3C, B | R: 0M, 0C

1.  Send 2 Cannibals (C,C) Left to Right:
    *   L: 3M, 1C | R: 0M, 2C, B (State: (3,1,0)) - *Valid*
2.  Send 1 Cannibal (C) Right to Left:
    *   L: 3M, 2C, B | R: 0M, 1C (State: (3,2,1)) - *Valid*
3.  Send 2 Cannibals (C,C) Left to Right:
    *   L: 3M, 0C | R: 0M, 3C, B (State: (3,0,0)) - *Valid*
4.  Send 1 Cannibal (C) Right to Left:
    *   L: 3M, 1C, B | R: 0M, 2C (State: (3,1,1)) - *Valid*
5.  Send 2 Missionaries (M,M) Left to Right:
    *   L: 1M, 1C | R: 2M, 2C, B (State: (1,1,0)) - *Valid*
6.  Send 1 Missionary (M) and 1 Cannibal (C) Right to Left:
    *   L: 2M, 2C, B | R: 1M, 1C (State: (2,2,1)) - *Valid*
7.  Send 2 Missionaries (M,M) Left to Right:
    *   L: 0M, 2C | R: 3M, 1C, B (State: (0,2,0)) - *Valid*
8.  Send 1 Cannibal (C) Right to Left:
    *   L: 0M, 3C, B | R: 3M, 0C (State: (0,3,1)) - *Valid*
9.  Send 2 Cannibals (C,C) Left to Right:
    *   L: 0M, 1C | R: 3M, 2C, B (State: (0,1,0)) - *Valid*
10. Send 1 Cannibal (C) Right to Left:
    *   L: 0M, 2C, B | R: 3M, 1C (State: (0,2,1)) - *Valid*
11. Send 2 Cannibals (C,C) Left to Right:
    *   L: 0M, 0C | R: 3M, 3C, B (State: (0,0,0)) - *Goal Reached!*

*(Note: The solution steps on page 24 seem slightly different/confusing in notation. The sequence above is a standard known solution. The state space diagram on page 209 provides a visual map of valid states and transitions.)*

---

## Example 4: The 8-Puzzle

### Problem Description

-   A **sliding-block/tile puzzle**, one of the most popular toy problems in AI studies.
-   **Setup:** A 3x3 grid containing 8 numbered tiles (1-8) and one blank space.
-   **Goal:** Arrange the tiles from a given initial configuration into a specified goal configuration.
-   **Actions:** Move the **BLANK** tile UP, DOWN, LEFT, or RIGHT.
-   **Constraints:**
    -   Cannot move into a space occupied by another tile (implicit in moving the blank).
    -   Cannot move outside the boundaries/edges of the 3x3 grid.

*Example Initial and Goal States (from page 28):*

```
INITIAL      GOAL
1 2 3        1 2 3
* 4 6        4 5 6
7 5 8        7 * 8
(* represents the blank space)
```

### Problem Formulation


1.  **States:** A specific configuration of the 8 tiles and the blank space on the 3x3 grid. Specifies the location of each tile.
    -   *Complexity:* There are $9!/2 = 181,440$ reachable states from any given state. (Note: Only half of the $9!$ permutations are reachable). This problem is **NP-Complete** An NP-Complete problem is a very hard problem where it's easy to check a solution, but extremely difficult to find one.

2.  **Initial State:** Any valid configuration can be designated as the initial state.

3.  **Actions:** The simplest formulation defines actions as movements of the blank space: `{Left, Right, Up, Down}`. The available actions depend on the blank's current position (e.g., if blank is in the top-left corner, only `Right` and `Down` are possible).

4.  **Transition Model:** Given a state and a valid action (moving the blank), returns the resulting state (the configuration after the blank and the adjacent tile swap places).
    -   *Example:* If we apply `Left` to the initial state shown above (blank moves left), the '4' tile moves right into the blank's previous spot. *(See Figure 3.4 reference, implicitly on page 29/30)*.

5.  **Goal Test:** Checks if the current state configuration matches the specified goal configuration. (Other goal configurations are possible).

6.  **Path Cost:** Each step (move of the blank tile) costs 1. The path cost is the total number of moves.

#### Examples

![[Pasted image 20250501234958.png]]
![[Pasted image 20250501235020.png]]
![[Pasted image 20250501235028.png]]

---

## Example 5: N-Queens Problem (4-Queens, 8-Queens)

*(Insert images from pages 37, 38, 39, 40, 41, 42, 43, 44, 45 here. These show the problem, examples, formulation, and state space trees.)*

### Problem Description

-   **The N-Queens Problem:** Place N queens on an N×N chessboard such that **no two queens threaten each other** i.e no two of them are on the same row, column, or diagonal.
-   **Threat Condition:** A queen attacks any piece in the same **row, column, or diagonal**.
-   **Goal:** Find a configuration of N queens satisfying the non-attacking constraint.

*(Image on page 39 shows an almost-solution for 8-Queens)*
*(Image on page 45 shows a possible solution for 4-Queens)*
#### 4 Queens
![[Pasted image 20250501235402.png]]

#### 8 Queens
![[Pasted image 20250501235915.png]]

### Problem Formulation (Incremental Approach)


1.  **States:** Any arrangement of 0 to 8 queens on the board.
    - *Alternative Formulation (often better for search):* States where queens are added one column at a time. A state can be represented by the row positions of queens in columns 1 to k (for $k \le N$).

2.  **Initial State:** No queens on the board (empty board).

3.  **Actions:** Add a queen to any empty square.
    - *Alternative Formulation:* Add a queen to the next available column in a row that is not attacked by existing queens.

4.  **Transition Model:** Returns the board with a queen added to the specified square.

5.  **Goal Test:** 8 queens are on the board, and none are attacked by any other queen.

6.  **Path Cost:** Not typically relevant for this problem; we just need to find *a* valid configuration.

#### State Space Tree for 4 queens

![[Pasted image 20250501235833.png]]


---

## Example 6: Water Jug Problem

*(Insert images from pages 46, 47, 48 here)*

### Problem Description

-   **Setup:** You are given two jugs: a 4-gallon one (X) and a 3-gallon one (Y). Neither has measuring marks.
- ![[Pasted image 20250502000008.png]]
-   **Tool:** A pump to fill the jugs with water.
-   **Goal:** Get exactly 2 gallons of water into the 4-gallon jug (X).

### Possible Actions / Rules


Let `(x, y)` represent the state where jug X has `x` gallons and jug Y has `y` gallons. $0 \le x \le 4$, $0 \le y \le 3$.

1.  Fill X completely: If `x < 4`, then `(4, y)`.
2.  Fill Y completely: If `y < 3`, then `(x, 3)`.
3.  Empty X: If `x > 0`, then `(0, y)`.
4.  Empty Y: If `y > 0`, then `(x, 0)`.
5.  Pour Y into X until X is full: If `x+y >= 4` and `y > 0`, then `(4, y - (4-x))`.
6.  Pour X into Y until Y is full: If `x+y >= 3` and `x > 0`, then `(x - (3-y), 3)`.
7.  Pour all of Y into X: If `x+y <= 4` and `y > 0`, then `(x+y, 0)`.
8.  Pour all of X into Y: If `x+y <= 3` and `x > 0`, then `(0, x+y)`.

### Solution Sequence Example

1.  Start: `(0, 0)`
2.  Fill Y: `(0, 3)`
3.  Pour Y into X: `(3, 0)`
4.  Fill Y: `(3, 3)`
5.  Pour Y into X until X is full: `(4, 2)` (Pour 1 gallon from Y to X)
6.  Empty X: `(0, 2)`
7.  Pour Y into X: `(2, 0)` - **Goal Reached!** (Jug X has 2 gallons)

![[Pasted image 20250502000238.png]]
---

## Real-World Problem Examples Revisited

These examples illustrate the complexity and requirements of solving problems outside the "toy" domain.

### Airline Travel Planning

-   **States:** Complex, involving location (airport), current time, previous flight segments, fare bases, domestic/international status, user preferences (seat class, frequent flyer info). Requires tracking "historical" aspects.
-   **Initial State:** Specified by the user's query (origin, destination, dates, etc.).
-   **Actions:** Take any flight from the current location, in any seat class, leaving after the current time (plus buffer for transfers).
-   **Transition Model:** Resulting state includes the new location (destination airport), arrival time, updated cost, etc.
-   **Goal Test:** Are we at the final destination specified by the user?
-   **Path Cost:** Multi-faceted, depending on monetary cost, waiting time, flight time, customs/immigration procedures, seat quality, time of day, airplane type, frequent-flyer miles awarded, etc.

### VLSI Layout

-   Positioning millions of components/connections on a chip.
-   **Goals:** Minimize area, minimize circuit delays, minimize stray capacitances, maximize manufacturing yield.
-   This is a highly complex optimization problem.

### Protein Design

-   Finding a sequence of amino acids that folds into a 3D protein with specific properties (e.g., to cure a disease).
-   Involves predicting complex molecular interactions and structures.

---

## Defining Problems as State Space Search

### Steps for Formal Definition

1.  Define a **State Space** containing **all possible configurations** of relevant objects.
    -   *Consider:* What information is crucial to define a unique situation?
2.  Specify one or more **Initial States** describing possible starting situations.
3.  Specify one or more **Goal States** representing acceptable solutions.
4.  Specify a set of rules describing available **Actions** (also called **Operators**).
    -   *Consider:*
        -   What unstated assumptions exist in the informal problem description? (e.g., In Romania map, assume roads are traversable).
        -   How general should the rules be? (e.g., `Go(city1, city2)` vs. specific `Go(Arad, Sibiu)` rules).
        -   How much pre-computation should be embedded in the rules? (e.g., Pre-calculating distances vs. calculating on the fly).

---

## Production Systems

### Concept

A production system provides a formal framework for implementing search algorithms, particularly rule-based ones. It consists of:

1.  **A Set of Rules:**
    -   Each rule typically has a **Left Side (Pattern/Condition)** determining its applicability.
    -   And a **Right Side (Action/Operation)** describing what to do if the rule is applied.
    -   *Format:* `IF (condition) THEN (action)`

2.  **One or More Knowledge Bases (Databases):**
    -   Contains the information relevant to the problem, often structured.
    -   Includes the current state of the world, static facts, etc.
    -   *Example:* The current configuration of the 8-puzzle, the rules of chess.

3.  **Control Strategy:**
    -   Determines the **order** in which rules are applied or compared against the current state.
    -   Specifies how to **resolve conflicts** if multiple rules are applicable simultaneously.
    -   *Examples:* Choose the first applicable rule, choose the rule leading to the best estimated state (heuristic). Controls the search process (like BFS, DFS).

4.  **A Rule Applier:**
    -   The mechanism that matches rule conditions against the knowledge base and executes the action of the selected rule, modifying the knowledge base (current state).

### Example: Water Jug Production Rules

| S.No. | Initial State (Condition) | Condition Check       | Final State      | Description of Action Taken                               |
| :---- | :------------------------ | :-------------------- | :--------------- | :-------------------------------------------------------- |
| 1.    | (x,y)                     | If x < 4              | (4, y)           | Fill the 4 gallon jug completely                          |
| 2.    | (x,y)                     | if y < 3              | (x, 3)           | Fill the 3 gallon jug completely                          |
| 3.    | (x,y)                     | If x > 0              | (x-d, y)         | Pour *some* part `d` from the 4 gallon jug (less precise) |
| 4.    | (x,y)                     | If y > 0              | (x, y-d)         | Pour *some* part `d` from the 3 gallon jug (less precise) |
| 5.    | (x,y)                     | If x > 0              | (0, y)           | Empty the 4 gallon jug                                    |
| 6.    | (x,y)                     | If y > 0              | (x, 0)           | Empty the 3 gallon jug                                    |
| 7.    | (x,y)                     | If (x+y) >= 4 & y > 0 | (4, y-[4-x])     | Pour from 3-gal to fill 4-gal jug                         |
| 8.    | (x,y)                     | If (x+y) >= 3 & x > 0 | (x-[3-y], 3)     | Pour from 4-gal to fill 3-gal jug                         |
| 9.    | (x,y)                     | If (x+y) <= 4 & y > 0 | (x+y, 0)         | Pour all from 3-gal into 4-gal jug                      |
| 10.   | (x,y)                     | if (x+y) <= 3 & x > 0 | (0, x+y)         | Pour all from 4-gal into 3-gal jug                      |

### Example: 8-Puzzle Production Rules

![[Pasted image 20250502000531.png]]

-   **Working Memory:** Represents the current board state and the goal state.
-   **Production Set (Rules):**
    -   `IF (current state == goal state) THEN halt.`
    -   `IF (blank is not on left edge) THEN move blank left.`
    -   `IF (blank is not on top edge) THEN move blank up.`
    -   `IF (blank is not on right edge) THEN move blank right.`
    -   `IF (blank is not on bottom edge) THEN move blank down.`
-   **Control Strategy:** Determines which valid move (rule) to apply next (e.g., BFS explores all valid moves level by level, DFS picks one and goes deep).

---

## Problem Characteristics

*(Insert image from page 56 here)*

Analyzing these characteristics helps understand the nature of a problem and choose appropriate solving techniques.

1.  **Is the problem decomposable?**
    -   Can it be broken down into smaller, independent **subproblems**?
    -   *Example:* Symbolic integration can be decomposed (e.g., ∫(x² + sin(x)) dx = ∫x² dx + ∫sin(x) dx). The 8-puzzle is *not* easily decomposable.

2.  **Can solution steps be ignored or undone?**
    -   **Ignorable:** Steps can be ignored (e.g., Theorem proving - discovering a lemma might be useful but isn't strictly necessary for the final proof path).
    -   **Recoverable:** Steps can be undone (e.g., 8-puzzle - can move the blank back). Requires keeping track of state.
    -   **Irrecoverable:** Steps cannot be undone (e.g., Chess - once a piece is moved, you can't take it back in the game context). Requires careful planning.

3.  **Is the universe predictable?**
    -   Are the outcomes of actions certain? (Deterministic vs. Stochastic)
    -   *Example:* 8-puzzle is predictable. Playing bridge is not (uncertainty about opponent hands). Controlling a robot arm might be unpredictable due to friction, motor variations. Planning problems often assume predictability.

4.  **Is a good solution Absolute or Relative?**
    -   **Absolute:** Any path/solution is acceptable (e.g., finding *any* legal assignment in N-Queens).
    -   **Relative:** Need the *best* solution based on some quality measure (e.g., finding the shortest path in route finding). **Good heuristics** play an important role here.

5.  **Is the solution a state or a path?**
    -   **State:** The final configuration is the solution (e.g., N-Queens, finding the final board state).
    -   **Path:** The sequence of actions is the solution (e.g., Route finding, the path itself is the answer).

6.  **What is the role of knowledge?**
    -   How much information is required beyond the basic rules?
    -   *Example:* Chess requires significant knowledge (strategy, tactics). Newspaper reading requires vast amounts of general knowledge. Simple puzzles require less external knowledge.

7.  **Does the task require interaction with a person?**
    -   **Solitary:** Agent works alone (e.g., Theorem proving).
    -   **Conversational:** Agent interacts with a user (e.g., Medical diagnosis system asking questions, responding to reactions).

8.  **Problem Classification:** Grouping problems based on these characteristics.

---

## Issues in Designing Search Programs

Key considerations when building search-based problem solvers:

1.  **Direction of Search:**
    -   **Forward Reasoning:** Start from the initial state and apply rules/actions to reach the goal.
    -   **Backward Reasoning:** Start from the goal state and apply rules/actions in reverse to find a path back to the initial state.
    -   *Choice:* Depends on branching factors. If many states lead to the goal but few actions lead away from it, backward search might be better.

2.  **Selecting Matching (Applicable) Rules:**
    -   Need efficient procedures to match the conditions of production rules against the current state in the knowledge base.
    -   *Challenge:* With many rules and complex states, matching can be computationally expensive.

3.  **Knowledge Representation Problem:**
    -   How to represent each node (state) of the search process effectively?
    -   *Trade-offs:* Representing the state concisely (e.g., small array for Chess board) might require more complex rules/functions, while a more detailed representation might simplify rules but consume more memory/time.

---

## Searching for Solutions: Uninformed Search Strategies


### Overview

-   **Uninformed (Blind) Search:** Strategies that use **no additional information** about states beyond what's provided in the problem definition.
-   They can only:
    -   Generate successor states.
    -   Distinguish a goal state from a non-goal state.
-   *Analogy:* Searching in the dark.

![[Pasted image 20250502000616.png]]

### Common Uninformed Search Algorithms

1.  **Breadth-First Search (BFS)**
2.  **Depth-First Search (DFS)**
3.  **Depth-Limited Search (DLS)**
4.  **Iterative Deepening Depth-First Search (IDDFS)**

![[Pasted image 20250502000724.png]]
### 1. Breadth-First Search (BFS)

![[Pasted image 20250502000741.png]]
-   **Strategy:** Expands nodes level by level.
    1.  Expand the **root node** first.
    2.  Expand **all successors** of the root node.
    3.  Expand **all successors** of those nodes, and so on.
-   Implemented using a FIFO (First-In, First-Out) queue for the frontier (nodes waiting to be expanded).

![[Pasted image 20250502000802.png]]

#### Advantages of BFS:

-   **Complete:** Guarantees finding a solution if one exists.
-   **Optimal (Uniform Cost):** Finds the **minimal solution** (shallowest goal node, least number of steps) if path costs are uniform (e.g., each step costs 1).

#### Disadvantages of BFS:

-   **Memory Intensive:** Requires storing all nodes at the current depth level in memory to expand the next level. Can consume **lots of memory** ($O(b^d)$, where b is branching factor, d is depth).
-   **Time Consuming:** Can take **lots of time** ($O(b^d)$) if the solution is far away (deep) from the root node.

### 2. Depth-First Search (DFS)

![[Pasted image 20250502000823.png]]
-   **Strategy:** Always expands the **deepest node** in the current frontier (the edge of the explored part) of the search tree. It explores one path as far as possible before backtracking.
-   Implemented using a LIFO (Last-In, First-Out) stack for the frontier.
-   Traversal Order: Often explores "Root -> Left Subtree -> Right Subtree".

![[Pasted image 20250502000844.png]]

#### Advantages of DFS:

-   **Memory Efficient:** Consumes **very little memory** ($O(b \times m)$, where m is the maximum depth) as it only needs to store the current path and its siblings.
-   **Fast (Potentially):** Can find a solution quickly if it happens to be down the first path explored. May reach the goal node in less time than BFS if it traverses the "right" path early.
-   Can find a solution without examining much of the search space if lucky.

#### Disadvantages of DFS:

-   **Incompleteness:** May **not terminate** if the search space contains infinite paths (or very long paths/cycles) and doesn't find a solution. It can go on infinitely down one path.
-   **Non-Optimal:** Does not guarantee finding the shortest path solution. The first solution found might be much deeper (higher cost) than an optimal one.
-   **Duplicate Nodes:** Cannot easily check for duplicate nodes (revisiting states) without storing explored states, which negates the memory advantage.
-   *Issue Mitigation:* The non-termination issue can be addressed using a **cut-off depth** (leading to DLS).

### 3. Depth-Limited Search (DLS)



-   **Strategy:** A modification of DFS to handle infinite state spaces. It performs a DFS but only down to a **predetermined depth limit (L)**.
-   Nodes at the depth limit `L` are treated as if they have no successors.
-   **Process:** If the depth limit is fixed (e.g., L=2), DLS performs DFS exploring paths up to length 2.

![[Pasted image 20250502001034.png]]
shows DLS with limit L=2. It explores A->B->D, then backtracks. It explores A->C->E, then backtracks. It stops at depth 2.)

![[Pasted image 20250502001101.png]]
shows DLS with limit L=2, finding goal J at depth 2: S -> B -> I -> J)

#### Termination Conditions:

-   A solution is found within the depth limit.
-   No solution exists within the given depth limit.

#### Advantages of DLS:

-   **Memory Efficient:** Like DFS ($O(b \times L)$).
-   **Terminates:** Avoids the infinite path problem of DFS (if L is finite).

#### Disadvantages of DLS:

-   **Incompleteness:** If the shallowest solution is *deeper* than the depth limit `L`, DLS will **fail** to find it.
-   **Non-Optimal:** Like DFS, it doesn't guarantee finding the optimal solution, even if multiple solutions exist within the limit.
-   **Choosing L:** Difficult to choose the right depth limit `L`.
    -   If `L` is too small (less than depth `d` of shallowest goal), it's incomplete.
    -   If `L` is too large (more than `d`), execution time increases unnecessarily.

### 4. Iterative Deepening Depth-First Search (IDDFS)

*(Insert images from pages 73, 74, 75, 79, 80 here)*

-   **Strategy:** Combines the benefits of BFS (completeness, optimality for uniform cost) and DFS (memory efficiency). It repeatedly runs DLS with **iteratively increasing depth limits**.
-   **Process:**
    1.  Run DLS with limit L=0.
    2.  If no solution, run DLS with limit L=1.
    3.  If no solution, run DLS with limit L=2.
    4.  ...and so on, until a goal is found.
-   The search stops when the depth limit `d` reaches the depth of the **shallowest goal node**.

![[Pasted image 20250502001207.png]]
shows IDDFS iterations: L=0 (A), L=1 (A,B,C), L=2 (A,B,D,E, C,F,G - Goal G found))

![[Pasted image 20250502001236.png]]
show iterations of IDDFS on a binary tree for limits 0, 1, 2, 3)

#### Advantages of IDDFS:

-   **Combines Benefits:** Inherits the **memory advantage** of DFS ($O(b \times d)$) and the **completeness and optimality** (for uniform cost) of BFS.
-   Generally preferred when the search space is large and the depth of the solution is unknown.

#### Disadvantages of IDDFS:

-   **Repeated Work:** The main drawback is that it **repeats** the work of previous phases (iterations). Nodes in the upper parts of the tree are expanded multiple times.
    -   *Mitigation:* This repetition is usually not as costly as it seems, especially in trees with high branching factors, as most nodes are at the deepest level. The overhead is generally considered acceptable for the benefits gained.

### Uninformed Search Examples

#### Blocks World

![[Pasted image 20250502001525.png]]

-   **World:** Flat surface (table), identical blocks (identified by letters), blocks can be stacked infinitely high.
-   **Goal:** Rearrange blocks from a start configuration to a goal configuration.

#### BFS traversal for a specific Blocks World problem

![[Pasted image 20250502001541.png]]

#### DFS for World blocks problem
![[Pasted image 20250502001631.png]]

#### Robot Block World
![[Pasted image 20250502001730.png]]
![[Pasted image 20250502001742.png]]
![[Pasted image 20250502001749.png]]

#### Romania Problem (Revisited)

![[Pasted image 20250502001814.png]]

 
 Applying BFS/DFS/DLS/IDS to find a path from Arad to Bucharest. Sequence of visited nodes would differ based on the strategy. 
 
![[Pasted image 20250502001835.png]]
#### 8-Puzzle (Revisited)

##### Using BFS
![[Pasted image 20250502002006.png]]

##### Using IDDS
![[Pasted image 20250502001933.png]]

---

## Informed (Heuristic) Search Strategies

### Overview

-   **Informed Search:** Uses **problem-specific knowledge** beyond the basic problem definition to guide the search more efficiently.
-   This knowledge is captured in a **heuristic function**.
-   **Goal:** Find solutions more efficiently (often faster, examining fewer nodes) than uninformed strategies.

### Best-First Search

![[Pasted image 20250502002157.png]]
shows steps of a generic Best-First Search


-   **Core Idea:** Use an **evaluation function $f(n)$** for each node `n` to estimate its "desirability".
-   **Strategy:** Expand the node `n` that has the **smallest $f(n)$ value** first.
-   $f(n)$ provides an estimate of the cost (or desirability) of a path going through node `n`.
-   **Implementation:** Typically uses a priority queue for the frontier, ordered by $f(n)$.


![[Pasted image 20250502002225.png]]
shows finding the shortest path S->G using costs)

![[Pasted image 20250502002250.png]]
shows another example graph

-   **Special Cases:** Different choices for the evaluation function $f(n)$ lead to specific algorithms:
    1.  **Greedy Best-First Search**
    2.  **A\* Search** (and others like AO\*)

### 1. Greedy Best-First Search

-   **Strategy:** Tries to expand the node that appears to be **closest to the goal**, assuming this will lead to a solution quickly.
-   **Evaluation Function:** Uses only the **heuristic function $h(n)$**; that is, **$f(n) = h(n)$**.
-   **Heuristic Function $h(n)$:** An estimate of the cost from node `n` to the nearest goal state.
    -   Provides an informed way to guess which neighbor might lead to a goal.
    -   Lower $h(n)$ implies the node is estimated to be closer to the goal.
-   **"Greedy" Name:** At each step, it greedily tries to get as close to the goal as possible based *only* on the estimated cost *to* the goal, ignoring the cost *already incurred* to reach the node.

![[Pasted image 20250502002425.png]]
![[Pasted image 20250502002437.png]]
shows an example: S->D (h=5 is lower than A's h=9), D->E (h=3 is lower than B's h=4), E->G (h=0). Path: S->D->E->G)

![[Pasted image 20250502002501.png]]
shows another example: Start A, Goal E. Path A->C->E based on heuristic values)

![[Pasted image 20250502002510.png]]
shows S->B->F->G based on lowest h(n) values)

#### Example: Romania Problem with Straight-Line Distance (SLD) Heuristic

-   **Heuristic $h_{SLD}(n)$:** Straight-line distance from city `n` to the goal city (Bucharest).
Straight line distances as an admissible heuristic as they will never overestimate the cost to the goal. This is because there is no shorter distance between two cities than the straight line distance.
![[Pasted image 20250502002703.png]]
![[Pasted image 20250502002714.png]]

-   **Search Steps (Greedy Best-First using $h_{SLD}$):**
![[Pasted image 20250502002730.png]]
    1.  **Initial State:** Arad (h=366)
    2.  **Expand Arad:** Neighbors are Sibiu (h=253), Timisoara (h=329), Zerind (h=374). Choose **Sibiu** (lowest h).
    3.  **Expand Sibiu:** Neighbors are Arad (h=366), Fagaras (h=176), Oradea (h=380), Rimnicu Vilcea (h=193). Choose **Fagaras** (lowest h).
    4.  **Expand Fagaras:** Neighbors are Sibiu (h=253), Bucharest (h=0). Choose **Bucharest** (Goal!).
-   **Resulting Path:** Arad -> Sibiu -> Fagaras -> Bucharest (Cost = 140 + 99 + 211 = 450)

#### Advantages of Greedy Best-First Search:

-   Can be much faster than uninformed search if the heuristic is good.

#### Disadvantages of Greedy Best-First Search:

-   **Not Optimal:** Does *not* guarantee finding the lowest-cost path. It can be led down a path that looks promising initially but becomes very costly later.
    -   *Romania Example:* The path found (450) is *not* the shortest. Arad -> Sibiu -> Rimnicu Vilcea -> Pitesti -> Bucharest is shorter (140 + 80 + 97 + 101 = 418). 
-   **Incomplete:** Can get stuck in loops (if not checking visited states) or follow infinite paths. Similar to DFS in behavior if it goes down a wrong path guided by a misleading heuristic.
-   Can behave like an unguided DFS in the worst case.

### 2. A\* Search ("A-Star")


-   **Strategy:** Combines the strengths of Uniform Cost Search (which minimizes cost so far) and Greedy Best-First Search (which minimizes estimated cost to goal). It aims to find the **cheapest solution path**.
-   **Evaluation Function:** **$f(n) = g(n) + h(n)$**
    -   **$g(n)$:** The **actual cost** of the path from the start state to node `n`.
    -   **$h(n)$:** The **estimated cost** (heuristic) of the cheapest path from node `n` to a goal state.
    -   **$f(n)$:** The **estimated cost** of the cheapest solution path that goes **through node $n$**.
-   **Goal:** Minimize the total estimated solution cost. Expands the node with the lowest $f(n)$ value.
-   Widely known and commonly used best-first search algorithm.

![[Pasted image 20250502002831.png]]
shows the breakdown of f(n) = g(n) + h(n))


#### A\* Example Walkthrough (Page 117, 118)

![[Pasted image 20250502002856.png]]
showing graph with costs and heuristic values (implicitly defined by node labels, e.g., A=10). Goal is implied, likely lowest heuristic value.)
(Let's assume Goal is J, heuristic h(J)=0)
Let's redefine the numbers in circles as heuristic h(n) and edge weights as g(n) step costs.

![[Pasted image 20250502002927.png]]

#### Another Example
![[Pasted image 20250502002936.png]]
*Graph with S (h=7), A (h=9), B (h=4), C (h=2), D (h=5), E (h=3), G (h=0)*
*Start: S, Goal: G*

1.  **Expand S (g=0, h=7, f=7):**
    -   Neighbors: A (g=3, h=9, f=3+9=12), D (g=2, h=5, f=2+5=7)
    -   Frontier: { D(f=7), A(f=12) }
2.  **Expand D (g=2, h=5, f=7):** (Chosen as lowest f)
    -   Neighbors: B (g=2+1=3, h=4, f=3+4=7), E (g=2+4=6, h=3, f=6+3=9)
    -   Frontier: { B(f=7), E(f=9), A(f=12) }
3.  **Expand B (g=3, h=4, f=7):** (Chosen, tie-breaking or order dependent)
    -   Neighbors: C (g=3+2=5, h=2, f=5+2=7), E (g=3+1=4, h=3, f=4+3=7)
    -   Frontier: { C(f=7), E(f=7), E(f=9), A(f=12) } *(Note: two paths to E)*
4.  **Expand C (g=5, h=2, f=7):** (Chosen)
    -   Neighbors: G (g=5+4=9, h=0, f=9+0=9)
    -   Frontier: { E(f=7), E(f=9), G(f=9), A(f=12) }
5.  **Expand E (g=4, h=3, f=7):** (Chosen - the one reached via B with lower g-cost)
    -   Neighbors: G (g=4+3=7, h=0, f=7+0=7)
    -   Frontier: { G(f=7), E(f=9), G(f=9), A(f=12) }
6.  **Expand G (g=7, h=0, f=7):** (Chosen) -> **GOAL!**

-   **Resulting Path:** S -> D -> B -> E -> G
-   **Cost:** 7

#### Another Example

![[Pasted image 20250502003104.png]]
![[Pasted image 20250502003112.png]]

#### A* Applied to the romania problem
![[Pasted image 20250502003139.png]]
![[Pasted image 20250502003149.png]]
![[Pasted image 20250502003158.png]]




#### Advantages of A\* Search:

-   **Optimal:** Guarantees finding the **least-cost path** if the heuristic function $h(n)$ is **admissible** (and consistent, for optimal efficiency).
-   **Complete:** Guaranteed to find a solution if one exists (assuming finite branching factor and positive step costs).
-   Often the **best algorithm** in terms of finding optimal solutions efficiently compared to other search methods.

#### Disadvantages of A\* Search:

-   **Memory Requirement:** Still keeps all generated nodes in memory (in the frontier/priority queue and potentially an explored set). Can be memory-intensive for large-scale problems ($O(b^d)$ in worst case).
-   **Complexity:** Performance depends heavily on the quality of the heuristic. While better than uninformed search, can still be computationally expensive.
-   **does not always produce shortest path** as it mostly based on heuristics and approximation.

#### Applications:

-   Traffic Navigation Systems (GPS)
-   Pathfinding in games and robotics
-   Underwater obstacle avoidance (USV)
-   Many optimization and planning problems.

### Admissibility and Consistency of Heuristics


These properties are crucial for the optimality of A\* search.

1.  **Admissibility:**
    -   **Definition:** A heuristic $h(n)$ is **admissible** if it **never overestimates** the true cost to reach the nearest goal state from node $n$.
    -   **Formula:** $h(n) \le h^*(n)$, where $h^*(n)$ is the *true* cost of the optimal path from $n$ to a goal.
    -   **Importance:** If $h(n)$ is admissible, A\* search using $f(n) = g(n) + h(n)$ is **optimal**.
    -   *Example:* Straight-line distance ($h_{SLD}$) is admissible for route finding because the straight line is the shortest possible distance.

2.  **Consistency (Monotonicity):**
    -   **Definition:** A heuristic $h(n)$ is **consistent** if, for every node $n$ and every successor $n'$ generated by action $a$, the estimated cost of reaching the goal from $n$ is no greater than the step cost $c(n, a, n')$ plus the estimated cost of reaching the goal from $n'$.
    -   **Formula (Triangle Inequality):** $h(n) \le c(n, a, n') + h(n')$.
    -   **Importance:** If $h(n)$ is consistent, A\* search is optimally efficient (guaranteed not to re-expand nodes with a shorter path found later). Also, if $h(n)$ is consistent, it is also admissible (assuming $h(goal)=0$).
    -   *Intuition:* The heuristic values should not decrease more than the cost of the step taken to get there.

-   **Heuristics as "Rules of Thumb":** Educated guesses, intuitive judgments, common sense used to guide search. 
![[Pasted image 20250502003406.png]]
### Heuristics for Example Problems

#### 8-Puzzle Heuristics (Page 143)

![[Pasted image 20250502003437.png]]

*State (N):*
```
5   8
4 2 1
7 3 6
```
*Goal State:*
```
1 2 3
4 5 6
7 8
```

1.  **$h_1(N)$ = Number of Misplaced Tiles:**
    -   Count tiles not in their goal position (excluding blank).
    -   In the example: Tiles 5, 8, 4, 2, 1, 3, 6 are misplaced (7 is correct). $h_1(N) = 7$. *(Note: Image calculation $h_1=6$ might be using a different example state or made an error).*
    -   *Admissible:* Yes, because each misplaced tile must be moved at least once.

2.  **$h_2(N)$ = Sum of Manhattan Distances:**
    -   For each tile (excluding blank), calculate the **Manhattan distance** (number of horizontal + vertical steps) from its current position to its goal position. Sum these distances.
    -   *Manhattan Distance:* $|x_1 - x_2| + |y_1 - y_2|$. 
- ![[Pasted image 20250502012139.png]]
    -   *Example Calculation (based on image):*
        -   Tile 5: (0,0) -> (1,1) = |0-1|+|0-1|=2
        -   Tile 8: (0,2) -> (2,1) = |0-2|+|2-1|=3
        -   Tile 4: (1,0) -> (1,0) = 0
        -   Tile 2: (1,1) -> (0,1) = |1-0|+|1-1|=1
        -   Tile 1: (1,2) -> (0,0) = |1-0|+|2-0|=3
        -   Tile 7: (2,0) -> (2,0) = 0
        -   Tile 3: (2,1) -> (0,2) = |2-0|+|1-2|=3
        -   Tile 6: (2,2) -> (1,2) = |2-1|+|2-2|=1
        -   $h_2(N) = 2 + 3 + 0 + 1 + 3 + 0 + 3 + 1 = 13$.
    -   *Admissible:* Yes, because each move can only reduce the Manhattan distance of one tile by one. It never overestimates the number of moves required.
    -   *Dominance:* $h_2$ generally provides a better estimate than $h_1$ and leads to more efficient A\* search.


#### 8-Queens Heuristic (Page 148)

*(Insert image from page 148)*

-   **$h(N)$ = Number of pairs of queens attacking each other** (directly or indirectly).
-   **Goal:** Find a state where $h(N) = 0$.
-   This heuristic is often used in **local search** algorithms like hill climbing for N-Queens.
-   *Example Calculation (from image):* $h=17$ for the state shown (count all attacking pairs).

---

## AO\* Algorithm (AND-OR Graphs)

*(Insert images from pages 59, 96, 128, 129, 130, 131, 132, 133, 134, 135, 136, 137, 216, 217, 218, 229 here)*

### Concept

-   Used for problems that can be decomposed into **subproblems**.
-   Represents the problem using an **AND-OR graph**.
    -   **OR nodes:** Represent choices between different ways (subproblems) to solve the main problem. (Standard nodes in state space search).
    -   **AND nodes:** Represent the need to solve *all* connected subproblems to solve the parent problem. Often shown using an arc connecting the links.
-   AO\* performs a **heuristic search** on these graphs.

![[Pasted image 20250502003547.png]]
Goal "want to eat food" can be solved by OR{ order from restaurant, (AND{ purchase ingredients, cook }), steal food (not shown but possible)} 

![[Pasted image 20250502003559.png]]
Goal "Acquire TV set" -> OR{ Steal TV, (AND{ Earn money, Buy TV}) } 

### Algorithm Idea

-   Similar to A\*, uses $f(n) = g(n) + h(n)$.
-   Handles the AND links by summing costs/heuristics appropriately.
-   Propagates costs and revises estimates upwards from solved/explored nodes.
-   It searches for a **solution graph** (a subgraph that demonstrates a solution) rather than just a single path.

### Working of AO* Algorithm
The AO* algorithm works on the formula given below :  
**f(n) = g(n) + h(n)**  
where,

- g(n): The actual cost of traversal from initial state to the current state.
- h(n): The estimated cost of traversal from the current state to the goal state.
- f(n): The actual cost of traversal from the initial state to the goal state.

Now, to get a better idea of the AO* algorithm lets take a look at an example.  
Example-
![[Pasted image 20250502004039.png]]
Here, in the above example all numbers in brackets are the heuristic value i.e h(n). Each edge is considered to have a value of 1 by default.

**Step-1**  
Starting from node A, we first calculate the best path.  
f(A-B) = g(B) + h(B) = 1+4= 5 , where 1 is the default cost value of travelling from A to B and 4 is the estimated cost from B to Goal state.  
f(A-C-D) = g(C) + h(C) + g(D) + h(D) = 1+2+1+3 = 7 , here we are calculating the path cost as both C and D because they have the AND-Arc. The default cost value of travelling from A-C is 1, and from A-D is 1, but the heuristic value given for C and D are 2 and 3 respectively hence making the cost as 7.
![[Pasted image 20250502004106.png]]
The minimum cost path is chosen i.e A-B.

**Step-2**  
Using the same formula as step-1, the path is now calculated from the B node,  
f(B-E) = 1 + 6 = 7.  
f(B-F) = 1 + 8 = 9  
Hence, the B-E path has lesser cost. Now the heuristics have to be updated since there is a difference between actual and heuristic value of B. The minimum cost path is chosen and is updated as the heuristic , in our case the value is 7. And because of change in heuristic of B there is also change in heuristic of A which is to be calculated again.  
f(A-B) = g(B) + updated((h(B)) = 1+7=8

![[Pasted image 20250502004115.png]]
**Step-3**  
Comparing path of f(A-B) and f(A-C-D) it is seen that f(A-C-D) is smaller. Hence f(A-C-D) needs to be explored.  
Now the current node becomes C node and the cost of the path is calculated,  
f(C-G) = 1+2 = 3  
f(C-H-I) = 1+0+1+0 = 2  
f(C-H-I) is chosen as minimum cost path,also there is no change in heuristic since it matches the actual cost. Heuristic of path of H and I are 0 and hence they are solved, but Path A-D also needs to be calculated , since it has an AND-arc.  
f(D-J) = 1+0 = 1, hence heuristic of D needs to be updated to 1. And finally the f(A-C-D) needs to be updated.  
f(A-C-D) = g(C) + h(C) + g(D) + updated((h(D)) = 1+2+1+1 =5.

![[Pasted image 20250502004124.png]]
As we can see that the solved path is f(A-C-D).

### AO\* Examples

Arcs indicate AND nodes.
-   The algorithm explores paths, calculates f-costs, and revises node costs based on children.
-   For an AND node, the cost is the sum of costs of all children + costs of the links.
-   For an OR node, the cost is the minimum cost among its children.
-   The process involves marking nodes as solved and propagating cost revisions upwards.

#### Example 1
![[Pasted image 20250502003632.png]]
![[Pasted image 20250502003640.png]]
![[Pasted image 20250502003651.png]]


![[Pasted image 20250502003731.png]]
provides corrections for Example #1 analysis: Correct revised costs are calculated based on updated children costs

#### Example 2 
![[Pasted image 20250502003815.png]]
![[Pasted image 20250502003822.png]]

#### Example 3 
![[Pasted image 20250502003839.png]]
![[Pasted image 20250502003846.png]]


## What is the difference between A* Algorithm and AO* algorithm?

- A* algorithm provides with the optimal solution, whereas AO* stops when it finds any solution.
- AO* algorithm requires lesser memory compared to A* algorithm.
- AO* algorithm doesn't go into infinite loop whereas the A* algorithm can go into an infinite loop.
---

You are absolutely right! My apologies, I seem to have overlooked generating the dedicated section for the Monkey and Banana Problem despite it being present in the slides.

Here is the formatted and enriched section for the Monkey and Banana Problem, ready to be inserted into your Obsidian notes, likely within the "Example Problems" section or as a standalone example.

## Monkey and Banana Problem


### Problem Description

This is a classic AI planning problem illustrating how an agent can form a sequence of actions to achieve a goal when intermediate steps are necessary.

-   **Setup:**
    -   A hungry monkey is in a room.
    -   Bananas are hanging from the center of the ceiling, out of reach.
    -   There is a box (or chair) in the room (e.g., initially at the window or some location).
    -   In some versions, a stick might also be available.
-   **Goal:** The monkey wants the bananas but cannot reach them directly.
-   **Task:** Determine the sequence of actions the monkey should take to get the bananas.

*(Page 150 Variant):* Monkey at the door, banana in the middle, box at the window.

### Actions Allowed 

1.  **Walk:** Move around on the floor.
2.  **Climb:** Climb *onto* the box. (Or Climb *off* the box).
3.  **Push:** Push the box around the room (only possible if the monkey is on the floor and at the box).
4.  **Grasp:** Grasp the bananas (only possible if the monkey is standing on the box *directly under* the bananas).
*(Alternative Actions - Stick Version in state diagram): Grab stick, Climb chair, Drop stick, Wave stick, Get off chair, Grab banana, Eat banana.*

### State Representation

![[Pasted image 20250502013423.png]]
A state can be defined by the locations and statuses of the objects:

-   `on(Agent, Location)`: Where the agent is (e.g., `on(monkey, floor)`, `on(monkey, box)`).
-   `at(Object, Location)`: Where objects are (e.g., `at(monkey, door)`, `at(box, window)`, `at(bananas, ceiling_middle)`).
-   `status(Object, Status)`: Status of objects (e.g., `status(bananas, hanging)`, `status(bananas, grabbed)`).
-   `has(Agent, Object)`: Whether the agent possesses an object (e.g., `has(monkey, stick)` - in stick version).

#### Initial State:

-   `on(monkey, floor)`
-   `on(box, floor)`
-   `at(monkey, a)` *(Assuming 'a' is a location like 'door')*
-   `at(box, b)` *(Assuming 'b' is a location like 'window')*
-   `at(bananas, c)` *(Assuming 'c' is 'ceiling_middle')*
-   `status(bananas, hanging)`

#### Goal State:

-   The monkey must have the bananas. The exact state depends on what happens after grabbing. A common goal state is simply `has(monkey, bananas)` or:
-   `on(monkey, box)`
-   `on(box, floor)`
-   `at(monkey, c)`
-   `at(box, c)`
-   `at(bananas, c)` *(Location doesn't change, but status does)*
-   **`status(bananas, grabbed)`**

### Problem Formulation (as State Space Search)

1.  **States:** Defined by the positions of the monkey and box, and whether the monkey has the bananas (and potentially the status/location of the bananas and stick).
2.  **Initial State:** As defined above (e.g., monkey at door, box at window, monkey on floor, bananas hanging).
3.  **Actions:** {Walk(to_location), Push(box, to_location), Climb_on_box, Climb_off_box, Grasp_bananas}. Actions are only applicable under certain conditions (e.g., must be at box to push, must be on box under bananas to grasp).
4.  **Transition Model:** Defines how actions change the state variables (e.g., `Walk(L)` changes `at(monkey, X)` to `at(monkey, L)`; `Climb_on_box` changes `on(monkey, floor)` to `on(monkey, box)` if `at(monkey, Loc)` and `at(box, Loc)`).
5.  **Goal Test:** Is `status(bananas, grabbed)` true? (Or `has(monkey, bananas)`).
6.  **Path Cost:** Usually, each action costs 1. The aim is to find *any* valid sequence, often optimality isn't the primary focus for this illustrative problem.

### Solution Sequence (Conceptual)

A likely sequence involves:
1.  Walk to the box.
2.  Push the box under the bananas.
3.  Climb onto the box.
4.  Grasp the bananas.

### State Diagram
![[Pasted image 20250502013526.png]]

## Local Search Algorithms

### Core Idea

-   Used for **optimization problems** where the **path to the goal does not matter**, only the final state itself.
-   Operate using a **single current node** and generally move only to its **neighbours**.
-   Do **not** typically retain paths followed.
-   Often used for computationally hard problems where systematic search is infeasible.

*(Analogy: Trying to find the highest peak in a mountain range by only looking at your immediate surroundings and always moving uphill.)*

### Advantages

-   **Low Memory Usage:** Use very little memory (often constant amount) as they don't store paths or large frontiers.
-   **Scalability:** Can often find **reasonable solutions** in **large or infinite (continuous)** state spaces where systematic algorithms fail.

### Disadvantages

-   **Not Systematic:** They don't explore the whole search space methodically.
-   **Not Complete:** May not find a solution even if one exists.
-   **Not Optimal:** Often find local optima rather than the global optimum.

### Applications

-   AI (Optimization, Scheduling)
-   Mathematics
-   Operations Research
-   Engineering
-   Bioinformatics

### State-Space Landscape 

![[Pasted image 20250502004251.png]]

-   Visualize the search space as a landscape:
    -   **Location:** Defined by the state.
    -   **Elevation:** Defined by the value of the **Objective Function** (to be maximized) or **Heuristic Cost Function** (to be minimized).
-   **Goal:** Find the state with the maximum elevation (global maximum) or minimum elevation (global minimum).

#### Landscape Features 

-   **Local Maximum:** A state better (higher value) than all its neighbours, but not necessarily the best overall.
-   **Global Maximum:** The best possible state in the entire landscape (highest value).
-   **Plateau / Flat Local Maximum:** A flat region where neighbouring states have the same value. Can be a local maximum if no uphill exit exists.
-   **Shoulder:** A plateau from which an uphill move is possible.
-   **Ridge:** A sequence of local maxima or a narrow elevated region, difficult for simple hill climbing to navigate.
-   **Current State:** The agent's current position on the landscape.

### Hill Climbing Search


-   **Algorithm:** A simple local search technique.
    -   Start at an initial state.
    -   Repeatedly move to the **best neighbouring state** (the one with the highest value / lowest cost) until no neighbour improves upon the current state.
-   **Steepest-Ascent Version:** Chooses the neighbour with the *steepest* uphill move (greatest improvement).
-   **Characteristics:**
    -   Only looks at immediate neighbours.
    -   Does not maintain a search tree.
    -   Terminates when it reaches a "peak" (local maximum).
    -   *Analogy:* Trying to find the top of Mount Everest in a thick fog while suffering from amnesia. 

#### How it Works

1.Define the current state as an initial state 
2.Loop until the goal state is achieved or no more operators can be applied on the current state: 
1. Apply an operation to current state and **get a new state** 
2. **Compare** the new state with the goal 
3. **Quit** if the goal state is achieved 
4. Evaluate new state with heuristic function and **compare it with the current state** 
5. **If the newer state is closer** to the goal compared to current state, **update the current state**

#### Pseudocode
![[Pasted image 20250502004553.png]]

#### Disadvantages / Problems with Hill Climbing (Pages 164, 165)

1.  **Local Maxima:** Gets stuck on peaks that are not the global maximum. Once reached, no neighbour offers improvement, so the search terminates prematurely.
2.  **Ridges:** Difficult to navigate; movement along the ridge top might be required, but moves off the ridge might be downhill. The sequence of local maxima along a ridge can trap the algorithm.
3.  **Plateaux:** If the region is flat, the algorithm doesn't know where to go next. Can lead to wandering or premature termination (on flat local maxima).

![[Pasted image 20250502004627.png]]

#### Hill Climbing Examples

-   **N-Queens:**
- ![[Pasted image 20250502004757.png]]
    -   *Objective Function:* Minimize the number of conflicting pairs ($h(n)$ from page 148). Goal: $h=0$.
    -   *Neighbours:* States generated by moving a single queen to another square in the same column.
    -   Start with a random configuration, move queens to reduce conflicts until a local minimum (possibly $h=0$) is reached.
-   **8-Puzzle (Pages 231, 232, 234):**
 ![[Pasted image 20250502004812.png]]
shows a successful solution path



 ![[Pasted image 20250502004832.png]]
 shows getting stuck at a local maximum where $h=11$ or $h=12$, but $h=0$ is the goal
 
-   *Objective Function:* Minimize a heuristic like Manhattan distance. Goal: $h=0$.
    -   *Neighbours:* States reachable by one valid move of the blank tile.


#### Hill Climbing Properties 

-   **Not Complete**
-   **Not Optimal**
-   **Why Use?**
    -   Low memory requirements.
    -   Effective for finding *good enough* solutions in extremely large state spaces.
    -   Variants (Random restarts, Simulated Annealing, etc.) can mitigate drawbacks.

#### Comparing Hill Climbing vs Best-First Search

Hill-climbing and greedy algorithms are both heuristics that can be used for optimization problems. 

In a **hill-climbing** heuristic, you start with an initial solution. Generate one or more neighboring solutions. Pick the best and continue until there are no better neighboring solutions. This will generally yield one solution. In hill-climbing, we need to know how to evaluate a solution, and how to generate a "neighbor."

In a **greedy** heuristic, we need to know something special about the problem at hand. A greedy algorithm uses information to produce a single solution. 

In **BFS**, it's about **finding the goal**. So it's about picking the best node (the one which we hope will take us to the goal) among the possible ones. We keep trying to go towards the goal. 

But in **hill climbing**, it's about maximizing the target function (i.e., **minimising heuristic cost**). We pick the node which provides the highest ascent. So **unlike BFS, the 'value' of the parent node is also taken into account**. If we can't go higher, we just give up. In that case we may not even reach the goal. We might be at a local maxima.

![[Pasted image 20250502005129.png]]

---

## Constraint Satisfaction Problems (CSP)

### Core Idea

-   A class of problems where the goal is to find a state (an assignment of values to variables) that **satisfies a given set of constraints**.
-   Focus is on finding *any* valid solution, often path doesn't matter.

- **Variables:** A set of variables $V_1, ..., V_n$.
- **Domains:** For each variable $V_i$, a domain $Dom[V_i]$ of possible values.
- **Constraints:** A set of constraints $C_1, ..., C_m$ specifying allowable combinations of values for subsets of variables.
- **Solution:** An **assignment** of a value from its domain to every variable, such that **all constraints are satisfied**.

### CSP Formulation 

-   **Operates in the space of constraint sets** or partial assignments.
-   **Initial State:** Problem description constraints / Empty assignment.
-   **Goal State:** Any state (assignment) where all constraints are satisfied / Assignment is complete and consistent.
-   **Successor Function:** Assign a value to an unassigned variable, ensuring consistency with currently assigned variables.
-   **Path Cost:** Typically irrelevant.

### CSP Process 

1.  Discover and **propagate constraints** as far as possible.
2.  If needed, **search** (often using backtracking) by hypothesizing assignments and checking constraints.

### Example: Cryptarithmetic Puzzles

![[Pasted image 20250502005355.png]]
![[Pasted image 20250502005402.png]]
![[Pasted image 20250502005408.png]]

#### Example
![[Pasted image 20250502005417.png]]
![[Pasted image 20250502005615.png]]

#### Example 
![[Pasted image 20250502005448.png]]


#### Example 
![[Pasted image 20250502005456.png]]
![[Pasted image 20250502005636.png]]

#### Example
![[Pasted image 20250502005504.png]]
![[Pasted image 20250502005644.png]]

-   **Problem:** Assign unique digits (0-9) to letters such that an arithmetic equation holds true.
-   **Example: `TO + GO = OUT`** (Page 167-169)
    -   **Variables:** T, O, G, U
    -   **Domain:** {0, 1, 2, ..., 9}
    -   **Constraints:**
        -   Each letter has a unique digit value (Alldiff(T,O,G,U)).
        -   Sum must hold: `O + O = T + 10*C1`, `T + G + C1 = U + 10*C2`, `C2 = O` (where C1, C2 are carries).
        -   Leading digits cannot be zero (T≠0, G≠0, O≠0). *(Note: O=0 is often allowed if not leading final sum)*
    -   *(Page 168 shows a derivation assuming O=1 because it's the carry-out C2. Solution: T=7, O=2, G=8, U=5 -> 72+82=154 - Error in slide derivation? Let's re-evaluate based on standard rules)*
    -   *Standard derivation `TO+GO=OUT`:*
        - O must be C2 (carry out from T+G). If T,G ≤ 9, C1 ≤ 1, then T+G+C1 ≤ 9+9+1 = 19. So U can be 0-9, C2 can be 0 or 1. O = C2.
        - O cannot be 0 (usually leading digits aren't 0, applies to O in OUT). So **O=1**.
        - C2 = 1.
        - T + G + C1 = U + 10 * 1 => T+G+C1 = U+10
        - O + O = T + 10 * C1 => 1 + 1 = T + 10*C1 => 2 = T + 10*C1. Since T must be a digit, C1 must be 0, so **T=2**.
        - Now, T+G+C1 = U+10 => 2+G+0 = U+10 => G = U+8.
        - Variables left: G, U. Digits used: {1, 2}. Remaining: {0, 3, 4, 5, 6, 7, 8, 9}.
        - Need G=U+8. Possible pairs (G,U): (8,0), (9,1). Since O=1, U cannot be 1. So **U=0, G=8**.
        - **Solution:** T=2, O=1, G=8, U=0. Check: `21 + 81 = 102`. (OUT = 102). Valid.
        - *(Page 169 solution: T=7, O=9, G=8, U=3 -> 79+89=168 -> OUT=168? Conflicting examples/solutions provided).* Let's stick to the definition.
-   **Example: `TWO + TWO = FOUR`** (Page 170, 171) Solution: 765 + 765 = 1530. (T=7, W=6, O=5, F=1, U=3, R=0). 
-   **Example: `SEND + MORE = MONEY`** 

### Example: Map Coloring


-   **Problem:** Assign colors to regions on a map such that no two adjacent regions have the same color.
-   **CSP Formulation:**
- ![[Pasted image 20250502005728.png]]
    -   **Variables:** Regions (WA, NT, Q, NSW, V, SA, T).
    -   **Domain:** {red, green, blue}.
    -   **Constraints:** Adjacent regions must have different colors.
        -   e.g., `WA ≠ NT`, `WA ≠ SA`, `NT ≠ SA`, `NT ≠ Q`, `SA ≠ Q`, `SA ≠ NSW`, `SA ≠ V`, `Q ≠ NSW`, `NSW ≠ V`.
    -   *(Constraint Graph - Page 178: Nodes are variables, edges represent constraints between adjacent regions)*.
#### Map Colouring Full Example

![[Pasted image 20250502005820.png]]
![[Pasted image 20250502005828.png]]
![[Pasted image 20250502005834.png]]
![[Pasted image 20250502005841.png]]
![[Pasted image 20250502005848.png]]
![[Pasted image 20250502005853.png]]


### Solving CSPs: Backtracking Search

-   A common algorithm for CSPs. It's a form of **depth-first search**.
-   **Idea:** Assign values to variables one by one. If an assignment violates a constraint, **backtrack** to the previous variable and try a different value.
-   **Process:**
    1.  Select an unassigned variable.
    2.  Try assigning a value from its domain.
    3.  Check if the assignment is consistent with all constraints involving currently assigned variables.
    4.  If consistent, recurse to assign the next variable.
    5.  If inconsistent, or if recursion returns failure, try the next value for the current variable.
    6.  If no values work for the current variable, return failure (triggering backtrack).

![[Pasted image 20250502010002.png]]

### Improving Backtracking Efficiency

-   **Variable Ordering:**
    -   **Minimum Remaining Values (MRV) / Most Constrained Variable:** Choose the variable with the *fewest* legal values remaining in its domain. 
    - ![[Pasted image 20250502010020.png]]
    - ![[Pasted image 20250502010045.png]]
    -   **Most Constraining Variable / Degree Heuristic:** Choose the variable involved in the *most* constraints on *unassigned* variables (used as a tie-breaker).
-   **Value Ordering:**
    -   **Least Constraining Value:** Prefer the value that *rules out the fewest* choices for neighboring variables in the constraint graph.
    - ![[Pasted image 20250502010134.png]]
-   **Constraint Propagation:** Inferring consequences of assignments to reduce search space.
    -   **Forward Checking:** When a variable X is assigned, check each unassigned variable Y connected to X by a constraint. Delete any values from Y's domain inconsistent with the assignment to X. If any variable's domain becomes empty, backtrack immediately.
    - Example - 4 Queens
    - ![[Pasted image 20250502010219.png]]
    - ![[Pasted image 20250502010231.png]]
    - ![[Pasted image 20250502010258.png]]
    - ![[Pasted image 20250502010303.png]]
    - ![[Pasted image 20250502010310.png]]
    - ![[Pasted image 20250502010316.png]]
    - ![[Pasted image 20250502010321.png]]
    - ![[Pasted image 20250502010335.png]]
    - ![[Pasted image 20250502010341.png]]
    - ![[Pasted image 20250502010346.png]]
    - ![[Pasted image 20250502010352.png]]
    - ![[Pasted image 20250502010359.png]]
    - ![[Pasted image 20250502010407.png]]

Example - Map Coloring for Forward Checking

![[Pasted image 20250502010500.png]]
![[Pasted image 20250502010511.png]]
![[Pasted image 20250502010521.png]]
![[Pasted image 20250502010528.png]]


-   **Arc Consistency:** Stronger than forward checking. An arc X -> Y is consistent if, for *every* value x in X's domain, there is *some* allowed value y in Y's domain. Make all arcs consistent. Can detect failures earlier. 

Arc Consistency for Map Coloring
![[Pasted image 20250502010602.png]]
![[Pasted image 20250502010608.png]]
![[Pasted image 20250502010614.png]]
![[Pasted image 20250502010620.png]]

### Real-World CSP Applications

-   Assignment problems (e.g., Who teaches which class?)
-   Timetabling (e.g., Exam schedules, course scheduling)
-   Transportation scheduling
-   Floor planning
-   Factory scheduling
-   Hardware configuration (finding compatible components)
-   Sudoku, Crosswords 
![[Pasted image 20250502010707.png]]
![[Pasted image 20250502010715.png]]

-   Latin Square Problem **
![[Pasted image 20250502010723.png]]
---

## Genetic Algorithms (GA)

### Core Idea

-   A variant of **stochastic local search** (or population-based search) inspired by **biological evolution**.
-   Simulates **Darwinian selection** ("survival of the fittest").
-   Maintains a **population** of candidate solutions (states, individuals, chromosomes).
-   Successor states are generated by **combining two parent states** (crossover) and introducing random changes (mutation).

![[Pasted image 20250502010742.png]]

### Biological Analogy

-   **Population:** Set of individuals (potential solutions).
-   **Chromosome:** Representation of an individual solution (e.g., a bit string, a sequence of numbers).
-   **Gene:** A part of the chromosome (e.g., a single bit, a number).
-   **Fitness:** How "good" a solution is, according to a **fitness function**.
-   **Selection:** Fitter individuals are more likely to be chosen to reproduce.
-   **Crossover:** Combines genetic material from two parents to create offspring.
-   **Mutation:** Random small changes in an individual's chromosome.

### Phases of a Genetic Algorithm 

1.  **Initial Population:** Generate a set of random individuals (solutions).
2.  **Fitness Function:** Evaluate the competing ability (fitness score) of each individual. Higher score usually means better solution and higher probability of selection.
3.  **Selection:** Select the fittest individuals to pass their genes to the next generation. Probability of selection is often proportional to fitness.
4.  **Crossover:**
    -   Randomly choose pairs of selected parents.
    -   Randomly choose a **crossover point** within the genes (chromosome).
    -   Create offspring by swapping the parts of the parent chromosomes after the crossover point.
5.  **Mutation:**
    -   Introduce small random changes (e.g., flip some bits in the bit string) to maintain genetic diversity and avoid getting stuck in local optima.
6.  **Termination:** Repeat steps 2-5 until the population converges (offspring are not significantly different from parents, or a satisfactory solution is found, or a generation limit is reached).
![[Pasted image 20250502010808.png]]


![[Pasted image 20250502010820.png]]
shows the overall GA loop: START -> Generate Pop -> Compute Fitness -> REPEAT { Selection -> Crossover -> Mutation -> Compute Fitness } UNTIL Converged -> STOP)

### Example: 8-Queens using GA

![[Pasted image 20250502010921.png]]
![[Pasted image 20250502010928.png]]
![[Pasted image 20250502010940.png]]


-   **State Representation (Chromosome):** A list of 8 digits (1-8), where the $i$-th digit represents the *row* of the queen in column $i$. *(Page 185: state 16257483 means queen in col 1 is row 1, col 2 is row 6, etc.)*
-   **Initial Population (a):** Generate random 8-digit strings (states).
-   **Fitness Function (b):** Number of **non-attacking pairs** of queens. Maximum possible is $8 \times 7 / 2 = 28$. Higher is better.
    -   *Calculation (Page 186):* For each queen, count pairs to its right that it does not attack. Sum these counts. (Example: 24748552 fitness = 23 = 6+5+4+3+3+2+0+0) *(Note: image calculation seems off, example state 32752411 fitness=23? Let's use 24748552 fitness=24)*
    -   *(Fitness 24 corresponds to state 24748552, Fitness 23 to 32752411, etc.)*
-   **Selection (c):** Select individuals based on fitness probability (e.g., higher fitness gets higher chance). Calculate probability: Fitness / Total Fitness. *(Page 189: 24 / (24+23+20+11) = 31%)* Pairs are chosen for mating (sometimes fitter individuals chosen multiple times).
-   **Crossover (d):** Choose a random crossover point. Swap tails of selected pairs to create offspring. *(Example: Parents 3275|2411 and 2474|8552, crossover at 4 -> Offspring 3275|8552 and 2474|2411)*
-   **Mutation (e):** Randomly change a digit (gene) in an offspring's chromosome. *(Example: 32748552 -> 32748152, changing position 6 from 5 to 1)*
-   **Repeat:** Create a new generation and repeat the process.

*(Page 191 shows another GA example with binary strings)*

---

## Adversarial Search (Games)

### Concept

-   Applies to problems where there is an "enemy" or **opponent** changing the state in a direction you might not want.
-   Common in **competitive, multiagent environments**, often modeled as **Games**.
-   Key challenge: Your actions depend on anticipating the opponent's actions.

### Common AI Game Type

-   **Deterministic:** No randomness in outcomes.
-   **Turn-taking:** Players alternate moves.
-   **Two-player:** MAX (our agent) vs. MIN (opponent).
-   **Zero-sum:** One player's gain is the other's loss. Total utility is constant.
-   **Perfect Information:** Both players know the complete state of the game (e.g., Chess, Go. *Not* Poker, Bridge).

### Games as Search Problems

Formal definition includes:

-   **S0 (Initial State):** Starting setup.
-   **PLAYER(s):** Function defining whose turn it is in state `s`.
-   **ACTIONS(s):** Legal moves in state `s`.
-   **RESULT(s, a):** Transition model (state after action `a` in state `s`).
-   **TERMINAL-TEST(s):** True if the game is over.
-   **UTILITY(s, p):** Payoff function defining the final numeric value of terminal state `s` for player `p`.
    -   *Chess Example:* +1 for win, 0 for draw, -1 for loss (for MAX).

-   **Game Tree:** Represents the possible game progressions. Nodes are states, edges are moves. . Can be enormous (Chess > $10^{40}$ nodes).
![[Pasted image 20250502011646.png]]

### Optimal Decisions in Games 

-   **Optimal Strategy:** A strategy that maximizes the player's utility assuming the opponent plays optimally to minimize it.
-   **Minimax Value:** The utility of a state assuming optimal play from both sides. Calculated recursively.

### Minimax Algorithm


-   **Goal:** Find the optimal strategy (best move) for MAX, assuming MIN plays optimally to minimize MAX's score.
-   **Approach:** Uses **Depth-First Search** to explore the game tree. Propagates utility values up from terminal nodes.
    -   **MAX nodes (∆):** Choose the action leading to the state with the **maximum** minimax value among children. 
    -   **MIN nodes (∇):** Choose the action leading to the state with the **minimum** minimax value among children. 
    - ![[Pasted image 20250502011715.png]]

-   **Recursion:** 
    -   `MINIMAX-VALUE(state)`:
        -   If `TERMINAL-TEST(state)`, return `UTILITY(state)`.
        -   If `PLAYER(state) == MAX`, return `max(MINIMAX-VALUE(RESULT(state, a)))` for all actions `a`.
        -   If `PLAYER(state) == MIN`, return `min(MINIMAX-VALUE(RESULT(state, a)))` for all actions `a`.

#### Minmax Pseudocode
![[Pasted image 20250502011747.png]]

#### Calculating Min Max Values
![[Pasted image 20250502011828.png]]
![[Pasted image 20250502011837.png]]
![[Pasted image 20250502011845.png]]
![[Pasted image 20250502011853.png]]

1.  Terminal nodes have utility values.
2.  Maximizer level (D, E, F, G) takes max of children: D=max(-1,4)=4, E=max(2,6)=6, F=max(-3,-5)=-3, G=max(0,7)=7.
3.  Minimizer level (B, C) takes min of children: B=min(4,6)=4, C=min(-3,7)=-3.
4.  Maximizer root (A) takes max of children: A=max(4,-3)=4. Optimal move for MAX is towards B.

#### Properties of Minimax

-   **Complete:** Yes, if the tree is finite.
-   **Optimal:** Yes, against an optimal opponent.
-   **Time Complexity:** $O(b^m)$ (Explores the entire tree).
-   **Space Complexity:** $O(bm)$ (For DFS exploration).
-   **Impractical:** Time cost is prohibitive for real games like chess.

### Alpha-Beta Pruning


-   **Goal:** Optimize the Minimax algorithm by **pruning** (eliminating) branches of the search tree that cannot influence the final decision.
-   **Core Idea:** Maintain two values during the search:
    -   **Alpha (α):** The best (highest) value found *so far* for MAX along the path to the root. Initialized to -∞.
    -   **Beta (β):** The best (lowest) value found *so far* for MIN along the path to the root. Initialized to +∞.
-   **Pruning Condition:** **α ≥ β**
    -   If this occurs at any MIN node, it means MAX already has a better choice (α) elsewhere, so MIN won't choose this path (as it leads to a value ≥ β). Prune remaining children of this MIN node.
    -   If this occurs at any MAX node, it means MIN already has a better choice (β) elsewhere, so MAX won't choose this path (as it leads to a value ≤ α). Prune remaining children of this MAX node.
-   **Updates:**
    -   MAX player updates α only.
    -   MIN player updates β only.
    -   α and β values are passed *down* to child nodes.

#### Example
![[Pasted image 20250502011945.png]]
![[Pasted image 20250502011954.png]]
![[Pasted image 20250502012001.png]]
![[Pasted image 20250502012008.png]]
![[Pasted image 20250502012014.png]]
![[Pasted image 20250502012022.png]]
![[Pasted image 20250502012028.png]]
![[Pasted image 20250502012035.png]]

1.  Start A: (α=-∞, β=+∞)
2.  Explore D via B:
    -   Pass (α=-∞, β=+∞) to B (MIN).
    -   Pass (α=-∞, β=+∞) to D (MAX).
    -   Visit D's child 2: α becomes max(-∞, 2) = 2.
    -   Visit D's child 3: α becomes max(2, 3) = 3. D returns 3.
3.  At B (MIN): Received 3 from D. β becomes min(+∞, 3) = 3. B's range is now (α=-∞, β=3).
4.  Explore E via B:
    -   Pass (α=-∞, β=3) to E (MAX).
    -   Visit E's child 5: α becomes max(-∞, 5) = 5.
    -   **Pruning Condition:** At E, α (5) ≥ β (3). MAX (at E) found a value 5, but MIN (at B) will never allow a value >= 3 (it already found 3 via D). So, MIN (B) will choose the path to D. We can **prune** the remaining children of E (node 9). E returns 5 (though B won't use it).
5.  At B (MIN): Received 5 from E. Value doesn't change β (min(3, 5) = 3). B returns 3.
6.  At A (MAX): Received 3 from B. α becomes max(-∞, 3) = 3. A's range is now (α=3, β=+∞).
7.  Explore F via C:
    -   Pass (α=3, β=+∞) to C (MIN).
    -   Pass (α=3, β=+∞) to F (MAX).
    -   Visit F's child 0: α remains max(3, 0) = 3.
    -   Visit F's child 1: α remains max(3, 1) = 3. F returns 3.
8.  At C (MIN): Received 3 from F. β becomes min(+∞, 3) = 3. C's range is now (α=3, β=3).
9.  Explore G via C:
    -   Pass (α=3, β=3) to G (MAX).
    -   Visit G's child 7: α becomes max(3, 7) = 7.
    -   **Pruning Condition:** At G, α (7) ≥ β (3). MAX (at G) found 7, but MIN (at C) will never allow a value >= 3 (it already found 3 via F). **Prune** remaining children of G (node 5). G returns 7.
10. At C (MIN): Received 7 from G. Value doesn't change β (min(3, 7) = 3). C returns 3.
11. At A (MAX): Received 3 from C. Value doesn't change α (max(3, 3) = 3). A returns 3.

-   **Result:** Final decision is 3 (via B -> D). Optimal move for MAX leads to B. Pruning eliminated exploring nodes 9 and 5.

![[Pasted image 20250502012058.png]]


#### Efficiency of Alpha-Beta

-   Returns the same move as Minimax.
-   Can potentially double the searchable depth or prune the tree significantly (roughly $O(b^{m/2})$ complexity in the optimal case). Effectiveness depends on move ordering (exploring best moves first maximizes pruning).

*(Page 308 provides a summary of game concepts, minimax, and alpha-beta)*

*(Extra examples and resources linked on pages 211-213, 215-219, 290)*

---

## Glossary of Terms

-   **A\* Search:** An informed search algorithm that finds the lowest-cost path using an evaluation function $f(n) = g(n) + h(n)$, where $g(n)$ is the actual cost from the start and $h(n)$ is an admissible heuristic estimate to the goal.
-   **Actions:** Operations an agent can perform to change from one state to another.
-   **Admissibility (Heuristic):** A property of a heuristic function where it *never overestimates* the true cost to reach the goal. Required for A\* optimality.
-   **Adversarial Search:** Search in a competitive environment where agents (opponents) have conflicting goals (e.g., games).
-   **Agent:** An entity that perceives its environment through sensors and acts upon that environment through actuators.
-   **Alpha (α):** In Alpha-Beta Pruning, the best (highest) value found so far for the MAX player along the current path.
-   **Alpha-Beta Pruning:** An optimization technique for the Minimax algorithm that prunes branches of the game tree that cannot influence the final decision.
-   **AND-OR Graphs:** Graphs used to represent problems decomposable into subproblems, where some require all subproblems to be solved (AND) and others offer choices (OR).
-   **AO\* Algorithm:** A heuristic search algorithm for finding solutions in AND-OR graphs.
-   **Backtracking Search:** A general algorithm for finding solutions, particularly in CSPs, by incrementally building a solution and abandoning paths (backtracking) as soon as they violate constraints.
-   **Best-First Search:** A general search strategy that expands the node deemed "best" according to an evaluation function $f(n)$.
-   **Beta (β):** In Alpha-Beta Pruning, the best (lowest) value found so far for the MIN player along the current path.
-   **Blind Search:** See **Uninformed Search**.
-   **Blocks World:** A classic AI planning domain involving stacking blocks on a table.
-   **Branching Factor (b):** The average number of successors (children) per node in a search tree.
-   **Breadth-First Search (BFS):** An uninformed search strategy that explores the search tree level by level. Complete and optimal for uniform costs, but memory-intensive.
-   **Chromosome:** In Genetic Algorithms, the representation of an individual solution.
-   **Completeness:** A property of a search algorithm guaranteeing it will find a solution if one exists.
-   **Consistency (Heuristic):** A property of a heuristic function where the estimated cost from a node `n` to the goal is less than or equal to the step cost to a successor `n'` plus the estimated cost from `n'` to the goal ($h(n) \le c(n, a, n') + h(n')$). Implies admissibility.
-   **Constraint Satisfaction Problem (CSP):** A problem defined by variables, their domains, and constraints on the values variables can take simultaneously. The goal is to find a valid assignment.
-   **Constraints:** Restrictions on the values that variables can take in a CSP.
-   **Control Strategy:** The part of a production system that decides which rule to apply next.
-   **Crossover:** An operator in Genetic Algorithms that combines parts of two parent chromosomes to create offspring.
-   **Cryptarithmetic Puzzle:** A puzzle where letters represent unique digits, and an arithmetic equation must be satisfied.
-   **Depth-First Search (DFS):** An uninformed search strategy that explores as deeply as possible along one path before backtracking. Memory-efficient but potentially incomplete and non-optimal.
-   **Depth-Limited Search (DLS):** A variant of DFS that stops exploring paths beyond a predetermined depth limit `L`. Avoids infinite loops but can be incomplete if `L` is too small.
-   **Domain:** The set of possible values a variable can take in a CSP.
-   **Evaluation Function (f(n)):** A function used in informed search to estimate the desirability or cost of a path going through node `n`.
-   **Fitness Function:** In Genetic Algorithms, a function that measures the quality or "goodness" of an individual solution (chromosome).
-   **Formulate, Search, Execute:** The design cycle for a problem-solving agent.
-   **Forward Checking:** A constraint propagation technique in CSPs where assigning a value to a variable triggers checking constraints with connected unassigned variables, potentially reducing their domains.
-   **Game Tree:** A tree representing all possible sequences of moves in a game.
-   **Gene:** In Genetic Algorithms, a component of a chromosome.
-   **Genetic Algorithm (GA):** A population-based search algorithm inspired by biological evolution, using selection, crossover, and mutation.
-   **Global Maximum/Minimum:** The best possible state (highest/lowest value) in the entire state-space landscape.
-   **Goal Formulation:** The process by which an agent decides on its desired state(s).
-   **Goal State:** A state that satisfies the problem's objective.
-   **Goal Test:** A function that determines if a given state is a goal state.
-   **Greedy Best-First Search:** An informed search strategy that expands the node with the lowest heuristic value $h(n)$, estimating closeness to the goal. Fast but not optimal or complete.
-   **Heuristic Function (h(n)):** A function that estimates the cost from the current state `n` to the nearest goal state. Used in informed search.
-   **Heuristic Search:** See **Informed Search**.
-   **Hill Climbing Search:** A local search algorithm that iteratively moves to the best neighbouring state until a local optimum (peak) is reached.
-   **Informed Search:** Search strategies that use problem-specific knowledge (heuristics) to guide the search process, generally more efficient than uninformed search.
-   **Initial State:** The state from which the search begins.
-   **Initial Population:** The starting set of random solutions in a Genetic Algorithm.
-   **Iterative Deepening Depth-First Search (IDDFS):** An uninformed search strategy that combines DFS's memory efficiency with BFS's completeness and optimality by running DLS with increasing depth limits.
-   **Knowledge Base:** Stores information (facts, rules, current state) used by a production system or agent.
-   **Local Maximum/Minimum:** A state that is better (higher/lower value) than its immediate neighbours but not necessarily the best/worst globally. A point where Hill Climbing can get stuck.
-   **Local Search:** Search algorithms that operate on a single current state and move to neighbouring states, typically used for optimization where the path doesn't matter.
-   **Manhattan Distance:** A heuristic used for grid problems (like 8-puzzle), calculated as the sum of horizontal and vertical distances ($|x_1 - x_2| + |y_1 - y_2|$).
-   **Minimax Algorithm:** An algorithm for determining the optimal move in a two-player, zero-sum game by recursively calculating the minimum or maximum utility achievable from each state.
-   **Minimax Value:** The utility value of a state assuming both players play optimally.
-   **Missionaries and Cannibals:** A classic logic puzzle and AI toy problem involving constraints on moving groups across a river.
-   **Mutation:** An operator in Genetic Algorithms that introduces small random changes to an individual's chromosome.
-   **N-Queens Problem:** The problem of placing N non-attacking queens on an N×N chessboard.
-   **Objective Function:** A function whose value is to be optimized (maximized or minimized) in search, often used in local search and game playing (utility).
-   **Operator:** Another term for an **Action** in state space search.
-   **Optimal Solution:** A solution (path) with the lowest path cost among all possible solutions.
-   **Optimality:** A property of a search algorithm guaranteeing it will find the optimal (lowest cost) solution.
-   **Path Cost:** The total cost accumulated along a path from the start state to a given node.
-   **Payoff Function:** See **Utility Function**.
-   **Perfect Information:** A property of games where all players know the complete state at all times (e.g., Chess).
-   **Plateau:** A flat area in the state-space landscape where neighbouring states have the same value.
-   **Population:** In Genetic Algorithms, the set of candidate solutions considered in one generation.
-   **Problem Formulation:** The process of defining a problem in terms of states, actions, transitions, goals, and costs.
-   **Problem-Solving Agent:** An agent that finds sequences of actions to achieve goals.
-   **Production System:** A model of computation using rules (productions) applied to a knowledge base, controlled by a strategy.
-   **Pruning:** The process of eliminating parts of the search tree that do not need to be explored (e.g., Alpha-Beta Pruning).
-   **Ridge:** A feature in a state-space landscape that is higher than its surroundings but may only allow progress along its narrow crest.
-   **Search:** The process of exploring the state space to find a solution.
-   **Search Space:** The set of all possible states reachable from the initial state.
-   **Search Tree:** A representation of the exploration of the state space, with nodes as states and edges as actions.
-   **Selection:** The process in Genetic Algorithms where fitter individuals are chosen to reproduce.
-   **Shoulder:** A plateau in the state-space landscape from which an uphill move is possible.
-   **State Space:** The set of all possible states a problem can be in.
-   **State Space Representation:** A formal way to define a problem using Initial State, Actions, Transition Model, Goal Test, and Path Cost.
-   **Step Cost:** The cost of taking a single action to move between two states.
-   **Straight-Line Distance (SLD):** A common admissible heuristic for route-finding problems, the direct distance between two points.
-   **Successor Function:** A function that generates all possible states reachable from a given state by applying one action.
-   **Terminal State:** A state where the game or process ends.
-   **Toy Problem:** A simplified problem used to illustrate or test AI methods.
-   **Transition Model:** Defines the result of taking an action in a particular state (`RESULT(s, a)`).
-   **Uninformed Search:** Search algorithms that use only the information available in the problem definition, without heuristics.
-   **Utility Function:** A function that assigns a numeric value (utility or payoff) to a terminal state in a game, representing its desirability for a player.
-   **Vacuum Cleaner World:** A simple toy problem environment for agents.
-   **Water Jug Problem:** A classic puzzle involving measuring specific amounts of liquid using jugs of fixed capacities.
-   **Zero-Sum Game:** A game where the total payoff to all players is constant for every outcome; one player's gain is exactly the other player's loss.

---

## Overall Summary & Mind Map Concept

**Central Topic:** Problem Solving using Search

**Main Branches:**

1.  **Problem Formulation:**
    *   State Space (Initial State, Actions, Transition Model, Goal Test, Path Cost)
    *   Toy vs. Real-World Problems
    *   Problem Characteristics (Decomposable, Recoverable, Predictable, etc.)
    -   Production Systems
2.  **Search Strategies:**
    *   **Uninformed (Blind) Search:** (No heuristic $h(n)$)
        *   BFS (Level-by-level, Complete, Optimal*, Memory intensive)
        *   DFS (Deep dive, Memory efficient, Not complete/optimal)
        *   DLS (DFS with depth limit, Addresses DFS incompleteness for depth L)
        *   IDDFS (Iterative DLS, Best of BFS/DFS for uninformed)
    *   **Informed (Heuristic) Search:** (Uses heuristic $h(n)$)
        *   Best-First Search (General framework, uses $f(n)$)
        *   Greedy Best-First ($f(n)=h(n)$, Fast, Not optimal/complete)
        *   A\* Search ($f(n)=g(n)+h(n)$, Complete, Optimal if $h(n)$ admissible)
            *   Admissibility / Consistency
        *   AO\* Search (For AND-OR graphs / decomposable problems)
    *   **Local Search:** (Path doesn't matter, optimization)
        *   Hill Climbing (Simple, Gets stuck in local optima)
        *   (Others: Simulated Annealing, Genetic Algorithms - related)
    *   **Adversarial Search (Games):** (Competitive environment)
        *   Minimax (Optimal for perfect info games, Impractical)
        *   Alpha-Beta Pruning (Optimizes Minimax by pruning)
3.  **Constraint Satisfaction Problems (CSP):**
    *   Definition (Variables, Domains, Constraints)
    *   Solving (Backtracking Search)
    *   Optimizations (Variable/Value Ordering, Constraint Propagation - Forward Checking, Arc Consistency)
    *   Examples (Map Coloring, Cryptarithmetic, Scheduling)
4.  **Genetic Algorithms (GA):**
    *   Evolutionary approach (Population, Fitness, Selection, Crossover, Mutation)
    *   Application in Optimization / Search

**Key Takeaway:** Choosing the right search strategy depends heavily on the problem's characteristics, the importance of optimality vs. speed/memory, and whether heuristic information is available.

---
## Further Learning Resources

-   **Textbook:** Artificial Intelligence: A Modern Approach (AIMA) by Stuart Russell and Peter Norvig (Chapters 3, 4, 5, 6 correspond closely to these topics).
-   **Online Courses:** Search for courses on AI, Problem Solving, and Search Algorithms on platforms like Coursera, edX, Udacity.
-   **Websites:** GeeksforGeeks (AI section), Javatpoint, TutorialsPoint often have good explanations and examples of these algorithms. Specific links were provided in the original slides for some examples (e.g., AO*, Alpha-Beta).

```