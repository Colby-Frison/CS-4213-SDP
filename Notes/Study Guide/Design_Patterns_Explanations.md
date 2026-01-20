# Comprehensive Software Design Patterns Guide

This document covers General Responsibility Assignment Software Patterns (GRASP) and Gang of Four (GoF) design patterns.

---

## 1. GRASP "Patterns" (Principles)
*General Responsibility Assignment Software Patterns*

**Important Note:** GRASP is not a set of "implementation patterns" (like GoF patterns which describe specific class structures). Instead, GRASP provides a **learning aid** and a **mental toolkit** for object-oriented design. They are **principles** that guide you on *how to assign responsibilities* to classes and objects. When you are drawing a sequence diagram or deciding where to put a method, you are using GRASP principles, even if you don't realize it.

### Information Expert
*   **Concept:** Who should do X? The one who has the data to do X.
*   **Intent:** Assign responsibility to the class that has the information needed to fulfill it.
*   **Context:** Calculating a total sale price. The `Sale` object contains `SaleLineItem` objects, so it is the "Expert" on calculating the total.
*   **Pros:** Encapsulation is maintained; behavior is distributed to where data lives.
*   **Cons:** Can lead to "God Classes" if one class has all the information.

### Creator
*   **Concept:** Who should create X? The one who looks after X.
*   **Intent:** Assign responsibility for creating an instance of class A to class B if B "contains" A, records A, closely uses A, or has the initializing data for A.
*   **Context:** A `Board` contains `Square` objects. The `Board` should create the `Squares`.
*   **Pros:** Supports low coupling.
*   **Cons:** Sometimes leads to coupling if creation logic is complex (better suited for Factory).

### Controller
*   **Concept:** Who handles the incoming system event?
*   **Intent:** Assign responsibility for handling a system event to a class representing the overall system, a use case scenario, or the active device.
*   **Context:** A `Register` or `POSSystem` class receiving input from a UI layer. It delegates work to other objects.
*   **Pros:** Separates UI from business logic.
*   **Cons:** Can become bloated (Massive View Controller) if it handles too much logic itself rather than delegating.

### Low Coupling
*   **Concept:** How do we minimize impact of change?
*   **Intent:** Assign responsibilities so that coupling (dependency) remains low.
*   **Context:** Choosing between calling a specific database driver vs. an interface.
*   **Pros:** Easier maintenance, testing, and reuse.
*   **Cons:** Extreme low coupling can lead to excessive abstraction and complexity.

### High Cohesion
*   **Concept:** How do we keep objects focused?
*   **Intent:** Assign responsibilities so that cohesion remains high (a class does related things).
*   **Context:** Splitting a `User` class that handles auth, profile management, and email notifications into three separate classes.
*   **Pros:** Classes are easier to understand and maintain.
*   **Cons:** Too much granular cohesion can lead to an explosion of tiny classes.

### Polymorphism
*   **Concept:** How do we handle variations?
*   **Intent:** Assign responsibility for behavior using polymorphic operations instead of explicit type checks (if/else or switch).
*   **Context:** `PaymentProcessor.process()` implemented by `CreditCardProcessor` and `PayPalProcessor`.
*   **Pros:** Handling new variations is easy (Open/Closed Principle).
*   **Cons:** Can complicate code flow tracing; overkill for simple, stable logic.

### Pure Fabrication
*   **Concept:** What if there is no domain concept for this?
*   **Intent:** Assign a highly cohesive set of responsibilities to an artificial or convenience class that does not represent a problem domain concept.
*   **Context:** `PersistanceManager` or `Logger`. It's not a "real" thing in the business domain, but needed for clean code.
*   **Pros:** Supports High Cohesion and Low Coupling.
*   **Cons:** Can be abused to create too many service classes, leading to an anemic domain model.

### Indirection
*   **Concept:** How do we de-couple two things?
*   **Intent:** Assign responsibility to an intermediate object to decouple two other components.
*   **Context:** An Adapter or Facade.
*   **Pros:** Low coupling between components.
*   **Cons:** Adds a layer of complexity; performance overhead.

### Protected Variations
*   **Concept:** How do we future-proof against change?
*   **Intent:** Identify points of predicted variation or instability; create a stable interface around them.
*   **Context:** Wrapper around a 3rd party API that changes frequently.
*   **Pros:** Protects the system from changes in other elements.
*   **Cons:** Speculative generality (protecting against changes that never happen).

---

## 2. GoF: Creational Patterns
*Dealing with object creation mechanisms*

### Abstract Factory
*   **Structure:** Interface `Factory` has methods `createProductA()`, `createProductB()`.
*   **Intent:** Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
*   **Context:** UI Toolkit (create Button, ScrollBar, Window) for Windows vs. MacOS. A `WindowsFactory` creates `WindowsButton`, etc.
*   **Pros:** Ensures compatibility between products in a family.
*   **Cons:** Adding a new product type (e.g., "Slider") requires changing the interface and all subclasses.

