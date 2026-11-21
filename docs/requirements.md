# Task Manager: Requirements (v1)

## Purpose
A simple application to create, view, update and delete tasks.

## Functional Requirements
1. Create a task with a name, description and status.
2. List all tasks.
3. Update a task's name, description or status.
4. Delete a task.

## Task Fields
| Field       | Required | Rules                                   |
|-------------|----------|-----------------------------------------|
| name        | Yes      | 3 to 100 characters, not blank          |
| description | No       | Maximum 500 characters                  |
| status      | Yes      | One of: TODO, IN_PROGRESS, DONE         |

## Non-Functional Requirements
- Backend uses layered architecture: Controller -> Service -> Repository -> PostgreSQL.
- All input is validated before it reaches the database.
- Errors return clear, safe messages (no stack traces to the client).
- Core business logic has automated tests.

## Out of Scope for v1
- User accounts, login and JWT (planned for v2)
- Due dates, priorities, tags
- Multi-user sharing
