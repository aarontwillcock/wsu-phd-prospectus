# Prospectus Notes

## Suggestions from 2020-02-26 Meeting

- Combine papers + related works
- Put them in context of larger question
- Try to avoid using papers as distinct chapters
- Think about how you want to tell the story

## Whiteboard Notes

Research Question:

1. How can the physical system dynamics be used to improve schedulability, reduce schedulability / feasibility calculation time, or improve real-time system analysis tools?

Keywords / Foci:

1. Dynamics
   1. Use known dynamics to identify problems for future systems (for example, adaptivity models that don't yet exist)
   2. Codesign links between parameters (for example, short-circuit detection, engine control design, setpoint sequences)
2. Schedulability
   1. Use system dynamics to reveal underutilization (overly pessimistic analysis)
   2. Create task models to describe adaptivities not yet accounted for
3. Calculation Time
   1. Improving Existing Calculations: Avoid examining unnecessary intervals/situations (ex. Knapsack, Switched Control)
   2. Creating New Exact Calculations: Calculation doesn't exist at all
   3. Creating New Approximations: Applies to either improved calculations or new exact calculations.

## Refining my Goals

Components:

1. Calculation Improvements
   1. Existing Calculations: Improved by leveraging system dynamics to avoid examining unnecessary scenarios.
   2. Non-existant Calculations: Designing and implementing new calculations for demand characterization.
   3. Approximations: Approximating both new and improved calculations.
2. Codesign
   1. Linking physical system dynamics to real-time demand characterization and scheduling.
   2. Employing links to optimize physical and/or real-time performance.

## Airbag example

To demonstrate this, consider the requirements for an airbag in a vehicle.
The requirements for a supplemental restraint system (SRS) airbag is two-fold:
1) Decide, after a collision, if sufficient acceleration was generated to require airbags (as detected by an accelerometer) and
2) Fully inflate within [30-50 ms after the impact](https://www.nhtsa.gov/sites/nhtsa.dot.gov/files/rev_report_0.pdf) if the collision requires airbags

The requirements here are given in terms of logical and temporal requirements.
Logically, the computer must accurately calculate acceleration to determine whether an impact is severe enough to justify using airbags.
Temporally, the computer must deploy the airbags within 50ms of the airbag or risk further harm to the occupants.

https://crashstats.nhtsa.dot.gov/Api/Public/ViewPublication/812069.pdf

A failure in either domain will result in increased injury and higher mortality rate.
Specifically, determining that no airbag is needed when forces are high enough to kill occupants is a logical flaw.
Deploying the airbag too slowly may cause even more harm to the passenger.

## Why worry about dynamics

For any control system implementation, the system exists because some physical dynamic needs to be controlled.

Using knowledge of system dynamics gives us a few advantages:
1) Allows for more accurate demand characterization
2) Allows for faster calculation of demand characterization
More accurate or tractable demand characterization also yields more accurate and tractable feasibility and schedulability results.
3) Allows for codesign of scheduling and physical components.

1. Why do we care about more accurate demand characterization?
   1. More accurate calculations reveal more "space" that could be used by other tasks.
   2. More accurate calculations reduce the hardware requirements of the system and thus total cost of the system.
   3. Real-world impact: cheaper systems with the same safety-critical guarantees.
      1. For example, reducing cost of ECUs in vehicles. With 15 ECUs per car, reducing proc size multiplies savings by 15 x # cars built.
      2. Reducing the number of ECUs reduces power requirements, cabling, manf. cost.
2. Why do we care about faster demand characterization?
   1. Online recharacterization of demand is required when tasks:
      1. move between heterogenerous platforms,
      2. merge with other tasks, or
      3. change their operating parameters online.
   2. Safety critical systems may rely on migration of tasks between ECUs (https://hal.inria.fr/hal-01416879/document)
   3. Reducing demand characterization costs allows for online calculation where predetermined safety measures might be used.
3. Why do we care about codesign of scheduling and physical components?
   1. Allows for visualization of the tradeoff between scheduling and physical system dynamics
   2. Complexity, Concurrency, Correctness

## John Cav. Outline

1. Introduction
   1. Motivation
      1. RTS
      2. WCET
      3. my specific stuff
      4. Schedulability Analysis
   2. Approach
   3. Contributions
   4. Outline
2. Related Works
3. System Models and Terminology
   1. Real-Time Terminology
   2. Real-Time Task Models
      1. Autonomous Battery Operating System (ABOS)
      2. Engine Control Unit (ECU)
      3. Short Circuit Detection (SCD) 
   3. Control System Terminology
   4. Control System Models
      1. Switched Control System (SCS)
4. CATEGORY 1
5. CAT 2
6. CAT 3

## Remaining Works

1. Short Circuit Detection
   1. Codesign implementation of software and hardware task- Done
   2. Comparison against existing works
2. ABOS
   1. Fault detection - Conf. Paper (merge from Short Circuit but applied to cells)
   2. Battery size selection (demand modeling) - Conf. Paper
   3. Route Selection (V2G, G2V) - Conf. Paper merged from joint ABOS
3. SP Schedule
   1. WCD for SPSched - Submitted
   2. DBF for graph - Conf. Paper
   3. Online Optimization
4. Engine Control
   1. Knapsack AVR - Done
   2. Approx Alg of Knapsack - Extension of Conf. Paper
   3. Dynamic Skip Fire - Conf. Paper on DBF for DSF, DoD, VD, etc.
5. Hybrid Systems
   1. Multichem Route Selection / Eng
   2. Battery sizing for SDB

