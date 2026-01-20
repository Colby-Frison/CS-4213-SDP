Hunter Merrill (He/Him/His)
Sep 18 8:04pm
Reply from Hunter Merrill

Group J

Which design pattern should be used to reduce the work load of a bloated controller?
A) Expert
B) Creator
C) Controller
D) None of the above

Which of the following principles describes a Controller that does everything itself?
A) Bloat
B) Low coupling
C) Information hiding
D) Simple and stupid

In which of the following scenarios is it not appropriate to use the Creator pattern for Class A?
A) An object of Class A is instantiated within objects of Class B
B) An object of Class A contains objects of Class B
C) An object of Class A records objects of Class B
D) An object of Class A closely uses objects of Class B

Reply to post from Hunter MerrillReply

    Mark as UnreadMark as Unread

Deleted by Caleb Miller
Deleted Sep 19 9:43am

AS
Abdulmalik Shodunke
Sep 19 10:57am | Last edited Sep 19 10:58am
Reply from Abdulmalik Shodunke

Group M

Given multiple use cases for a problem in an application, which of the following would benefit from a controller pattern?

A. A web application with multiple functionalities to handle and process.

B. A database with several accessors to an instance that all others need.

C. A System-on-a-Chip pipeline to upload and compile code.

D. An interface that allows dynamic production of different methods to achieve a result.

 
Which pattern assigns a responsibility to the object that has the information necessary to fulfill that responsibility?
A. Expert Pattern
B. Controller Pattern
C. Creator Pattern
D. Strategy Pattern

 
What is the main idea of the Creator pattern?
A. Give the responsibility for creating an object to a class that closely uses or contains it.
B. Always let the controller class create every object in the system.
C. Require a separate factory class for every single object you make.
D. Create all objects inside the database manager.

Reply to post from Abdulmalik ShodunkeReply

    Mark as UnreadMark as Unread

Mark post as read
AZ
Antonio Natusch Zarco (He/Him/His)
Sep 19 11:27pm
Reply from Antonio Natusch Zarco

Group H

    Which of the following is NOT a benefit of the Expert GRASP pattern?,

a) Designing “smart object.”

b) Easy to understand and change due to high cohesion and low coupling.

c) High cohesion because responsibilities are assigned to objects that can fulfill the responsibilities.

d) Low coupling because the given request is handled directly by the object that has the information to fulfill the request

    What is a bloated controller?

a) A controller that is overloaded with excessive responsibilities

b) A controller who only has one responsibility

c) A controller that possesses high cohesion

d) A controller that is decoupled from a given database schema

 

 3. Which of the following criteria should be taken into account when implementing the Creator pattern?

a) Class A is an aggregation of Class B

b) An object of Class A partially contains objects of Class B

c) An object of Class A does not record objects of Class B

d) An object of Class A loosely uses objects of Class B 

Reply to post from Antonio Natusch ZarcoReply

    Mark as ReadMark as Read

Mark post as read
HH
Hyde Harris (He/Him/His)
Sep 21 9:16pm
Reply from Hyde Harris

Group F

1) What is an anti-expert?

A. A design that violates the expert pattern

B. A stupid object

C. An expert pattern that involves more than one object

D. A pattern where responsibilities are assigned objects with the information to fulfill the request.

2) How is object creation accomplished?

A. By calling the constructor of a class.

B. By defining a new method within the class.

C. By creating a new instance of an interface.

D. By using a special "factory" function.

3) Which of the following is NOT accomplished by the expert pattern?

A. Creates a generalized handler for all inputs.

B. Removes excess responsibilities from the controller.

C. Allows for "stupid objects."

D. Creates a low coupling and high cohesion design.

Reply to post from Hyde HarrisReply

    Mark as ReadMark as Read

Mark post as read
Barrett Ray (He/They)
Sep 21 10:13pm
Reply from Barrett Ray
Group E

    1. What is NOT a cure for bloated controllers? 
        (a) remove other objects and assign their duties to the controller
        (b) replace the controller with use case controllers to handle use case related events
        (c) change the controller to delegate responsibilities to appropriate business objects
        (d) apply separation of concerns: move the attributes to business objects or other objects
    2. The expert design pattern is useful when [ _________ ]. (Select the best answer from the choices provided.)
        (a) a specific niche is necessary within a complex system
        (b) you need to make systems high-cohesion everywhere
        (c) other classes are fulfilling a niche
        (d) you have multiple controllers

    3. According to the GRASP Creator pattern, which class should NOT have the responsibility of creating objects of a class C?
        (a) A class completely unrelated to objects of a class C.
        (b) A class that consists of objects of a class C.
        (c) A class that contains objects of a class C.
        (d) A class that updates objects of a class C.

Reply to post from Barrett RayReply

    Mark as ReadMark as Read

Mark post as read
Daisy Borja
Sep 24 4:55pm
Reply from Daisy Borja

Group A

 

1. How does the creator pattern support low coupling?

A. Coupling between the classes already exists

B. Creator creates new classes to support low coupling

