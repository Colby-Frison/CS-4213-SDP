# Composite Pattern

## 16.4.1 Representing Recursive Whole-Part Structures

The design of the state diagram editor needs to consider composite states, meaning the design has to represent complex structures where a state object may include other state objects. This design problem is common in software design:

- A tree consists of nodes and edges, and a node can represent a subtree
- A network consists of nodes and subnets  
- A system consists of subsystems and components, and a subsystem may contain other subsystems or components

The keywords are "recursive, part-whole" relationships. Looking up the patterns leads to the **Composite Pattern**, which is useful for processing complex class structures containing recursive part-whole relationships.

### Composite Pattern Specification

**Name:** Composite  
**Type:** GoF/Structural  

**Problem:** How to represent recursive, part-whole relationships and allow the client to deal with primitive and composite components uniformly.

**Solution:** Define a common interface to unify the primitive and composite components so that the client can access them uniformly.

**Design:** Structural

### Roles and Responsibilities

- **Component:** Defines an interface for the client to access both composite and primitive components uniformly. Provides default, do-nothing implementation for composite-only operations such as `add`, `remove` and `get`.

- **Composite Component:** Contains primitive and composite components and implements the composite-only operations.

- **Primitive Components:** These components do not contain other components. They implement `operation()` to provide component-specific behavior.

- **Client:** Creates or obtains an instance of a subclass of Component and calls its functions.

## Applying Composite Pattern

Step 2 identifies the composite pattern to represent a state diagram. Step 3 of the pattern-application process is to apply the composite pattern to the existing design.

To do this, we view the classes in the pattern as "variables," which we replace with classes in the existing design. First, we determine which class in the existing design should substitute for the client class in the pattern.

*The structural design shows that the Composite Component is an aggregation of Component. The inheritance relationship indicates that a Component is either a Primitive Component or a Composite Component. Thus, if Composite Component and Primitive Component 1 and 2 are substituted with State Diagram, State, and Transition, respectively, then a state diagram may contain states, transitions, as well as other state diagrams.*