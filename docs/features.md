# Task Manager: Feature List (v1)

## Backend Features (build first)
| ID  | Feature                  | Description                                  |
|-----|--------------------------|----------------------------------------------|
| B1  | Create task              | Save a new task with name, description, status |
| B2  | List tasks               | Return all tasks                             |
| B3  | Get task by id           | Return one task, or a clear "not found" error |
| B4  | Update task              | Change name, description or status           |
| B5  | Delete task              | Remove a task by id                          |
| B6  | Input validation         | Enforce the field rules before saving        |
| B7  | Error handling           | Consistent, safe error responses             |
| B8  | Automated tests          | Service layer tests, then API tests          |

## Frontend Features (Flutter, built after backend works)
| ID  | Feature                  | Description                                  |
|-----|--------------------------|----------------------------------------------|
| F1  | Task list screen         | Show all tasks with their status             |
| F2  | Add task screen          | Form to create a task                        |
| F3  | Edit task screen         | Form to change a task                        |
| F4  | Delete task              | Delete with a confirmation dialog            |

## Planned for Later (not in v1)
- v1.1: filter by status, pagination
- v2: user accounts, login, JWT

## Build Order
1. Database design
2. Backend B1 to B5, one feature at a time
3. B6 to B8 added alongside each feature
4. Flutter F1 to F4
5. Git workflow, deployment, basic CI/CD
