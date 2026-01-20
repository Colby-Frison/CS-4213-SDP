# Weekly question
>1. Which of the following is NOT a benefit of the Expert GRASP pattern?
>a) Designing “smart object.”
>b) Easy to understand and change due to high cohesion and low coupling. 
>c) High cohesion because responsibilities are assigned to objects that can fulfill the responsibilities. 
>d) Low coupling because the given request is handled directly by the object that has the information to fulfill the request

--- 
# Monday

## Issues with controller design pattern
### Tight coupling between the presentation and the business objects

**The Core Problem:** The presentation layer directly accesses and calls functions on the business objects. This creates a rigid dependency between them.

**Why This is Undesirable:**
1.  **Difficulty of Change:** Any change to the business objects' interfaces or logic (e.g., a function returning new values or the same values with new meanings) forces changes in the presentation layer, and vice versa. This makes maintenance costly and error-prone.
2.  **Inability to Support Multiple UIs:** It becomes very difficult to support different user interfaces (desktop, web, mobile) because the business logic is duplicated within each presentation layer. A change to the core logic requires updating every single UI implementation consistently, which is complex and likely to lead to inconsistencies.
3.  **Hinders Evolution:** This tight coupling makes software evolution, like adding a new web interface to an existing desktop application, a difficult and expensive process of duplication rather than a simple extension. This often forces companies into costly re-engineering projects.

**In essence,** the tight coupling binds the user interface directly to the business rules, creating a brittle system that is hard to change, maintain, and expand upon, especially as the application scales to dozens or hundreds of use cases.

### The presentation has to handle actor requests.

**The Problem:** The presentation object (e.g., the Checkout GUI) is given the responsibility of handling complex actor requests that require background processing (like processing a document checkout).

**The Principle:** The principle of separation of concerns states that a software component should be responsible for a single, distinct aspect of the functionality.

**The Conclusion:** According to this principle, the presentation's only concern should be managing the user interface—displaying information and capturing input. The task of processing business logic (like a checkout request) is a separate concern and should be the responsibility of a business object, not the presentation. The current design incorrectly blends these two distinct concerns into one component.

### The presentation is assigned too many responsibilities.

This text concludes that the design from the previous summaries results in a presentation object with **poor software design properties**:
1.  **Too Many Responsibilities:** The presentation is burdened with two major tasks: displaying the user interface **and** processing complex business logic. It is no longer a simple ("stupid") display object.
2.  **Violates High Cohesion:** The two responsibilities (UI presentation and business logic processing) are unrelated. High cohesion requires a module's parts to be strongly related and focused on a single purpose. Combining these unrelated tasks into one object results in low cohesion, making the object complex, difficult to understand, and hard to maintain.

In short, the design creates a single object that is overly complex and poorly structured because it mixes unrelated duties.

## Case controller vs. facade controller

| Feature               | Use Case Controller                                                                                  | Facade Controller                                                                                                                                                              |
| :-------------------- | :--------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Responsibility**    | Handles all actor requests for **a single, specific use case**.                                      | Handles **all requests** submitted to an entire system or organization.                                                                                                        |
| **Scope**             | Narrow (one controller per use case).                                                                | Broad (one controller for the whole system).                                                                                                                                   |
| **Design Principle**  | Preferred because it promotes **high cohesion, separation of concerns, and ease of change**.         | Used for specific scenarios where a single entry point is needed.                                                                                                              |
| **When to Use**       | This is the **most frequently used and preferred** approach for most systems.                        | Used when there are **very few actor requests** or the UI **cannot route** requests to different controllers (e.g., in system-to-system communication like interlibrary loan). |
| **Naming Convention** | Named after the use case it handles (e.g., `Checkout Controller`, `Login Controller`).               | Represents the entire system or organization.                                                                                                                                  |
| **Impact of Change**  | Changes to requirements are confined to a specific controller, making the system easier to maintain. | A change can impact this single, overarching controller, which may handle many different types of requests.                                                                    |
### Case controller



### Facade controller



# Wednesday

IDK


# Friday

Wasnt here

