# Weekly question

On next week

---

# Monday

> Case study on page 548 
> Visitor pattern on page 561

## Visitor pattern skeleton for case study

```java
import java.util.*;

// Visitor Interface
interface DiagramVisitor {
    void visit(State state);
    void visit(Transition transition);
}

// Element Interface
interface Element {
    void accept(DiagramVisitor visitor);
}

// Concrete Elements
class State implements Element {
    private String name;
    
    public State(String name) { this.name = name; }
    
    @Override
    public void accept(DiagramVisitor visitor) {
        visitor.visit(this);
    }
    
    public String getName() { return name; }
}

class Transition implements Element {
    private String name;
    
    public Transition(String name) { this.name = name; }
    
    @Override
    public void accept(DiagramVisitor visitor) {
        visitor.visit(this);
    }
    
    public String getName() { return name; }
}

// Concrete Visitors
class DisplayVisitor implements Visitor {
    @Override
    public void visit(State state) {
        System.out.println("Display state: " + state.getName());
    }
    
    @Override
    public void visit(Transition transition) {
        System.out.println("Display transition: " + transition.getName());
    }
}

class EditVisitor implements Visitor {
    @Override
    public void visit(State state) {
        System.out.println("Edit state: " + state.getName());
    }
    
    @Override
    public void visit(Transition transition) {
        System.out.println("Edit transition: " + transition.getName());
    }
}

// Object Structure
class StateDiagram {
    private List<Element> elements = new ArrayList<>();
    
    public void addElement(Element element) {
        elements.add(element);
    }
    
    public void applyVisitor(Visitor visitor) {
        for (Element element : elements) {
            element.accept(visitor);
        }
    }
}

// Controller
class DiagramController {
    private StateDiagram diagram = new StateDiagram();
    
    public void addState() {
        State state = new State("State " + (diagram.elements.size() + 1));
        diagram.addElement(state);
        
        DisplayVisitor display = new DisplayVisitor();
        state.accept(display);
    }
    
    public void addTransition() {
        Transition transition = new Transition("Transition " + (diagram.elements.size() + 1));
        diagram.addElement(transition);
        
        DisplayVisitor display = new DisplayVisitor();
        transition.accept(display);
    }
    
    public void editElement(Element element) {
        EditVisitor editor = new EditVisitor();
        element.accept(editor);
    }
}

// Demo
public class SimpleVisitorDemo {
    public static void main(String[] args) {
        DiagramController controller = new DiagramController();
        
        // Simulate user actions
        controller.addState();
        controller.addState(); 
        controller.addTransition();
        
        // Edit first state
        State firstState = new State("State 1");
        controller.editElement(firstState);
    }
}
```

# Wednesday

Presenting, and starting M9S3&4

# Friday

## Abstract Factory Pattern

**Category:** Creational  
**Intent:** Create families of related objects without specifying concrete classes  
**Context:** Creating different visual themes (Windows, Mac, Dark Mode) for the diagram editor's UI  
**Participants:** `ThemeFactory`, `LightThemeFactory`, `DarkThemeFactory`, `StateRenderer`, `TransitionRenderer`  
**Consequences:** ✅ Easy theme switching ✅ Consistent look ❌ Overhead for simple cases  

```java
// Abstract Factory for visual themes
interface ThemeFactory {
    StateRenderer createStateRenderer();
    TransitionRenderer createTransitionRenderer();
}

class LightThemeFactory implements ThemeFactory {
    public StateRenderer createStateRenderer() { 
        return new LightStateRenderer(); 
    }
    public TransitionRenderer createTransitionRenderer() { 
        return new LightTransitionRenderer(); 
    }
}

class DarkThemeFactory implements ThemeFactory {
    public StateRenderer createStateRenderer() { 
        return new DarkStateRenderer(); 
    }
    public TransitionRenderer createTransitionRenderer() { 
        return new DarkTransitionRenderer(); 
    }
}

// Usage in editor
public class DiagramEditor {
    private ThemeFactory theme;
    
    public void setTheme(ThemeFactory theme) {
        this.theme = theme;
        refreshDisplay();
    }
}
```

---

## Builder Pattern

**Category:** Creational  
**Intent:** Construct complex objects step by step  
**Context:** Building State objects with multiple properties (position, size, color, name, actions)  
**Participants:** `StateBuilder`, `State`, `DiagramController`  
**Consequences:** ✅ Flexible construction ✅ Clear object creation ❌ Additional complexity  

```java
// Builder for complex State objects
class StateBuilder {
    private String name = "Unnamed State";
    private int x = 0, y = 0;
    private int radius = 25;
    private Color color = Color.BLUE;
    
    public StateBuilder withName(String name) {
        this.name = name;
        return this;
    }
    
    public StateBuilder atPosition(int x, int y) {
        this.x = x;
        this.y = y;
        return this;
    }
    
    public StateBuilder withRadius(int radius) {
        this.radius = radius;
        return this;
    }
    
    public StateBuilder withColor(Color color) {
        this.color = color;
        return this;
    }
    
    public State build() {
        return new State(name, x, y, radius, color);
    }
}

// Usage when creating new states
public class DiagramController {
    public void createState() {
        State state = new StateBuilder()
            .withName("Initial State")
            .atPosition(100, 150)
            .withRadius(30)
            .withColor(Color.GREEN)
            .build();
        diagram.addElement(state);
    }
}
```

---

## Flyweight Pattern

**Category:** Structural  
**Intent:** Share common object state to support large quantities efficiently  
**Context:** Managing thousands of identical state icons/transition arrows in large diagrams  
**Participants:** `FlyweightFactory`, `IconFlyweight`, `State` (extrinsic state)  
**Consequences:** ✅ Massive memory savings ✅ Performance ❌ Complex state management  

```java
// Flyweight for shared visual properties
class IconFlyweight {
    private final Image iconImage;
    private final String iconType;
    
    public IconFlyweight(String iconType, String imagePath) {
        this.iconType = iconType;
        this.iconImage = loadImage(imagePath);
    }
    
    public void draw(Graphics g, int x, int y, String label) {
        // Draw shared icon image at specific position with label
        g.drawImage(iconImage, x, y, null);
        g.drawString(label, x, y + 35);
    }
}

class IconFactory {
    private static Map<String, IconFlyweight> icons = new HashMap<>();
    
    public static IconFlyweight getIcon(String type) {
        if (!icons.containsKey(type)) {
            if (type.equals("state")) {
                icons.put(type, new IconFlyweight("state", "/images/state.png"));
            } else if (type.equals("initial-state")) {
                icons.put(type, new IconFlyweight("initial-state", "/images/initial.png"));
            }
        }
        return icons.get(type);
    }
}

// State stores only extrinsic (unique) state
class State {
    private int x, y;
    private String name;
    private IconFlyweight icon; // Shared across all states
    
    public State(String name, int x, int y) {
        this.name = name;
        this.x = x;
        this.y = y;
        this.icon = IconFactory.getIcon("state");
    }
    
    public void draw(Graphics g) {
        icon.draw(g, x, y, name); // Delegate to shared flyweight
    }
}
```

---

## Most Important: Flyweight Pattern

**Why Flyweight Wins:** Large state diagrams can contain thousands of visual elements with identical rendering properties. Flyweight enables handling complex, real-world diagrams without memory bloat or performance degradation—making the editor scalable and professional-grade for enterprise use.

**Key Advantage:** Memory efficiency when dealing with large diagrams containing hundreds of states and transitions, all sharing common visual characteristics.