# Instructions
In this activity, you will work **individually and in groups** to study and compare the **23 Gang of Four (GoF) design patterns**.
### Objective:
- Gain hands-on familiarity with **Creational, Structural, and Behavioral** design patterns.
- Learn how to **compare, and contrast** patterns effectively.
- Practice working as a group to build a **collective understanding** and share insights.
### Instructions:

#### Step 1 – Group Assignment
- Using the [assigned pattern](https://sooners-my.sharepoint.com/:x:/g/personal/m_hak_ou_edu/EWv-yzYRCmdAvagVhQBHy9cBufzXixe7lO2gw-6bOu8hJw?e=ZxpKpz&nav=MTVfezAyNDMwMTQ0LUU0NjctNDZDRi1BN0Q2LTkxQzA5NERDRjVDN30)
	- Abstract Factory, Adapter, Visitor

- [Links to an external site.](https://sooners-my.sharepoint.com/:x:/g/personal/m_hak_ou_edu/EWv-yzYRCmdAvagVhQBHy9cBufzXixe7lO2gw-6bOu8hJw?e=ZxpKpz&nav=MTVfezAyNDMwMTQ0LUU0NjctNDZDRi1BN0Q2LTkxQzA5NERDRjVDN30). 
- Each student will be assigned **3 patterns**:
    - **1 Creational** (from 5 total)
    - **1 Structural** (from 7 total)
    - **1 Behavioral** (from 11 total)
- Within your group, no two members will have the same set of patterns. 
#### Step 2 – Individual Work (3 Patterns per Student)
For each of your assigned patterns, find the **1-page specification on your Text Book and Study it.** 
#### Step 3 – Group Work
As a group, consolidate your 15 patterns into:
1. A **Comparison Sheet (1–2 pages)
    - Table with **Intent** and **When to Use** for each pattern.
    - 2 short contrasts per category (e.g., _Factory Method vs. Abstract Factory_).
2. A **Presentation (4 minutes)
    - **Slide 1:** Overview – “Our 15 patterns at a glance”
    - **Slides 2–4:** One slide per category (Creational, Structural, Behavioral) with commonalities + 1 tricky trade-off.
    - **Slide 5:** A mini case – one example from a teammate’s real-world use.

#### Step 4 – Presentations
- Presentations will be split across class sessions.
- Each group will have **4 minutes max**.
- All group members should contribute (briefly).

# Assigned pattern
| **Abstract Factory** | You want to create objects of different families and hide from the client which family of objects is created.                           |
| :------------------- | :-------------------------------------------------------------------------------------------------------------------------------------- |
| **Adapter**          | You want to convert one interface to another.                                                                                           |
| **Visitor**          | You want to decouple type-dependent operations from their respective classes (to achieve high cohesion and designing "stupid objects"). |

## All patterns from group

| Abstract Factory | Adapter   | Visitor                 |
| ---------------- | --------- | ----------------------- |
| Builder          | Bridge    | Chain of Responsibility |
| Factory Method   | Composite | Command                 |
| Prototype        | Decorator | Interpreter             |
| Singleton        | Facade    | Iterator                |

## Abstract Factory
### Core Concept: Factories of Factories

Think of the Abstract Factory as a "super-factory" or a "factory of factories." Its primary goal is to isolate the creation of objects from their usage. The client code only interacts with interfaces and abstract classes, making it completely decoupled from the concrete implementations.

---

### 1. The "Why": Problem it Solves

Imagine you are building a cross-platform UI library. Your application needs to render buttons, text fields, and menus. However, these UI elements look and behave completely differently on Windows vs. macOS vs. Linux.

A naive approach would be to litter your code with conditional statements:
```java
if (OS == "Windows") {
    button = new WindowsButton();
} else if (OS == "Mac") {
    button = new MacButton();
} else {
    button = new LinuxButton();
}
// ... repeat for every single UI element
```

**Problems with this approach:**
1.  **Violates Open/Closed Principle:** Adding a new OS (e.g., Android) requires modifying every single conditional block in your code.
2.  **Tight Coupling:** Your application logic is tightly coupled to concrete classes (`WindowsButton`, `MacButton`).
3.  **Error-Prone:** It's easy to create a `WindowsButton` but a `MacMenu` by mistake, creating an inconsistent UI.

The Abstract Factory pattern solves this by ensuring that you get a **complete, consistent family of products** (all Windows widgets or all Mac widgets).

---

### 2. The Key Participants (UML Components)

The pattern typically involves these interfaces and classes:

1.  **AbstractFactory:** Declares an interface of `create` methods for each kind of product (e.g., `createButton()`, `createTextField()`). This is the heart of the pattern.
2.  **ConcreteFactory:** Implements the `AbstractFactory` interface to create products belonging to a specific family (e.g., `WindowsFactory`, `MacFactory`). Each factory is responsible for creating a full set of products that are designed to work together.
3.  **AbstractProduct:** Declares an interface for a type of product (e.g., `Button`, `TextField`).
4.  **ConcreteProduct:** Implements the `AbstractProduct` interface. These are the actual objects created by the `ConcreteFactory` (e.g., `WindowsButton`, `MacButton`).
5.  **Client:** The code that uses the `AbstractFactory` and `AbstractProduct` interfaces. It is completely decoupled from the concrete implementations.

---

### 3. The Flow of Information: A Step-by-Step Walkthrough

Let's map the theoretical components to a real example: creating a UI for a cross-platform application.

**Step 1: Define the Abstract Products**
First, you define what you need to create. These are interfaces that all concrete products will implement.
```java
// Abstract Product A
public interface Button {
    void render();
    void onClick();
}

// Abstract Product B
public interface TextField {
    void render();
    String getText();
}
```

**Step 2: Define the Concrete Products**
Next, create the actual implementations for each platform.
```java
// Concrete Product A1
public class WindowsButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering a button in Windows style");
    }
    @Override
    public void onClick() {
        System.out.println("Windows button clicked!");
    }
}

// Concrete Product A2
public class MacButton implements Button {
    @Override
    public void render() {
        System.out.println("Rendering a button in macOS style");
    }
    @Override
    public void onClick() {
        System.out.println("Mac button clicked!");
    }
}

// ... Similarly, define WindowsTextField and MacTextField
```

**Step 3: Define the Abstract Factory**
This interface declares methods for creating *each type* of abstract product. It's the contract that all concrete factories must follow.
```java
public interface GUIFactory { // The Abstract Factory
    Button createButton();
    TextField createTextField();
}
```

**Step 4: Define the Concrete Factories**
These factories are the "kits" that produce a full set of compatible products.
```java
public class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton(); // Creates the Windows variant
    }
    @Override
    public TextField createTextField() {
        return new WindowsTextField(); // Creates the Windows variant
    }
}

public class MacFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacButton(); // Creates the Mac variant
    }
    @Override
    public TextField createTextField() {
        return new MacTextField(); // Creates the Mac variant
    }
}
```
**Crucial Point:** A `WindowsFactory` will *only ever* create `WindowsButton` and `WindowsTextField`. This enforces consistency.

**Step 5: The Client Code**
The client is the most important part of the flow. It only knows about the abstract interfaces (`GUIFactory`, `Button`, `TextField`). It has no knowledge of `WindowsButton`, `MacFactory`, etc.

```java
public class Application {
    private GUIFactory factory;
    private Button button;
    private TextField textField;

    // The client is given a concrete factory at runtime.
    // This is often done through a configuration file or environment variable.
    public Application(GUIFactory factory) {
        this.factory = factory;
    }

    public void createUI() {
        // The client uses the ABSTRACT factory methods.
        // It doesn't know which concrete products are being created.
        this.button = factory.createButton();
        this.textField = factory.createTextField();
    }

    public void render() {
        button.render();
        textField.render();
    }
}
```

**Step 6: Configuring the Application (The "Glue")**
Finally, you need a piece of code, often called the "composition root," that decides which concrete factory to instantiate and inject into the client. This is the *only* place where concrete classes are mentioned.

```java
public class ApplicationConfigurator {
    public static void main(String[] args) {
        GUIFactory factory;
        String osName = System.getProperty("os.name").toLowerCase();

        // This conditional is now in ONE PLACE ONLY.
        if (osName.contains("win")) {
            factory = new WindowsFactory();
        } else if (osName.contains("mac")) {
            factory = new MacFactory();
        } else {
            throw new RuntimeException("Unknown OS: " + osName);
        }

        // The client is blissfully unaware of the OS-specific logic.
        Application app = new Application(factory);
        app.createUI();
        app.render();
    }
}
```

---

### 4. Flow of Information Summary

The flow can be visualized as a directed graph of dependencies:

**Client Code (`Application`)** ---depends-on---> **`GUIFactory`** & **`Button`/`TextField` Interfaces**

**`WindowsFactory`** ---implements---> **`GUIFactory`**
**`WindowsFactory`** ---creates---> **`WindowsButton`** ---implements---> **`Button`**
**`WindowsFactory`** ---creates---> **`WindowsTextField`** ---implements---> **`TextField`**

The **Client** is at the top, only pointing downward to the abstractions. The concrete implementations point upward to fulfill those abstractions. This is the essence of **Dependency Inversion**.

The configuration logic (`ApplicationConfigurator`) is the "wire" that connects the abstract client to the concrete factory needed for the current environment.

---

### 5. Key Benefits and When to Use

**Benefits:**
*   **Consistency:** Guarantees that the products you create are always compatible (all Windows or all Mac).
*   **Loose Coupling:** Client code is completely decoupled from concrete product classes. It only uses abstract interfaces.
*   **Single Responsibility Principle:** The creation code is centralized in the concrete factories.
*   **Open/Closed Principle:** Introducing a new product family (e.g., a `LinuxFactory`) is easy. You just create a new concrete factory and its products. The *client code does not change*.

**When to Use It:**
*   When a system must be independent of how its products are created, composed, and represented.
*   When a system must be configured with one of multiple families of products.
*   When you want to provide a class library of products, and you want to reveal their interfaces, not their implementations.
*   When the lifetime of a product is shorter than the lifetime of the client, and you need to easily swap product families.

**Drawbacks:**
*   **Complexity:** It adds a significant number of new interfaces and classes, which can make the codebase more complex for a simple scenario. **Don't use it if you only have one product family or if the conditional `if` statements are simpler.**
*   **Adding New Products is Hard:** If you need to add a new product type (e.g., a `Checkbox`), you must modify the `AbstractFactory` interface and *all* existing `ConcreteFactory` implementations. This can be a breaking change.

The Abstract Factory is a powerful pattern for enforcing consistency across large systems and is a cornerstone of building highly maintainable and configurable applications.

## Adapter

### Core Concept: The Universal Plug Adapter

Imagine you have a European plug (the **Client**) and an American wall socket (the **Target Interface**). They are incompatible. The Adapter is the common travel adapter you use. It has a European socket on one side (which fits your plug) and American prongs on the other (which fit the wall socket). It translates the request for power from one format to another.

The Adapter pattern allows objects with incompatible interfaces to collaborate by wrapping itself around one of the objects and providing a compatible interface for the other.

---

### 1. The "Why": Problem it Solves

You have an existing class (`Adaptee`) that has a useful functionality but an interface that doesn't match the one your client code expects. You cannot change the client code to use this strange interface, and you might not even have the source code for the `Adaptee` to change it.

**Without an Adapter, you might try to force the client to work with the incompatible interface, leading to:**
1.  **Brittle Code:** The client becomes tightly coupled to a specific, awkward interface.
2.  **Code Duplication:** You might write glue code throughout your application to handle the translation.
3.  **Violation of SRP (Single-Responsibility Principle):** Your business logic gets polluted with interface conversion code.

The Adapter pattern solves this by creating a middle-layer class that handles the conversion, allowing the client to work with the `Adaptee` through a familiar interface.

---

### 2. The Key Participants (UML Components)

There are two common implementations of the Adapter pattern: the **Class Adapter** (which uses inheritance) and the **Object Adapter** (which uses composition). The Object Adapter is more common and flexible, so we'll focus on it.

1.  **Target:** This is the interface that the **Client** understands and expects to work with. It defines the domain-specific interface.
2.  **Client:** The class that contains the existing business logic. It collaborates with objects conforming to the `Target` interface.
3.  **Adaptee:** The existing class with a useful but incompatible interface. This is the class that needs to be adapted. It's often a 3rd-party or legacy class.
4.  **Adapter:** The class that implements the `Target` interface and *wraps* the `Adaptee`. It translates requests from the `Target` interface into a form the `Adaptee` can understand.

---

### 3. The Flow of Information: A Step-by-Step Walkthrough

Let's use a concrete example. Imagine your application (`Client`) is built to process data using a standard `DataParser` interface. You want to start using a powerful, advanced 3rd-party JSON library (`Adaptee`), but its methods have completely different names.

**Step 1: Define the Target Interface**
This is what your client code is hardcoded to use. It's the contract it expects.
```java
// This is the interface your Client code expects.
public interface DataParser {
    void parseData(String data);
    String getResult();
}
```

**Step 2: The Client Code**
The client is programmed to work with any object that implements the `DataParser` interface. It knows nothing about the `Adaptee`.
```java
public class Application {
    private DataParser parser;

    // The client works with any DataParser (Dependency Injection)
    public Application(DataParser parser) {
        this.parser = parser;
    }

    public void processData(String data) {
        parser.parseData(data); // Calls the Target interface method
        String result = parser.getResult(); // Calls the Target interface method
        System.out.println("Result: " + result);
    }
}
```

**Step 3: Identify the Adaptee**
This is the class we need to integrate. It has the functionality we want but a weird interface.
```java
// A powerful 3rd-party JSON library with an incompatible interface.
public class AdvancedJsonLibrary {
    // The method name and parameter are different from 'parseData'
    public void jsonStringToObject(String jsonInput) {
        System.out.println("Parsing JSON: " + jsonInput);
        // Complex parsing logic here...
    }

    // The method name is different from 'getResult'
    public String getParsedObject() {
        // Returns the parsed result
        return "{ \"name\": \"John Doe\" }";
    }
}
```

**Step 4: Create the Adapter**
This is the crucial translator. It *implements* the `Target` interface and *contains* a reference to the `Adaptee`.
```java
// The Adapter: implements the Target and wraps the Adaptee.
public class JsonLibraryAdapter implements DataParser {

    private AdvancedJsonLibrary adaptee; // Reference to the object being adapted

    public JsonLibraryAdapter(AdvancedJsonLibrary adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void parseData(String data) {
        // Translate the 'parseData' call to the Adaptee's 'jsonStringToObject' call.
        adaptee.jsonStringToObject(data);
    }

    @Override
    public String getResult() {
        // Translate the 'getResult' call to the Adaptee's 'getParsedObject' call.
        return adaptee.getParsedObject();
    }
}
```

**Step 5: Glue it All Together in the "Kick-Off" (`main` method)**
This is where we wire everything up. The client remains completely unchanged.
```java
public class Demo {
    public static void main(String[] args) {
        // 1. Create the Adaptee object (the incompatible 3rd-party lib)
        AdvancedJsonLibrary jsonLibrary = new AdvancedJsonLibrary();

        // 2. Create the Adapter and wrap the Adaptee with it.
        DataParser adapter = new JsonLibraryAdapter(jsonLibrary);

        // 3. Pass the Adapter (which IS-A DataParser) to the Client.
        Application app = new Application(adapter);

        // 4. The client works correctly, unaware it's using the AdvancedJsonLibrary.
        String jsonData = "{ \"key\": \"value\" }";
        app.processData(jsonData);
    }
}
```

---

### 4. Flow of Information Summary

The flow of a single call, say `client.processData() -> parser.parseData()`, is as follows:

1.  The **Client** (`Application`) calls the `parseData(String data)` method on the object it believes is a `DataParser` (`Target`).
2.  This object is actually the **Adapter** (`JsonLibraryAdapter`).
3.  The Adapter receives this call. It understands the `Target` interface.
4.  The Adapter translates this call into a form the **Adaptee** (`AdvancedJsonLibrary`) can understand. In this case, it calls `adaptee.jsonStringToObject(data)`.
5.  The Adaptee executes its complex logic and returns (if necessary).
6.  The Adapter may then translate the return value (if necessary) and pass it back to the Client.

The client is only aware of the **Target** interface. The adaptee is only aware of its own interface. The adapter is the only component that knows about both, acting as the intermediary.

This can be visualized as:
**Client --[Target Interface]--> Adapter --[Adaptee Interface]--> Adaptee**

---

### 5. Adapter vs. Other Patterns

*   **Adapter vs. Facade:** Both wrap other objects, but their intentions differ. A **Facade** provides a *simplified* interface to a complex subsystem. An **Adapter** provides a *different* interface to an existing object, not necessarily a simpler one. The Adapter is designed to be used *in place of* the original object, while the Facade is a new entry point to many objects.
*   **Adapter vs. Decorator:** A **Decorator** *adds* new behavior to an object without changing its interface (it enhances it). An **Adapter** *changes* the interface of an object to make it compatible (it converts it).
*   **Adapter vs. Proxy:** A **Proxy** provides the *same* interface as its subject, controlling access to it. An **Adapter** provides a *different* interface.

---

### 6. Key Benefits and When to Use

**Benefits:**
*   **Single Responsibility Principle:** You decouple the business logic of your client from the interface conversion code.
*   **Open/Closed Principle:** You can introduce new types of adapters into your program without breaking the existing client code, as long as they work with the client through the `Target` interface.
*   **Reusability:** Allows the integration of classes that couldn't otherwise work together due to incompatible interfaces.

**When to Use It:**
*   **Integrating Legacy Code:** When you want to use an existing class whose interface isn't compatible with the rest of your code.
*   **Working with 3rd-Party Libraries:** To isolate your code from the specific interfaces of external libraries. If the library changes, you often only need to update the adapter.
*   **Interface Versioning:** When you need to provide a different interface for a class for backwards compatibility or other reasons.

The Adapter pattern is an essential tool for any developer, ensuring that systems can evolve and integrate new components without being held hostage by outdated or incompatible interfaces.

==The adapter pattern's core elements are in the adapter class, everything else stays the same besides when the adaptee object is created. This allows the SRP to stand true, completely separating the adapter from the business logic.==

## Visitor

The Visitor pattern is a powerful and complex behavioral pattern that separates an algorithm from the object structure on which it operates. It's one of the more challenging patterns to grasp, but its utility is immense for certain problems.

---

### Core Concept: The "Tax Auditor" Analogy

Imagine a company has a fixed structure of elements: `Manager`, `Engineer`, `Clerk` (these are the **Elements**). The government needs to perform various operations on all employees: calculate income **Tax**, check **Health Insurance** compliance, etc. (these are the **Visitors**).

You cannot change the core `Employee` classes every time a new government regulation comes out. The Visitor pattern is like sending a tax auditor (**Visitor**) to the company. The auditor visits each employee (**Element**), and based on the *type* of employee, performs a specific calculation. The company's structure remains unchanged; the auditing algorithm is applied *to* it.

The Visitor lets you define a new operation without changing the classes of the elements on which it operates.

---

### 1. The "Why": Problem it Solves

You have a complex object structure (e.g., a Abstract Syntax Tree, a document object model, a hierarchy of UI components) made of many different classes (e.g., `ParagraphNode`, `HeadingNode`, `ImageNode`).

You need to perform many unrelated operations on this structure (e.g., `ExportToXML`, `ApplyFontStyle`, `ExtractText`, `CountWords`).

**The naive approach leads to:**
1.  **Polluting the Classes:** Adding each new operation (e.g., `ExportToXML`) as a method to every single node class violates the **Single Responsibility Principle**. Your node classes become bloated with unrelated behavior.
2.  **Poor Maintainability:** Adding a new operation forces you to modify every class in the structure.
3.  **Impossible if Closed for Modification:** If the node classes are from a closed library, you can't add methods to them at all.

The Visitor pattern solves this by placing each new operation into a separate **Visitor** class. The object structure simply has to "accept" a visitor, and the visitor handles the rest.

---

### 2. The Key Participants (UML Components)

The pattern involves a double-dispatch mechanism, which is key to understanding it.

1.  **Visitor:** Declares a `visit` method for each *concrete* class of `Element` in the object structure. The method's name and signature identify the class, enabling the correct operation.
    *   `visitParagraph(Paragraph p)`
    *   `visitHeading(Heading h)`
2.  **Concrete Visitor:** Implements each operation defined by the `Visitor`. Each visitor is a self-contained algorithm (e.g., `XMLExportVisitor`, `TextExtractionVisitor`).
3.  **Element:** Declares an `accept` method that takes a `Visitor` as an argument. `accept(Visitor v)`
4.  **Concrete Element:** Implements the `accept` method. The implementation is always the same: `v.visitThisElement(this)`. This is the crucial "hook" that lets the visitor in.
5.  **Object Structure:** A collection or composite structure of `Element` objects (e.g., a list, a tree). Often, a client will iterate over this structure and call `accept()` on each element.

---

### 3. The Flow of Information: A Step-by-Step Walkthrough

Let's model the operations for a simple document made of different nodes.

**Step 1: Define the Element Interface and Concrete Elements**
First, we define our fixed object structure. The `accept` method is the only "operation" method they have.
```java
// Element interface
public interface DocumentNode {
    void accept(DocumentVisitor visitor);
}

// Concrete Element A
public class ParagraphNode implements DocumentNode {
    String text;

    public ParagraphNode(String text) { this.text = text; }
    public String getText() { return text; }

    // The key: It calls 'visitParagraph', passing itself.
    @Override
    public void accept(DocumentVisitor visitor) {
        visitor.visitParagraph(this);
    }
}

// Concrete Element B
public class HeadingNode implements DocumentNode {
    String title;
    int level;

    public HeadingNode(String title, int level) {
        this.title = title;
        this.level = level;
    }
    public String getTitle() { return title; }
    public int getLevel() { return level; }

    // The key: It calls 'visitHeading', passing itself.
    @Override
    public void accept(DocumentVisitor visitor) {
        visitor.visitHeading(this);
    }
}
// ... more node types (ImageNode, etc.)
```

**Step 2: Define the Visitor Interface**
This interface declares the "entry points" for every type of element. This is the contract all visitors must fulfill.
```java
// Visitor Interface
public interface DocumentVisitor {
    // A method for each concrete element type
    void visitParagraph(ParagraphNode paragraph);
    void visitHeading(HeadingNode heading);
    // void visitImage(ImageNode image);
}
```

**Step 3: Create Concrete Visitors (The Algorithms)**
Now we can create as many operations as we want *without ever touching the node classes again*.
```java
// Concrete Visitor 1: Operation for exporting to XML
public class XmlExportVisitor implements DocumentVisitor {
    @Override
    public void visitParagraph(ParagraphNode paragraph) {
        // This visitor knows exactly what to do with a ParagraphNode
        System.out.println("<paragraph>" + paragraph.getText() + "</paragraph>");
    }

    @Override
    public void visitHeading(HeadingNode heading) {
        // This visitor knows exactly what to do with a HeadingNode
        System.out.println("<h" + heading.getLevel() + ">" + heading.getTitle() + "</h" + heading.getLevel() + ">");
    }
}

// Concrete Visitor 2: Operation for extracting plain text
public class TextExtractionVisitor implements DocumentVisitor {
    private StringBuilder textBuilder = new StringBuilder();

    @Override
    public void visitParagraph(ParagraphNode paragraph) {
        textBuilder.append(paragraph.getText()).append("\n");
    }

    @Override
    public void visitHeading(HeadingNode heading) {
        textBuilder.append("*** ").append(heading.getTitle()).append(" ***\n");
    }

    public String getExtractedText() {
        return textBuilder.toString();
    }
}
// ... more visitors can be added (e.g., WordCountVisitor, HtmlExportVisitor)
```

**Step 4: The Client Code and Object Structure**
The client creates the structure and applies visitors to it.
```java
public class Document implements DocumentNode {
    private List<DocumentNode> nodes = new ArrayList<>();

    public void addNode(DocumentNode node) {
        nodes.add(node);
    }

    // The Document itself can also accept a visitor, which typically
    // means having the visitor visit all of its children.
    @Override
    public void accept(DocumentVisitor visitor) {
        for (DocumentNode node : nodes) {
            node.accept(visitor); // The crucial iteration
        }
    }
}

public class Client {
    public static void main(String[] args) {
        // 1. Build the object structure (the document)
        Document document = new Document();
        document.addNode(new HeadingNode("Introduction", 1));
        document.addNode(new ParagraphNode("This is the first paragraph."));
        document.addNode(new HeadingNode("Conclusion", 2));
        document.addNode(new ParagraphNode("This is the concluding text."));

        // 2. Create the visitors (the algorithms)
        DocumentVisitor xmlExporter = new XmlExportVisitor();
        DocumentVisitor textExtractor = new TextExtractionVisitor();

        System.out.println("=== Exporting to XML ===");
        // 3. Apply the visitor to the structure
        document.accept(xmlExporter);

        System.out.println("\n=== Extracting Text ===");
        document.accept(textExtractor);
        // For visitors that collect state, we need to get the result.
        String extractedText = ((TextExtractionVisitor) textExtractor).getExtractedText();
        System.out.println(extractedText);
    }
}
```

---

### 4. The "Double Dispatch" Flow Explained

This is the most critical concept. The flow for a single `document.accept(visitor)` call is:

1.  The `Client` calls `document.accept(xmlExporter)`.
2.  The `Document`'s `accept` method iterates and calls `node.accept(xmlExporter)` on each child node.
3.  For a `ParagraphNode`, its `accept` method is called. **The node knows its own concrete type.**
4.  The `ParagraphNode`'s `accept` method calls `visitor.visitParagraph(this)`. **It's making a method call based on its own type, passing itself as a parameter.**
5.  The `XmlExportVisitor`'s `visitParagraph(ParagraphNode p)` method is now executing. **The visitor now knows the concrete type of the node it's working with.**

This two-step process is **double dispatch**:
*   **First dispatch:** The `accept` method is chosen based on the type of the **element** (`ParagraphNode`).
*   **Second dispatch:** The `visitParagraph` method is chosen based on the type of the **visitor** (`XmlExportVisitor`).

This is how the pattern correctly associates the right operation with the right element without using type checks (`instanceof`).

---

### 5. Key Benefits, Drawbacks, and When to Use

**Benefits:**
*   **Open/Closed Principle:** You can introduce new operations (visitors) without changing the element classes.
*   **Single Responsibility Principle:** Multiple unrelated operations on the same structure are moved into their own classes.
*   **Collect State:** A visitor can accumulate state as it traverses the entire structure (e.g., the `TextExtractionVisitor`).

**Drawbacks:**
*   **Hard to Add New Elements:** If you add a new `ImageNode` class, you must update the `DocumentVisitor` interface and *all existing concrete visitors*, which can be a breaking change.
*   **Tight Coupling of Visitors to Elements:** Visitors often need to know the concrete classes of the elements, not just their interface.
*   **Can Break Encapsulation:** Visitors often require `public` getter methods on elements to do their work, potentially exposing internal state.

**When to Use It:**
*   When you have a stable hierarchy of classes (elements) but want to frequently define new operations over them.
*   When an operation must handle different classes in the hierarchy in different ways.
*   When the object structure is complex (like a composite tree) and you want to avoid polluting the element classes with unrelated behavior.

The Visitor pattern is a sophisticated tool for keeping operations cleanly separated from a stable object model, making it invaluable for tasks like compiler design (AST operations), document processing, and complex data structure analysis.

### More detail
### The Visitor Design Pattern: A Comprehensive Reference

#### 1. Introduction & Core Concept

The Visitor is a behavioral design pattern that allows you to separate algorithms from the object structures on which they operate. Its primary goal is to let you define new operations without changing the classes of the elements on which it operates.

**The Central Analogy:** Imagine a fixed company structure with different departments (Engineering, Sales, HR). You can send various auditors (a Tax Auditor, a Health Inspector, an Efficiency Expert) to the company. Each auditor performs their specific analysis by visiting each department. The company structure remains unchanged; the auditing algorithms are applied to it. The Visitor pattern formalizes this process in code.

#### 2. The Problem It Solves

When you have a complex object structure (e.g., a Abstract Syntax Tree, a document model, a UI component tree), you often need to perform many different operations (export, rendering, analysis). Adding these operations directly to the element classes leads to several problems:

*   **Violates Single Responsibility Principle:** Element classes become bloated with unrelated behaviors.
*   **Violates Open/Closed Principle:** Adding a new operation forces you to modify every single element class.
*   **Impossible with Closed Libraries:** If the element classes are from a third-party library, you cannot modify them to add new methods.

The Visitor pattern solves this by placing each new operation into a separate class, called a *visitor*.

#### 3. How It Works: The Double Dispatch Mechanism

The pattern's magic lies in a technique called **double dispatch**. It's a two-step process where the executed method depends on the runtime types of two objects: both the visitor and the element.

1.  **First Dispatch - The Element's `accept` method:** The client calls `element.accept(visitor)`. The JVM automatically chooses the correct `accept` method implementation based on the concrete type of the element (e.g., `Paragraph.accept()` vs. `Heading.accept()`).

2.  **Second Dispatch - The Visitor's `visit` method:** Inside the element's `accept` method, the element calls `visitor.visit(this)`, passing a reference to *itself*. The JVM now chooses the correct `visit` method implementation based on the concrete type of the *visitor* (e.g., `HtmlExportVisitor.visitParagraph()` vs. `TextExtractionVisitor.visitParagraph()`).

This double method call ensures the correct operation is performed on the correct element type without the need for messy `instanceof` checks.

#### 4. Key Participants (Components)

| Participant | Description | Role in the Collaboration |
| :--- | :--- | :--- |
| **Visitor** | Declares a `visit` method for each concrete `Element` class. | Defines the protocol for all operations that can be performed. |
| **Concrete Visitor** | Implements each `visit` method declared by the `Visitor`. Each visitor represents a distinct algorithm. | Contains the actual logic for a specific operation (e.g., `HtmlExportVisitor`, `TextExtractionVisitor`). |
| **Element** | Declares an `accept(Visitor v)` method. | The entry point that allows a visitor to "visit" this element. |
| **Concrete Element** | Implements the `accept` method, which is always `v.visitThisElement(this)`. | Identifies itself to the visitor and grants it access. |
| **Object Structure** | A collection or composite structure (e.g., a list, a tree) of `Element` objects. | Holds the elements and often implements an `accept` method to traverse all children. |
| **Client** | The code that uses the pattern. | Creates the concrete visitors, traverses the object structure, and calls `accept()` on each element. |

#### 5. Metaphors for Understanding

*   **The Official Tour (Not a Backdoor):** The `accept` method is not a backdoor; it is a secure, official entry point. The element is an active participant, like a department head who personally escorts a consultant (the visitor) into their department, granting them sanctioned access to its resources.
*   **The Super Getter:** A standard getter returns a single variable. A Visitor is an **algorithmic getter** or **super getter**. It's an intelligent agent that traverses an entire structure, uses complex logic to collect and process data from multiple objects, and can return a completely new, derived result (e.g., a full HTML document from individual nodes).
*   **The Original Object:** The visitor always receives a reference to the original, live element object (`this`). It does **not** work on a copy. Any operation it performs (like calling `getText()`) is done on the actual object.

#### 6. When to Use

**Use the Visitor pattern when:**
*   You need to perform many unrelated operations on a complex object structure.
*   The object structure is stable and rarely changes, but you need to frequently define new operations.
*   An operation must handle different classes in the structure in different ways.

**Avoid the Visitor pattern when:**
*   The object structure's classes change frequently (adding a new element type is very costly).
*   The operations don't need to handle different element types differently.
*   The pattern forces you to expose too much of the elements' internal state, breaking encapsulation.

#### 7. Pros and Cons

| Pros | Cons |
| :--- | :--- |
| **Open/Closed Principle:** Easily introduce new visitors without changing existing elements. | **Hard to Add New Elements:** Adding a new `ConcreteElement` requires changing the `Visitor` interface and all existing `ConcreteVisitors`. |
| **Single Responsibility Principle:** Move related behavior into a single visitor class. | **Tight Coupling:** Visitors often depend on the concrete classes of the elements, not just their interface. |
| **Accumulate State:** Visitors can collect information as they traverse the entire structure. | **Breaks Encapsulation:** Often requires elements to provide public getters for their state. |



## Prototype

#### **Explanation**
The Prototype is a creational design pattern that lets you create new objects by copying an existing object (called a prototype), rather than creating them from scratch. This is particularly useful when the construction of a new instance is more expensive (e.g., requires database calls, complex computations) than copying an existing one.

The pattern involves creating a prototype interface that declares a `clone` method. Concrete classes implement this method to return a copy of themselves. The client creates new objects by asking a prototype to clone itself, without being coupled to its concrete class.

#### **Flow of Information**
1.  A client needs a new object.
2.  Instead of using the `new` keyword, the client obtains a reference to an existing **prototype** object (often from a registry or cache).
3.  The client calls `prototype.clone()`.
4.  The prototype object's `clone` method creates a bitwise copy of itself. This can be a **shallow copy** (copying references) or a **deep copy** (copying referenced objects), depending on the need.
5.  The client receives the new, independent clone and can use it without affecting the original prototype.

#### **Code Example**
```java
// 1. The Prototype Interface
public interface Shape extends Cloneable {
    Shape clone(); // The core of the pattern
    void draw();
}

// 2. Concrete Prototype
public class Circle implements Shape {
    private int radius;

    public Circle(int radius) {
        this.radius = radius; // Suppose this is a costly operation
    }

    @Override
    public Shape clone() {
        // Create a new object with the same state
        return new Circle(this.radius);
    }

    @Override
    public void draw() {
        System.out.println("Drawing a circle with radius: " + radius);
    }
}

// 3. Client Usage
public class Client {
    public static void main(String[] args) {
        // Create a prototype instance (expensive operation)
        Circle prototypeCircle = new Circle(10);

        // Create new circles by cloning the cheap prototype
        Circle circle1 = (Circle) prototypeCircle.clone();
        Circle circle2 = (Circle) prototypeCircle.clone();

        circle1.draw(); // Drawing a circle with radius: 10
        circle2.draw(); // Drawing a circle with radius: 10
    }
}
```

**Intent:** To specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
**When to use:**
*   When the cost of creating a new instance of a class is more expensive than copying an existing one.
*   When a system should be independent of how its products are created, composed, and represented, and classes to instantiate are specified at runtime.

---

## Decorator

#### **Explanation**
The Decorator is a structural pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. It provides a flexible alternative to subclassing for extending functionality.

The pattern involves a set of decorator classes that are used to wrap concrete components. Decorators implement the same interface as the component they decorate, and they contain a reference to a component object. They delegate operations to the component and can perform additional actions before or after the delegation.

#### **Flow of Information**
1.  A **Client** needs an object with some core functionality and optional enhancements.
2.  The client starts with a **ConcreteComponent** object that implements the **Component** interface.
3.  The client wraps this component with one or more **Decorator** objects. Each decorator adds its own behavior.
4.  The client calls a method on the outermost decorator.
5.  The decorator performs its added behavior, then calls the same method on the wrapped component.
6.  This call can propagate through multiple layers of decorators before reaching the core component.
7.  The result travels back out through the decorators, which can also modify the return value.

#### **Code Example**
```java
// 1. The Core Component Interface
public interface Coffee {
    String getDescription();
    double getCost();
}

// 2. Concrete Component
public class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() { return "Simple Coffee"; }
    @Override
    public double getCost() { return 1.0; }
}

// 3. Base Decorator Class (implements the interface and holds a reference)
public abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost();
    }
}

// 4. Concrete Decorators
public class WithMilk extends CoffeeDecorator {
    public WithMilk(Coffee coffee) { super(coffee); }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Milk";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 0.5;
    }
}

public class WithSugar extends CoffeeDecorator { /* Similar implementation */ }

// 5. Client Usage
public class Client {
    public static void main(String[] args) {
        Coffee myCoffee = new SimpleCoffee(); // Base cost: 1.0
        myCoffee = new WithMilk(myCoffee);    // Cost: 1.0 + 0.5
        myCoffee = new WithSugar(myCoffee);   // Cost: 1.0 + 0.5 + 0.2

        System.out.println(myCoffee.getDescription() + " : $" + myCoffee.getCost());
        // Output: Simple Coffee, Milk, Sugar : $1.7
    }
}
```

**Intent:** To attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.
**When to use:**
*   To add responsibilities to individual objects dynamically and transparently, without affecting other objects.
*   When extension by subclassing is impractical (e.g., due to a large number of independent extensions leading to an explosion of subclasses).

---

## Interpreter

#### **Explanation**
The Interpreter is a behavioral pattern that defines a representation for a language's grammar along with an interpreter that uses the representation to interpret sentences in the language. It is effectively used to build interpreters for simple languages, such as query languages, regular expressions, or mathematical expressions.

The pattern involves defining an abstract expression class that declares an `interpret()` method. Terminal expressions represent leaf nodes in the grammar (e.g., variables, constants), while non-terminal expressions represent grammatical rules and contain other expressions (e.g., addition, loops).

#### **Flow of Information**
1.  The **Client** builds (or is given) an abstract syntax tree (AST) representing a sentence in the language. This tree is composed of **TerminalExpression** and **NonTerminalExpression** objects.
2.  The client triggers the interpretation by calling the `interpret()` method on the root of the AST.
3.  The `interpret` method is called recursively on each node in the tree.
4.  **Terminal expressions** return a value directly (often based on a context object).
5.  **Non-terminal expressions** interpret themselves by calling `interpret()` on their child expressions and then combining the results according to the grammatical rule they represent (e.g., adding two results together).
6.  The final result of the interpretation is returned from the root of the tree.

#### **Code Example (Simple Boolean Language)**
```java
import java.util.Map;

// 1. Abstract Expression
public interface Expression {
    boolean interpret(Map<String, Boolean> context);
}

// 2. Terminal Expression
public class Variable implements Expression {
    private String name;

    public Variable(String name) { this.name = name; }

    @Override
    public boolean interpret(Map<String, Boolean> context) {
        // Look up the variable's value in the context
        return context.getOrDefault(name, false);
    }
}

// 3. Non-Terminal Expressions
public class And implements Expression {
    private Expression left;
    private Expression right;

    public And(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public boolean interpret(Map<String, Boolean> context) {
        // Interpret both sides and apply the AND rule
        return left.interpret(context) && right.interpret(context);
    }
}

public class Or implements Expression { /* Similar to And */ }
public class Not implements Expression {
    private Expression expression;
    public Not(Expression expression) { this.expression = expression; }
    @Override
    public boolean interpret(Map<String, Boolean> context) {
        return !expression.interpret(context);
    }
}

// 4. Client Usage (Building and interpreting an expression: A AND B)
public class Client {
    public static void main(String[] args) {
        // Build the AST for the expression: A AND B
        Expression expression = new And(new Variable("A"), new Variable("B"));

        // Create a context (assign values to variables)
        Map<String, Boolean> context = Map.of("A", true, "B", false);

        // Interpret the expression
        boolean result = expression.interpret(context);
        System.out.println("A AND B = " + result); // Output: A AND B = false
    }
}
```

**Intent:** To define a grammatical representation for a language and provide an interpreter to deal with this grammar, allowing for the interpretation of sentences in the language.
**When to use:**
*   When you have a simple language (grammar) to interpret, and efficiency is not a critical concern.
*   When the grammar is represented as an abstract syntax tree, and each rule in the grammar can be represented as a class.

---

### **Summary: Intent & When to Use**

| Pattern         | Intent                                                             | When to Use                                                                                                                                |
| :-------------- | :----------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| **Prototype**   | Create new objects by copying an existing prototype instance.      | When object creation is costlier than copying, or when a system needs to be independent of its object creation process.                    |
| **Decorator**   | Dynamically add responsibilities to an object without subclassing. | To add functionality to individual objects transparently, especially where subclassing would lead to a combinatorial explosion of classes. |
| **Interpreter** | Define a grammar and use it to interpret sentences in a language.  | For simple languages where representing grammar rules as objects offers flexibility, and performance is not the primary concern.           |



# Comparisons

## Creational Patterns: Abstract Factory, Builder, Factory Method, Prototype, Singleton
1.  **Scope of Control:** **Abstract Factory** and **Factory Method** control *which* object is created, while **Builder** controls *how* a complex object is constructed step-by-step.
2.  **Object Management:** **Prototype** creates new objects by cloning an existing instance, whereas **Singleton** restricts instantiation to ensure only *one* instance of a class ever exists.

## Structural Patterns: Adapter, Bridge, Composite, Decorator, Facade
1.  **Relationship vs. Responsibility:** **Adapter** and **Bridge** focus on relationships between classes—Adapter makes existing interfaces work together, while Bridge decouples an abstraction from its implementation. **Decorator** focuses on dynamically adding responsibilities to an individual object.
2.  **Complexity Hiding:** **Facade** provides a simplified, unified interface to a complex subsystem, while **Composite** builds complex tree structures from simple components, treating individuals and groups uniformly.

## Behavioral Patterns: Visitor, Chain of Responsibility, Command, Interpreter, Iterator
1.  **Request Handling:** **Chain of Responsibility** passes a request along a chain of potential handlers until one processes it, promoting loose coupling between sender and receiver. In contrast, **Command** encapsulates a request as an object, allowing for parameterization and queuing of operations.
2.  **Traversal vs. Interpretation:** **Iterator** provides a way to access the elements of a collection sequentially without exposing its underlying structure. **Interpreter** defines a grammar for a language and uses it to interpret and evaluate expressions, often leveraging a tree structure built from that grammar.