### Builder
*   **Structure:** `Director` calls `Builder` methods (`buildPartA()`, `buildPartB()`) and then `getResult()`.
*   **Intent:** Separate the construction of a complex object from its representation so that the same construction process can create different representations.
*   **Context:** Building a complex SQL query or an HTTP Request with many optional headers.
*   **Pros:** Granular control over the construction process; clear separation of construction and representation.
*   **Cons:** Requires creating a separate Builder class; increased verbosity.

### Factory Method
*   **Structure:** Parent class defines `abstract create()`. Subclasses override `create()` to return specific object.
*   **Intent:** Define an interface for creating an object, but let subclasses decide which class to instantiate.
*   **Context:** `Document.createPage()`. A `ReportDocument` creates `TextPage`s, a `ResumeDocument` creates `SkillPage`s.
*   **Pros:** Follows Open/Closed Principle; decouples creator from concrete products.
*   **Cons:** Can lead to a lot of subclasses just to change the product being created.

### Prototype
*   **Structure:** Object has a `clone()` method.
*   **Intent:** Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
*   **Context:** Game entities (enemies) where you spawn many similar instances with slight variations.
*   **Pros:** Avoids subclassing; efficient for complex object creation.
*   **Cons:** "Cloning" complex objects with circular references is tricky (deep vs. shallow copy).

### Singleton
*   **Structure:** Private constructor, static `getInstance()` method.
*   **Intent:** Ensure a class has only one instance and provide a global point of access to it.
*   **Context:** Logging service, Database connection pool, Configuration manager.
*   **Pros:** Controlled access to a single instance.
*   **Cons:** Considered a global state anti-pattern; hard to unit test; hides dependencies.

---

## 3. GoF: Structural Patterns
*Dealing with object composition*

### Adapter
*   **Structure:** `Adapter` implements `Target` interface and delegates to `Adaptee`.
*   **Intent:** Convert the interface of a class into another interface clients expect.
*   **Context:** Making a legacy XML parser work with a new JSON-based data loader interface.
*   **Pros:** Reusability of existing code; interoperability.
*   **Cons:** Can add complexity if there are many adaptations needed.

### Bridge
*   **Structure:** `Abstraction` (Shape) holds reference to `Implementor` (Renderer). Subclasses of `Abstraction` (Circle) use `Implementor`.
*   **Intent:** Decouple an abstraction from its implementation so that the two can vary independently.
*   **Context:** `Shape` (abstraction) and `Renderer` (implementation). You can add new Shapes or new Renderers (OpenGL, DirectX) without Cartesian product of classes.
*   **Pros:** Separation of concerns; flexibility.
*   **Cons:** Increases complexity; hard to understand initially.

### Composite
*   **Structure:** `Component` interface is implemented by `Leaf` and `Composite` (which holds list of `Component`).
*   **Intent:** Compose objects into tree structures to represent part-whole hierarchies. Treat individual objects and compositions of objects uniformly.
*   **Context:** File system (Files and Folders), UI components (Panel contains Buttons and other Panels).
*   **Pros:** Simplifies client code (can treat leaf and node same way).
*   **Cons:** Can make design overly general (hard to restrict children types).

### Decorator
*   **Structure:** `Decorator` implements `Component` and wraps a `Component`. Adds behavior before/after delegation.
*   **Intent:** Attach additional responsibilities to an object dynamically.
*   **Context:** Java I/O Streams (`BufferedInputStream(new FileInputStream(...))`). Adding scrollbars to a window.
*   **Pros:** More flexible than inheritance for extending functionality.
*   **Cons:** Can result in many small objects; debugging can be difficult due to layers.

### Facade
*   **Structure:** Simple class calls methods on many complex classes.
*   **Intent:** Provide a unified interface to a set of interfaces in a subsystem.
*   **Context:** A `SmartHomeFacade` that turns on lights, adjusts thermostat, and locks doors with one method `arriveHome()`.
*   **Pros:** Simplifies usage for client; reduces coupling.
*   **Cons:** Facade can become a "god object" coupled to all subsystem classes.

### Flyweight
*   **Structure:** `FlyweightFactory` manages shared objects. Client passes extrinsic state.
*   **Intent:** Use sharing to support large numbers of fine-grained objects efficiently.
*   **Context:** Text editor storing characters (glyph, font style shared; position unique).
*   **Pros:** Reduces memory usage significantly.
*   **Cons:** Code complexity increases; state must be separated into intrinsic (shared) and extrinsic (unique).

### Proxy
*   **Structure:** `Proxy` implements same interface as `RealSubject`. Controls access to it.
*   **Intent:** Provide a surrogate or placeholder for another object to control access to it.
*   **Context:** Lazy loading images (Virtual Proxy), Access control (Protection Proxy), Remote method calls (Remote Proxy).
*   **Pros:** Controls access; allows lazy initialization.
*   **Cons:** Adds indirection; can mask latency in remote calls.