C. It adds more dependencies

D. Any class can be chosen to be the creator

 

2. The Expert pattern is best applied when writing use case scenarios because the designer can assign responsibilities directly to the ___.

A. Information expert

B. Business controller

C. System interface

D. Domain boundary

 

3. Which type of system is best described as a transformational system in activity modeling?

A. One that primarily reacts to external stimuli in real-time

B. One that transforms inputs into outputs through a network of information-processing activities

C. One that focuses only on inter-object message passing

D. One that requires continuous user interaction throughout the process

Reply to post from Daisy BorjaReply

    Mark as ReadMark as Read

Mark post as read
CW
Cade Ward
Sep 25 8:18pm
Reply from Cade Ward

Group D

Given multiple use cases for a problem in an application, which of the following would benefit from a controller pattern?

A. A web application with multiple functionalities to handle and process.
B. A database with several accessors to an instance that all others need.
C. A System-on-a-Chip pipeline to upload and compile code.
D. An interface that allows dynamic production of different methods to achieve a result.

Which pattern assigns a responsibility to the object that has the information necessary to fulfill that responsibility?

A) Expert Pattern
B) Controller Pattern
C) Creator Pattern
D) Strategy Pattern

What is the main idea of the Creator pattern?

A. Give the responsibility for creating an object to a class that closely uses or contains it.
B. Always let the controller class create every object in the system.
C. Require a separate factory class for every single object you make.
D. Create all objects inside the database manager.

Reply to post from Cade WardReply

    Mark as ReadMark as Read

Mark post as read
JS
John Schruben
Sep 26 8:46am | Last edited Sep 26 8:47am
Reply from John Schruben

GROUP G

1) Which of these is a benefit of the creator pattern?

          A) It creates high coupling.
          B) It promotes reusability.
          C) The creator introduces new dependencies.
          D) It removes the need to create objects.

2) Which of these is not a benefit of the controller pattern?

          A) It decouples the presentation and business objects
          B) It makes things easier to change
          C) It allows you to write different front ends while using the same logic classes
          D) Hight cohesion because responsibilities are assigned to objects that can fulfill the responsibilities.

Reply to post from John SchrubenReply

    Mark as ReadMark as Read

Mark post as read
EP
Evan Perkins
Sep 29 9:29am
Reply from Evan Perkins

Group C:

1. Which statement best describes/explains the goal of the Expert pattern
A. To assign responsibilities to the class that has the necessary information to fulfill them.

B. To always assign responsibilities to the controller regardless of knowledge.

C. To distribute responsibilities randomly among classes to reduce workload.

D. To ensure that only the user interface handles all incoming requests.

 

2. Why does the Creator pattern support low coupling between classes?

A. Because it assigns creation responsibility to a class that already has a natural relationship with the object.

B. Because it forces unrelated classes to build objects they don't use.
C.  Because it requires introducing extra factory classes in all cases.

D. Because it prevents domain classes from collaborating with each other.

 

3. What is the primary benefit of introducing a controller in a system design?

A. It decouples the user interface from business logic by centralizing system event handling.

B. It guarantees that the controller never grows too complex.

C. It allows developers to eliminate the need for expert objects.

D. It automatically generates state diagrams for each and every use case.

Reply to post from Evan PerkinsReply

    Mark as ReadMark as Read

Mark post as read
IM
Ian Morris
Oct 6 9:27am
Reply from Ian Morris

Group I

When implementing the Expert design pattern, which class should be assigned a particular responsibility?
A. The class that has the necessary information to fulfill the responsibility.
B. The class that has the fewest existing responsibilities.
C. The class that has the most related responsibilities.
D. The class that will make the code easiest to test.

Which statement best describes the role of a controller object?
A. It is responsible for handling system events and coordinating the actions between the UI and domain objects.
B. It is responsible for directly performing all business logic within the user interface layer.
C. It replaces the user interface and domain layers entirely.
D. It handles ALL logic.

Which of the following best describes the Creator pattern?
A. Assign the responsibility for creating an instance of a class to the class that has the information needed to create it.
B. Always delegate object creation to a factory class, regardless of context.
C. Assign object creation to the class that needs more responsibility.
D. Let all objects be created by a global function to ensure consistency.

Reply to post from Ian MorrisReply

    Mark as ReadMark as Read

Mark post as read
GS
Garrett Snow (He/Him/His)
Oct 11 6:16am
Reply from Garrett Snow

Group B

What isn’t a benefit of the expert pattern?
A) Classes can be re used for other things
B) Easy to understand and maintain
C) High cohesion 
D) Low coupling of objects

 

What does the expert pattern do?
A) Passes off tasks to the appropriate classes whenever needed
B) Plays a key role in object oriented program design
C) Combines all tasks and processing to a single controller
D) Creates shared objects


Which of the following is *not true* of the OSM Model?
A) It is a member of the GRASP family of models
B) The OSM model requires the team to understand the state behaviors
C) The OSM model can facilitate easier communication among the team
D) An OSM model should have every state be reachable

 