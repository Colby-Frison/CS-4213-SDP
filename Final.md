# Exam Readiness

I have analyzed the codebase and familiarized myself with the course material to assist you with your final exam.

## Context Analysis
- **Design Patterns**: I have reviewed the comprehensive guide in `Notes/Study Guide/Design_Patterns_Explanations.md`, covering both GRASP (e.g., Information Expert, Controller) and GoF patterns (Creational, Structural, Behavioral).
- **Practical Implementations**: I have examined the code examples, specifically the State Pattern implementation in `Assignments/Group/Participation 3`, which helps in understanding how these patterns are applied in C#.
- **Course Progression**: I've looked through the weekly notes and questions, noting the focus on comparing patterns (e.g., Facade vs. Adapter) in the later weeks.

I am ready to answer your questions using this context. Please paste the exam questions here or ask them directly.


# Questions

Keep your answer less than 150 words. Words beyond the limit will not be considered for grading.

## Question 1

The Law of Increasing Entropy or Complexity, where the structure of the software degrades as changes are made.After 10 years, the Daily Operations Dashboard has grown messy. Every new feature adds more conditionals, duplicated logic, and cross-module dependencies. Developers say adding anything new breaks old functionality.
Select ONE GoF pattern that best helps control or reduce complexity.
Justify why your chosen pattern is the most effective response to the Law of Increasing Complexity, and explain how applying it would slow the system’s entropy.

### Answer

**Pattern: State Pattern**

The State pattern is the best choice because the current system suffers from messy conditionals and fragile dependencies, which are classic signs of poor state management. It works by replacing massive `switch` statements with separate classes for each state, directly eliminating duplicated logic. This slows entropy by adhering to the Open/Closed Principle: you add new features or states by creating new classes instead of modifying - and potentially breaking—stable code. Finally, because each state encapsulates its own behavior, the main Dashboard code remains clean, ensuring complexity grows linearly with new files rather than exponentially tangling the existing system.

## Question 2

The Law of Feedback Systems, where all the other laws are caused by feedback behavior. Changes in one part of the dashboard cause ripple effects everywhere. The system feels like a tightly wound machine where everything depends on everything else.
Select ONE GoF pattern that best manages feedback loops or decouples components.
Justify why your chosen pattern is the best response to the Law of Feedback Systems, explaining how it helps control and structure interactions.

### Answer

**Pattern: Mediator Pattern**

The mediator pattern is the best solution for breaking the "tightly wound" feedback loops where "everything depends on everything else." By introducing the central Mediator object, components no longer communicate directly with each other - they only communicate with the mediator. This transforms the many-to-many dependency web into a manageable one-to-many structure. The mediator centralizes the control logic for the dashboard, decoupling components and preventing changes in one part of the dashboard from propagating uncontrollably to other, stabilizing the system and counteracting the Law of Feedback Systems.

## Question 3

The Law of Declining Quality, where the quality of E-type systems appear to be declining until they are rigorously adapted to changes in the operating environment. Even without adding features, the dashboard’s reliability is worsening. Bugs appear in modules that have not changed for years. QA teams say the architecture no longer fits new operational environments.
Select ONE GoF pattern that helps maintain architectural quality and isolate fragile components.
Explain why your chosen pattern addresses the Law of Declining Quality, and how it improves stability without rewriting everything.

### Answer

**Pattern: Adapter Pattern**

The adapter pattern is a good choice in addressing the Law of Declining Quality, as it enables a system to adapt to new "operating environments" - like new APIs, hardware, or third party services - without modifying the fragile legacy code. By wrapping the new, incompatible environment in an Adapter that conforms to the system's existing interface, the legacy code is isolated from external damage. This stops the decline in reliability as developers don't have to touch the old, stable modules to support new requirements. Instead, the adapter takes on the abnormalities of the new environments, providing stability and extending the system's lifespan without a rewrite.

Like in previous projects instead of directly implementing APIs into the core system, we would write wrappers, to create a consistent interface and protect our code from potential issues of the new environment.

## Question 4

In the Daily Operations Dashboard, a new requirement states that the system must calculate a Project Health Score for each active project.
The score depends on multiple factors:
 - Percentage of completed tasks
 - Number of delayed tasks
 - Average team workload
 - Escalated issues
 - Budget health from the Finance subsystem
During a design meeting, the team cannot agree on where this calculation logic should live. There are four different opinons: 1) “Put it inside the DashboardController—it already displays the score.” 2) “Give it to Project—it owns the tasks and progress data.” 3) “Create a HealthCalculator utility class to avoid cluttering the domain model.” 4) “Let Finance handle it since some metrics come from their system.”
When dependencies are mapped out, the debate intensifies, especially since some teams worry about tight coupling and duplicated logic. In your opinion, which component should be responsible for computing the Project Health Score according to the GRASP Information Expert principle? Justify your answer by explaining which component has the necessary information, how your choice reduces coupling, and why the other options (Controller, Utility class, Finance) may cause maintainability or consistency issues.

### Answer

**Responsible Component: `Project`**

If we follow the information expert principle, the Project class is the best place to calculate the Project Health Score. This is because Project already owns or aggregates the majority of the necessary data. By assigning the responsibility here, we maintain high cohesion and low coupling, as the class only needs to query its own internal state.

The other options create maintenance issues. A controller (option 1) should coordinate, not calculate - adding business logic there would lead to a bloated "God class". A utility class (option 3) causes "Feature envy", where an external object constantly reaches into Project's private data. Finally, Finance (option 4) is a separate domain, so giving it operational responsibilities - like tracking task delays - creates unnecessary cross-subsystem coupling and confuses the system's structure.

In the past I have had to make similar choices, and I have usually found delegating calculations to the owner is best.