---

## 4. GoF: Behavioral Patterns
*Dealing with object interaction and responsibility*

### Chain of Responsibility
*   **Structure:** Handler has `nextHandler`. If it can't handle request, passes to next.
*   **Intent:** Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request.
*   **Context:** Event bubbling in UI; Logging filters (Debug -> Info -> Error).
*   **Pros:** Decouples sender and receiver; flexible assignment of responsibilities.
*   **Cons:** No guarantee the request will be handled; debugging flow can be hard.

### Command
*   **Structure:** `Command` object has `execute()`. Wraps `Receiver` and parameters.
*   **Intent:** Encapsulate a request as an object, letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
*   **Context:** GUI Buttons (ActionListeners), Macro recording, Undo/Redo stacks.
*   **Pros:** Decouples invoker from receiver; easy to add new commands; supports undo/redo.
*   **Cons:** Proliferation of small command classes.

### Interpreter
*   **Structure:** Classes for `TerminalExpression` and `NonTerminalExpression` form an AST.
*   **Intent:** Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
*   **Context:** SQL parsers, Regex engines, Mathematical expression evaluators.
*   **Pros:** Easy to change and extend grammar.
*   **Cons:** Inefficient for complex grammars; hard to maintain if grammar is large.

### Iterator
*   **Structure:** `Iterator` interface (`hasNext`, `next`) separates traversal from collection.
*   **Intent:** Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
*   **Context:** `for (Item i : list)` loops; traversing a tree or graph.
*   **Pros:** Standard interface for traversal; supports multiple simultaneous traversals.
*   **Cons:** Can be overkill for simple lists.

### Mediator
*   **Structure:** `Mediator` knows all `Colleague`s. Colleagues only know Mediator.
*   **Intent:** Define an object that encapsulates how a set of objects interact.
*   **Context:** Air Traffic Control tower; Chat room server. Components talk to Mediator, not each other.
*   **Pros:** Reduces coupling between colleagues; centralizes control.
*   **Cons:** Mediator can become a complex monolith ("God Object").

### Memento
*   **Structure:** `Originator` creates `Memento` (state snapshot). `Caretaker` stores it.
*   **Intent:** Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.
*   **Context:** "Save Game" functionality; Undo mechanisms in editors.
*   **Pros:** Preserves encapsulation boundaries while saving state.
*   **Cons:** Can be expensive (memory/storage) if state is large.

### Observer
*   **Structure:** `Subject` has list of `Observers`. Calls `update()` on them when state changes.
*   **Intent:** Define a one-to-many dependency so that when one object changes state, all its dependents are notified and updated automatically.
*   **Context:** MVC (Model updates Views); Event listeners; Newsletter subscriptions.
*   **Pros:** Open/Closed principle (add new observers without changing subject).
*   **Cons:** Memory leaks (Lapsed Listener Problem); update order not guaranteed.

### State
*   **Structure:** Object delegates behavior to a `State` object. Switching state object changes behavior.
*   **Intent:** Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.
*   **Context:** TCP Connection (Closed, Listen, Established); Vending Machine; Document Workflow (Draft, Review, Published).
*   **Pros:** Eliminates massive switch/if-else statements; makes state transitions explicit.
*   **Cons:** Increases number of classes.

### Strategy
*   **Structure:** Context holds reference to a `Strategy` interface. Client injects concrete strategy.
*   **Intent:** Define a family of algorithms, encapsulate each one, and make them interchangeable.
*   **Context:** Sorting algorithms (QuickSort vs MergeSort); Route calculation (Fastest vs Shortest vs Scenic).
*   **Pros:** Eliminates conditional statements; easy to switch algorithms at runtime.
*   **Cons:** Client must know the differences between strategies.

### Template Method
*   **Structure:** Abstract class defines method with fixed steps. Calls abstract methods for customizable steps.
*   **Intent:** Define the skeleton of an algorithm in an operation, deferring some steps to subclasses.
*   **Context:** Data mining algorithm (step 1: read data, step 2: process [abstract], step 3: save).
*   **Pros:** Code reuse; strict control over the algorithm structure.
*   **Cons:** Hard to maintain if the skeleton needs to change; Liskov Substitution Principle violations if subclasses change flow too much.

### Visitor
*   **Structure:** `Visitor` has method for each Element type (`visit(ElementA)`, `visit(ElementB)`). Element has `accept(Visitor)`.
*   **Intent:** Represent an operation to be performed on the elements of an object structure. Lets you define a new operation without changing the classes of the elements on which it operates.
*   **Context:** Compiler (AST traversal for type check, code gen, pretty print); Tax calculation on different item types.
*   **Pros:** Easy to add new operations (Visitors).
*   **Cons:** Hard to add new element types (requires changing all Visitors).
