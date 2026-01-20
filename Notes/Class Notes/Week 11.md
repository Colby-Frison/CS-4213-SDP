# Weekly question
**Question:** 


**Answer:** 



>From chapter 16
	16.4,16.5, 16.6,16.7
	Weekly question is for week 10&11 so first two are week 10 second 2 are week 11
---

# Monday

## Important questions

1. **Abstract Factory + Builder:** Why might you combine these two patterns in the same system?
2. **Flyweight:** What kind of shared data would you extract if implementing flyweight in a text editor?
3. **Flyweight + Composite:** How could these pattern work together?
4. Give an example where a design without a pattern led to duplicate  code, and explain which pattern could fix it.
---
1. **Composite + iterator:** how do these two pattern often complement each other.
2. **Strategy:** when could using too many strategy  objects become a maintenance issue?
3. **Memento:** What would you make when storing multiple mementos for undo/redo functionality?

## M9S3&4-Participation 5-3

Patterns to discuss: **State, Observer, Adapter, Chain of Responsibility, and Decorator.**
# Wednesday

## Observer Pattern

**Category:** Behavioral  
**Intent:** Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically  
**Context:** Multiple UI components need to react to diagram changes - properties panel, toolbar, status bar, and canvas must stay synchronized when states/transitions are modified  
**Participants:** 

**Consequences:** 
Pros:
- **Loose Coupling**
- **Dynamic Relationships**
- **Broadcast Communication**
- **Reusability**
Cons:
 - **Unpredictable Update Order**
 - **Performance Overhead**
 - **Unexpected Updates**
 - **Memory Leaks Risk** 

```java
// Observer Interface
interface DiagramObserver {
    void diagramChanged();
}

// Subject (Observable)
class DiagramModel {
    private List<DiagramObserver> observers = new ArrayList<>();
    
    public void addObserver(DiagramObserver o) {
        observers.add(o);
    }
    
    private void notifyObservers() {
        for (DiagramObserver o : observers) {
            o.diagramChanged();
        }
    }
    
    public void addState(State state) {
        // Add state logic...
        notifyObservers();
    }
    
    public void removeState(State state) {
        // Remove state logic...
        notifyObservers();
    }
}

// Concrete Observers
class Canvas implements DiagramObserver {
    public void diagramChanged() {
        System.out.println("Canvas: Redrawing diagram");
        repaint();
    }
    
    private void repaint() {
        // Redraw logic
    }
}

class PropertiesPanel implements DiagramObserver {
    public void diagramChanged() {
        System.out.println("Properties: Refreshing properties");
        refreshProperties();
    }
    
    private void refreshProperties() {
        // Update properties UI
    }
}

// Usage
public class Editor {
    public static void main(String[] args) {
        DiagramModel model = new DiagramModel();
        Canvas canvas = new Canvas();
        PropertiesPanel props = new PropertiesPanel();
        
        model.addObserver(canvas);
        model.addObserver(props);
        
        // All observers notified automatically
        model.addState(new State("Initial"));
    }
}
```


## Adapter Pattern

```java
// Target Interface (what the client expects)
interface DiagramExporter {
    void export(Diagram diagram, String filename);
}

// Adaptee (incompatible existing class)
class LegacyXMLSerializer {
    public void saveToXML(Object data, String filePath) {
        System.out.println("LegacyXMLSerializer: Saving to " + filePath);
        // Complex legacy XML serialization logic
    }
}

// Adapter (makes Adaptee work with Target interface)
class XMLExporterAdapter implements DiagramExporter {
    private LegacyXMLSerializer legacySerializer;
    
    public XMLExporterAdapter(LegacyXMLSerializer serializer) {
        this.legacySerializer = serializer;
    }
    
    @Override
    public void export(Diagram diagram, String filename) {
        // Adapt the interface - convert Diagram to Object, filename to filePath
        legacySerializer.saveToXML(diagram, "exports/" + filename + ".xml");
    }
}

// Another Adaptee
class JsonWriter {
    public void writeJson(Object obj, String outputFile) {
        System.out.println("JsonWriter: Writing JSON to " + outputFile);
        // JSON serialization logic
    }
}

// Another Adapter
class JsonExporterAdapter implements DiagramExporter {
    private JsonWriter jsonWriter;
    
    public JsonExporterAdapter(JsonWriter writer) {
        this.jsonWriter = writer;
    }
    
    @Override
    public void export(Diagram diagram, String filename) {
        jsonWriter.writeJson(diagram, filename + ".json");
    }
}

// Client code that uses the Target interface
class ExportManager {
    public void exportDiagram(DiagramExporter exporter, Diagram diagram, String name) {
        exporter.export(diagram, name);
    }
}

// Demo
public class AdapterDemo {
    public static void main(String[] args) {
        Diagram diagram = new Diagram();
        ExportManager exportManager = new ExportManager();
        
        // Use legacy XML serializer through adapter
        DiagramExporter xmlExporter = new XMLExporterAdapter(new LegacyXMLSerializer());
        exportManager.exportDiagram(xmlExporter, diagram, "my-diagram");
        
        // Use JSON writer through adapter  
        DiagramExporter jsonExporter = new JsonExporterAdapter(new JsonWriter());
        exportManager.exportDiagram(jsonExporter, diagram, "my-diagram");
    }
}
```

```java

//output:
LegacyXMLSerializer: Saving to exports/my-diagram.xml
JsonWriter: Writing JSON to my-diagram.json

```



# Friday
