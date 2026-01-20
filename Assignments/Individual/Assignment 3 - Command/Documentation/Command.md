# Command Pattern Summary

## Pattern Overview

The **Command Pattern** is a behavioral design pattern that encapsulates requests as objects, allowing you to parameterize clients with different requests, queue or log requests, and support undoable operations.

## Core Components

### 1. **Command Interface**
- Defines a uniform interface for all concrete commands
- Typically includes:
  - `execute()`: Performs the operation
  - `undo()`: Reverses the execute operation (optional)
  - `redo()`: Reverses the last undo (optional)
  - `reversible()`: boolean indicating if command can be undone

### 2. **Concrete Commands**
- Implement the Command interface
- Each subclass handles one specific operation
- Store parameters needed for execution
- Examples from the persistence framework:
  - `GetUser`, `GetBook`, `SaveBook`, `SaveLoan`

### 3. **Client**
- Creates command objects
- Invokes `execute()` methods in desired order
- Can queue commands for later execution
- In the example: `RDBImpl` acts as the client

### 4. **Invoker** (optional)
- Stores and executes commands
- Manages undo/redo stacks

## Implementation in Persistence Framework

### Database Context Problem
- Traditional database implementations have 2*N operations for N object classes
- Leads to large, hard-to-maintain classes
- Command pattern distributes responsibilities

### Design Solution

```java
// Command Interface
interface DBCmd {
    public Object execute();
}

// Concrete Command Example
class GetUser implements DBCmd {
    String uid;
    String username, password;
    Connection conn;
    
    public GetUser(String uid) {
        this.uid = uid;
    }
    
    public Object execute() {
        User user = new User();
        try {
            // Load JDBC driver, connect to database
            Class.forName(driver);
            conn = DriverManager.getConnection(url, username, password);
            Statement stmt = conn.createStatement();
            
            // Execute query
            String query = "SELECT * FROM User WHERE uid='" + uid + "'";
            ResultSet rs = stmt.executeQuery(query);
            
            // Process results
            user.setUid(rs.getString("uid"));
            user.setName(rs.getString("Name"));
            
            stmt.close();
            conn.close();
        } catch(Exception e) {
            e.printStackTrace();
        }
        return user;
    }
}

// Client Usage in RDBImpl
public class RDBImpl implements DBImplInterface {
    public User getUser(String uid) {
        DBCmd cmd = new GetUser(uid);
        return (User) cmd.execute();
    }
    
    public void saveBook(Book b) {
        DBCmd cmd = new SaveBook(b);
        cmd.execute();
    }
}
```

## Undo/Redo Mechanism

### Required Components:
- **executed stack**: Stores successfully executed commands
- **undone stack**: Stores commands that have been undone

### Process Flow:
1. **Undo**: 
   - Check if top command is reversible
   - Pop from executed stack, call `undo()`
   - Push to undone stack

2. **Redo**:
   - Pop from undone stack, call `redo()`
   - Push to executed stack

## Benefits

### 1. **Code Organization**
- Reduces size of delegating classes (DBMgr)
- Each command handles one specific operation

### 2. **Flexibility**
- Easy to add new commands
- Commands can be composed using Composite pattern
- Dynamic command generation and loading

### 3. **Advanced Features**
- Command queuing for later execution
- Undo/redo capabilities
- Logging for system recovery
- Dynamic execution sequence changes

### 4. **Separation of Concerns**
- High cohesion: Each command does one thing
- Clear responsibility assignment

## Related Patterns

### **Command vs Bridge**
- **Command**: Different functionalities, client creates/invokes commands
- **Bridge**: Same functionality for different platforms, client doesn't create implementations

### **Command vs Strategy**
- **Command**: Different operations
- **Strategy**: Same operation with different algorithms

## Practical Applications

1. **Persistence Frameworks**: Database operations as commands
2. **Editor Applications**: Undo/redo functionality
3. **Agent Systems**: Action planning and execution
4. **Testing Frameworks**: Test case execution (e.g., JUnit)
5. **Fault-Tolerant Systems**: Logging and recovery

## Liabilities
- Increased number of classes to design and implement
- Additional complexity for simple scenarios

The Command Pattern is particularly valuable in systems requiring flexible operation execution, undo/redo capabilities, or where operations need to be treated as first-class objects that can be stored, queued, and manipulated dynamically.