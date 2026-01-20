# Weekly question

> What is the purpose of constructing a domain model?
> a) To depict the relationships between the event-driven subsystem and its context
> b) To implement the full functionality of the event-driven subsystem 
> c) To optimize the performance of the event-driven subsystem  
> d) To replace the design model with the implementation model

From section 13.4.2

---

# Monday
## Discussion Topic: GRASP → State Change Bridge

OURS:
- Actor is pedestrians and cars
- Performance layer is the lights and sensors
- Controller will communicate the lights and sensors with the business logic
- Business logic is timer/any other logic

## States vs. Events
**Object state modeling (OSM)** is concerned with the identification, modeling, design, and specification of state-dependent, reactive behavior of systems and objects

>While the design of interactive systems is centered around use cases, the design of event-driven systems is focused on state- dependent reactions of objects to events of interest



# Wednesday
No class



# Friday
Talked about OSM, why and what

![[Pasted image 20250926092609.png]]

### 1. Project Intake
-  A new client project is received by the business-development team.
-  The project is entered into the system through an intake form.
-  The system creates a project record with deadlines, departments involved, and client requirements.
-   A project may need internal review and approval before any tasks are sent out.


| Classes with attributes shown in parentheses                                                                                                                      | State                                                                    |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Client_Project(client_requirements : requirement\[]), form(project : project), project_record(deadline : int) requirement(department : department\[]), department | busines_development_team(working/idle), internal_review(approval,denial) |
| Aggregation relationships: Project_record(dealdepartment, requirements)                                                                                           | Guard conditions: Pending review is approved. Pending review is denied   |

| Thing of interest                                                                     | Generalized case                                                  | Classification |
| ------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | -------------- |
| Overall project pipeline with color-coded progress, key blockers, and summary metrics | A specific perspective or view of information                     | State          |
| Task-level progress, departmental workload, overdue work, and staff performance       | A specific perspective or view of information                     | State          |
| Own assignments, upcoming due dates, and any issues needing attention                 | A specific perspective or view of information                     | State          |
| Executives view the dashboard                                                         | An actor interacting with the system                              | Event          |
| Managers view the dashboard                                                           | An actor interacting with the system                              | Event          |
| Staff view the dashboard                                                              | An actor interacting with the system                              | Event          |
| Underlying project, task, and performance data changes                                | Status of something                                               | State          |
| System filters data based on user role                                                | A rule or process that determines what information is shown       | Guard          |
| System presents the appropriate dashboard view                                        | An action to be performed as a system/object response to an event | Action         |
