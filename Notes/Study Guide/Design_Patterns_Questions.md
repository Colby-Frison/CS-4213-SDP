# Design Patterns Study Questions

This document contains creative questions designed to test your understanding of GRASP and GoF design patterns. Answers are provided at the end of the document.

---

## GRASP Questions

1.  **Information Expert vs. High Cohesion:** A `Sale` class has all the information about `Items`, `TaxRates`, and `CustomerLoyalty`. According to Information Expert, it should calculate the final price. However, adding tax logic and loyalty logic makes the class huge. Which other GRASP pattern suggests splitting this up, and how would you resolve the conflict?
2.  **Controller:** You are building a web API. Why might having a single "SystemController" class that handles all incoming requests be a violation of the Controller pattern's best practices, even if it fits the definition?
3.  **Pure Fabrication:** You need to save objects to a database. The domain objects (e.g., `User`, `Order`) should not know about SQL or database connections to maintain Low Coupling. What kind of Pure Fabrication object would you create, and what GoF pattern does it often resemble?
4.  **Protected Variations:** How does the Protected Variations pattern relate to the Open/Closed Principle? Give a concrete example of using an interface to "protect" your system from a volatile third-party weather API.

## GoF Questions

### Creational
5.  **Abstract Factory + Singleton:** In many systems, an Abstract Factory is implemented as a Singleton. Why is this a common combination? What are the risks of doing this?
6.  **Builder vs. Factory Method:** You are creating a complex `RPGCharacter` with stats, inventory, armor, and class specific traits. Why would you choose Builder over Factory Method for this specific scenario?
7.  **Prototype:** Imagine a game where enemies spawn every 5 seconds. Why might Prototype be more performance-efficient than using `new Enemy()` if the initialization of `Enemy` involves loading heavy 3D assets?

### Structural
8.  **Adapter + Facade:** What is the key difference in *intent* between an Adapter and a Facade? Can you have a situation where you wrap a Facade in an Adapter?
9.  **Composite + Decorator:** You have a `TextComponent` interface. You use Composite to build a hierarchy of text blocks (paragraphs, sentences). How could you use Decorator in this same system to add "Bold" or "Italic" styling to specific leaf nodes or entire composite groups?
10. **Bridge:** You are designing a cross-platform video player that needs to support Windows, Linux, and MacOS, and also support different rendering engines (DirectX, OpenGL, Vulkan). How would the Bridge pattern prevent a class explosion (e.g., `WindowsDirectXPlayer`, `LinuxOpenGLPlayer`, etc.)?
11. **Flyweight:** In a word processor, you decided to make every character an object. The system crashed due to memory overflow. How does Flyweight solve this, and what is the specific difference between the "intrinsic" state (like the character 'A') and "extrinsic" state (like position x=10, y=50)?

### Behavioral
12. **Strategy + Factory:** You have a `PaymentProcessor` that needs to select a payment strategy (PayPal, Stripe, Crypto) based on user input. How can a Factory pattern help the Strategy pattern here?
13. **Observer + Mediator:** Both patterns involve communication between objects. In a complex form with 20 interdependent inputs (changing one dropdown updates 5 others), why might Mediator be cleaner than Observer?
14. **Command + Memento:** You are building a text editor with infinite Undo/Redo. The Command pattern handles the execution of actions. What role does Memento play in this combination? Why not just store the reverse logic in the Command itself?
15. **Chain of Responsibility:** You are building a middleware for a web server (Auth check -> Logging -> Compression -> Request handling). Why is Chain of Responsibility better here than a giant `if-else` block in a central handler?
16. **State vs. Strategy:** Structurally, State and Strategy look almost identical (both delegate to an interface). What is the semantic difference in *who* drives the transition? Does the Client change the Strategy, or does the State change itself?
17. **Visitor:** You have a stable hierarchy of `ASTNode` types (IfNode, ForLoopNode, AssignmentNode) for a compiler. You need to add a new operation "GeneratePythonCode" and later "GenerateJavaCode". Why is Visitor the perfect fit here, and what would happen if you tried to add a new node type `WhileLoopNode` later?

---

# Answers

