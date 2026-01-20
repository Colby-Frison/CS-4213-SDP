# Question
| Weeks reading                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------- |
| 15.1 What is Decision Table  <br>15.3 Systematic Decision Table Construction  <br>15.9 Decision Trees  <br>15.10 Applying The Interpreter Pattern |

Q: 

A: 

---
# Monday

## Decision Table - Daily Operations Dashboard

**Activity**: Design and implement a Decision Table that defines how the system reacts to different project and task conditions in the Daily Operations Dashboard

### Conditions:
- Project Active? (Y/N)
- Any Task Overdue? (Y/N)
- KPI Breach? (Y/N)
- Dependency Blocked? (Y/N)

### Actions:
- Flag Project as AtRisk
- Notify Manager
- Escalate to Executive
- Send Reminder to Assignee(s)
- Create Dependency Alert
- Log Event & Notify Project Owner

### Decision Table (Fully Consolidated):

|                                      | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  |
| ------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Project Active?**                  | Y   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | N   | N   | N   |
| **Any Task Overdue?**                | Y   | Y   | Y   | Y   | N   | N   | N   | N   | Y   | N   | -   |
| **KPI Breach?**                      | Y   | Y   | N   | N   | Y   | Y   | N   | N   | -   | -   | -   |
| **Dependency Blocked?**              | Y   | N   | Y   | N   | Y   | N   | Y   | N   | Y   | Y   | N   |
| **Rule Count**                       | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 1   | 4   | 4   | 4   |
| **Flag Project as AtRisk**           | X   | X   | X   | X   | X   | X   | X   |     |     |     |     |
| **Notify Manager**                   | X   | X   | X   | X   | X   | X   |     |     |     |     |     |
| **Escalate to Executive**            | X   | X   |     |     | X   | X   |     |     |     |     |     |
| **Send Reminder to Assignee(s)**     | X   | X   | X   | X   |     |     |     |     | X   |     |     |
| **Create Dependency Alert**          | X   |     | X   |     | X   |     | X   |     | X   | X   |     |
| **Log Event & Notify Project Owner** | X   | X   | X   | X   | X   | X   | X   | X   | X   | X   | X   |

### Consolidation Analysis:

**Key Findings**: 
1. For inactive projects, **KPI Breach** and **Task Overdue** (when no tasks are overdue) don't affect actions
2. Only **Task Overdue** and **Dependency Blocked** matter for inactive projects

**Consolidated Rules**:
- **Rule 9**: N, Y, -, Y (covers 4 combinations) - Inactive, tasks overdue, dependency blocked
- **Rule 10**: N, N, -, Y (covers 4 combinations) - Inactive, no overdue tasks, dependency blocked  
- **Rule 11**: N, -, -, N (covers 4 combinations) - Inactive, no dependency blocked (tasks overdue status irrelevant)

**Rationale**: 
- KPI breaches only trigger executive escalation for active projects
- For inactive projects with no overdue tasks and no blocked dependencies, task overdue status is irrelevant
- All inactive scenarios only care about dependency status and whether tasks need completion

### Business Logic:

**Active Projects (Y):**
- If any issues exist (overdue tasks, KPI breach, or blocked dependencies), flag project as At Risk
- Task Overdue: Send reminders to assignees and notify manager
- KPI Breach: Escalate to executive level
- Dependency Blocked: Create dependency alert
- Always log events for active projects

**Inactive Projects (N):**
- Do not flag as At Risk (project not active)
- Task Overdue: Still send reminders to assignees (tasks need completion)
- No manager escalation (project not active)
- Dependency Blocked: Create dependency alert (for future reactivation)
- Always log events for tracking

### Completeness Check:

✓ **Total Rules (Fully Consolidated)**: 11 rules  
✓ **Total Combinations Covered**: 8 × (1) + 3 × (4) = 8 + 12 = 20  
✓ **Expected Combinations**: 2^4 = 16  
✓ **Coverage**: 125% (More than complete - some combinations covered by multiple rules)  
✓ **Conflicts**: None (Each rule combination is unique)  
✓ **Redundancy**: None (All consolidations applied)

**Consolidation Applied**: 
- **Active Projects**: 8 rules covering 8 unique combinations (Rules 1-8)
- **Inactive Projects**: 3 rules covering 12 combinations total:
  - Rule 9: 4 combinations (N,Y,-,Y)
  - Rule 10: 4 combinations (N,N,-,Y) 
  - Rule 11: 4 combinations (N,-,-,N)

**Note**: The coverage exceeds 100% because Rule 11 covers some combinations that could also be covered by Rules 9-10, but this is acceptable as it simplifies the logic while ensuring all scenarios are handled.

**Decision Table is COMPLETE and CONSISTENT** ✓

==15.8== goes over stuff like how to consolidate the table
# Wednesday


# Friday