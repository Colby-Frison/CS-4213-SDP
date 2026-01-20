# Diagram Creation Notes

This document describes the design decisions and creation process for the UML diagrams created for Assignment 3: MVC Design and Refactoring.

## MVC Class Diagram

### Design Decisions

**System Choice: Note-taking Application**
The note-taking application was selected as it provides a clear separation of concerns that naturally maps to the MVC pattern. The system includes:
- Rich data entities (Note, Notebook, Tag) that form the Model
- Multiple user interface components (List, Editor, Search, Category views) that form the View
- Coordination logic (Controllers) that mediate between Model and View

**Model Components:**
- **Note**: Core entity representing a single note with title, content, timestamps, and tags
- **Notebook**: Container for organizing multiple notes
- **Tag**: Categorization system allowing notes to be tagged with multiple categories
- **NoteRepository**: Data access layer handling persistence operations

The Model layer follows the principle of encapsulation, where each entity manages its own data and provides controlled access through getters and setters. The repository pattern is used to abstract data storage operations.

**View Components:**
- **NoteListView**: Displays a list of all notes with basic information
- **NoteEditorView**: Rich text editor interface for creating and editing notes
- **SearchView**: Search interface allowing users to find notes by content
- **CategoryView**: Interface for managing tags and categories

Each view component is responsible only for presentation logic and user interaction. Views notify controllers of user actions but do not directly manipulate the model.

**Controller Components:**
- **NoteController**: Handles all note-related operations (CRUD)
- **SearchController**: Manages search functionality and query processing
- **CategoryController**: Handles tag and category management

Controllers coordinate between views and the model. They receive user input from views, perform necessary operations on the model through the repository, and update views with results.

**Relationships:**
- Controllers depend on repositories (dependency relationship)
- Controllers update views (dependency relationship)
- Views notify controllers of user actions (dependency relationship)
- Model entities have associations (Note-Tag many-to-many, Notebook-Note one-to-many)

### PlantUML Implementation Notes

The diagram uses PlantUML packages to clearly separate Model, View, and Controller components. Notes are added to highlight the role of each component type. The diagram emphasizes:
1. Clear separation between the three MVC layers
2. Dependency direction (controllers depend on repositories, views depend on controllers)
3. Model relationships (associations between Note, Tag, and Notebook)

## MVC Sequence Diagram

### Design Decisions

**Interaction Selected: Create Note**
The "Create Note" interaction was chosen as it demonstrates a complete user workflow that involves all MVC components:
1. User initiates action through View
2. View notifies Controller
3. Controller coordinates with Model and Repository
4. Controller updates View with results
5. User sees feedback

**Sequence Flow:**
1. **User Action**: User clicks "New Note" button in the editor view
2. **View to Controller**: View notifies controller of the action
3. **Controller Creates Model**: Controller instantiates a new Note object
4. **Persistence**: Controller saves the note through the repository
5. **View Update**: Controller updates the view to display the new note
6. **User Input**: User enters title and content
7. **Validation**: Controller validates the input
8. **Save Operation**: If valid, controller updates the note and saves it
9. **Feedback**: View displays success or error message to user

**Key Design Elements:**
- **Activation boxes** show when each component is active
- **Alt blocks** demonstrate conditional flow (validation success/failure)
- **Message labels** clearly indicate the operation being performed
- **Return messages** show data flow back through the system

The sequence diagram illustrates the asynchronous nature of MVC interactions, where the controller acts as a mediator between the view and model, ensuring proper separation of concerns.

### PlantUML Implementation Notes

The sequence diagram uses:
- Actor notation for the User
- Participant notation for system components
- Activation boxes to show active periods
- Alt blocks for conditional logic (validation)
- Clear message naming following the pattern: `operation(parameters)`

## Refactoring Diagrams

### Refactoring 1: Extract Interface (Flexibility)

**Purpose**: Show how extracting an interface improves flexibility by allowing different storage implementations.

**Before State**: NoteController directly depends on FileStorage, making it impossible to switch to DatabaseStorage without modifying the controller.

**After State**: NoteController depends on IStorageRepository interface, allowing any implementation (FileStorage, DatabaseStorage, CloudStorage) to be used interchangeably.

**Key Elements**:
- Interface definition with common operations
- Multiple concrete implementations
- Dependency inversion principle application

### Refactoring 2: Extract Class (Reuse)

**Purpose**: Demonstrate how extracting validation logic into a separate class eliminates code duplication.

**Before State**: Validation and sanitization methods are duplicated across NoteController, SearchController, and CategoryController.

**After State**: All validation logic is centralized in NoteValidator class, which is used by all controllers.

**Key Elements**:
- Extracted validator class with reusable methods
- ValidationResult class for structured error handling
- Dependency relationships showing controller usage

### Refactoring 3: Extract Service Layer (Testability)

**Purpose**: Show how separating business logic from controller improves testability.

**Before State**: Business logic (word count, formatting, duplicate checking) is mixed with controller coordination logic.

**After State**: Business logic is extracted to NoteService layer, which can be unit tested independently of the controller and view.

**Key Elements**:
- Service layer between controller and repository
- Business logic methods in service
- Controller becomes a thin coordination layer

## General Diagram Guidelines

All diagrams follow these principles:
1. **Clarity**: Each diagram focuses on a single concept or interaction
2. **Completeness**: All necessary components and relationships are shown
3. **Consistency**: Naming conventions and notation are consistent across diagrams
4. **Readability**: Appropriate use of packages, notes, and spacing for clarity

The PlantUML format was chosen for its:
- Text-based source control friendliness
- Wide tool support (IDEs, documentation generators)
- Ability to generate high-quality images
- Version control compatibility