1.  **Information Expert vs. High Cohesion:** While `Sale` has the info, giving it too many responsibilities violates **High Cohesion**. To resolve this, you might delegate specific calculations to other helper classes (like a `TaxCalculator` or `LoyaltyService`), keeping the `Sale` class focused on coordinating the total rather than knowing every tax rule. This is also an example of **Pure Fabrication** or **Indirection**.
2.  **Controller:** A single "SystemController" becomes a **Bloated Controller** (or God Class), which has low cohesion and high coupling. The Controller pattern suggests using *UseCase Controllers* (e.g., `OrderController`, `UserController`) to distribute the logic rather than a single entry point for the entire application.
3.  **Pure Fabrication:** You would create a Data Access Object (DAO) or Repository. This is a Pure Fabrication because "Repository" isn't a business concept like "Customer". It often resembles the **Adapter** or **Bridge** pattern (adapting your domain objects to the database world).
4.  **Protected Variations:** It is essentially the mechanism to achieve OCP. By wrapping the unstable weather API in a stable `IWeatherProvider` interface, the rest of the system depends on the interface. If the API changes, you only update the implementation of the wrapper, "protecting" the rest of the system from the variation.
5.  **Abstract Factory + Singleton:** You usually only need one factory instance per application run (e.g., one `WindowsUIFactory`). Making it a Singleton ensures global access and consistent UI generation. Risk: Harder to test (global state) and hard to swap if you ever *do* need parallel factories.
6.  **Builder vs. Factory Method:** `RPGCharacter` creation is a multi-step process with many optional parameters. Factory Method is good for "one-step" creation. Builder is better here because it allows step-by-step construction (`.setArmor(...)`, `.setWeapon(...)`) and avoids a constructor with 20 arguments.
7.  **Prototype:** If `new Enemy()` requires parsing a 50MB 3D model file from disk every time, it is slow. Prototype loads it once into memory, and then `clone()` performs a memory copy (much faster) to create new instances.
8.  **Adapter vs. Facade:** Adapter makes *incompatible* interfaces work together (fixing a square peg in a round hole). Facade provides a *simplified* interface to a complex subsystem (making a simple dashboard for a complex engine). Yes, you can wrap a Facade in an Adapter if the Facade's interface doesn't match what an existing client expects.
9.  **Composite + Decorator:** You can wrap any node (Leaf or Composite) in a `BoldDecorator`. Since Decorator implements the same interface as the Component, the Composite doesn't know the difference. This allows you to style a single word or an entire paragraph recursively.
10. **Bridge:** You separate the `VideoPlayer` abstraction (Play, Stop, Pause) from the `VideoRenderer` implementation (DrawFrame).
    *   Refined Abstractions: `WindowsPlayer`, `LinuxPlayer`
    *   Concrete Implementors: `DirectXRenderer`, `OpenGLRenderer`
    *   The Player holds a reference to a Renderer. This avoids `WindowsDirectXPlayer` style cartesian products.
11. **Flyweight:** **Intrinsic state** is the data shared by thousands of objects (the pixel shape of 'A', the font 'Arial'). **Extrinsic state** is the context-specific data (position x,y, color). The Flyweight factory stores the Intrinsic state once; the client passes the Extrinsic state to the flyweight when drawing.
12. **Strategy + Factory:** The Client shouldn't strictly know *which* concrete strategy class to instantiate (coupling). A Factory can take a string (e.g., "PAYPAL") and return the correct `PaymentStrategy` object, keeping the client code clean.
13. **Observer vs. Mediator:** With Observer, 20 inputs observing each other leads to a "spiderweb" of dependencies (Cascading updates). Mediator centralizes this logic: "Input A changed, tell Mediator. Mediator decides to update Inputs B, C, and D." It decouples the colleagues.
14. **Command + Memento:** The Command object stores the logic to `execute()`. To support `undo()`, the Command can store a Memento of the state *before* execution. When `undo()` is called, the Command restores that state. Storing reverse logic (e.g., "minus 5" to undo "plus 5") works for simple math but fails for complex state changes (like "delete text"). Memento restores the exact previous state reliably.
15. **Chain of Responsibility:** It allows you to dynamically add/remove/reorder middleware handlers without changing the core code. An `if-else` block is rigid and violates Open/Closed Principle.
16. **State vs. Strategy:**
    *   **Strategy:** Client usually chooses the strategy once (e.g., "Save as PDF"). The strategy rarely switches itself.
    *   **State:** The "Context" object transitions between states dynamically based on inputs (e.g., TCP Connection goes from listening -> established -> closed). States often trigger the switch to the *next* state.
17. **Visitor:** Visitor is perfect because the *object structure* (AST nodes) is stable (you rarely add new language syntax constructs), but the *operations* (Generate Code, Lint, Optimize) change often. If you added `WhileLoopNode`, you would have to update *every single Visitor class* to handle `visitWhileLoopNode`, which is the main downside of Visitor.
