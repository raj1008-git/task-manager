# Task Manager: API Design (v1)

Base URL: /api/v1
All requests and responses use JSON.

## Endpoints
| Method | Path        | Purpose           | Success          | Errors        |
|--------|-------------|-------------------|------------------|---------------|
| POST   | /tasks      | Create a task     | 201 Created      | 400           |
| GET    | /tasks      | List all tasks    | 200 OK           | none expected |
| GET    | /tasks/{id} | Get one task      | 200 OK           | 404           |
| PUT    | /tasks/{id} | Update a task     | 200 OK           | 400, 404      |
| DELETE | /tasks/{id} | Delete a task     | 204 No Content   | 404           |

## Create Task: POST /tasks
Request:
    {
      "name": "Write API docs",
      "description": "Document all endpoints",
      "status": "TODO"
    }
- name is required (3 to 100 characters, not blank).
- description is optional (maximum 500 characters).
- status is optional and defaults to TODO.
Response 201 (with a Location header pointing to /api/v1/tasks/{id}):
    {
      "id": 2,
      "name": "Write API docs",
      "description": "Document all endpoints",
      "status": "TODO",
      "createdAt": "2026-11-22T10:15:30+05:30",
      "updatedAt": "2026-11-22T10:15:30+05:30"
    }

## List Tasks: GET /tasks
Response 200: an array of task objects (same shape as above).
An empty list returns [] with status 200, not an error.

## Get Task: GET /tasks/{id}
Response 200: one task object.
Response 404: error object (see below).

## Update Task: PUT /tasks/{id}
Request (name and status are required, because PUT replaces the task):
    {
      "name": "Write API docs",
      "description": "Document all endpoints and errors",
      "status": "IN_PROGRESS"
    }
Response 200: the updated task object.
Response 400: validation error. Response 404: not found.

## Delete Task: DELETE /tasks/{id}
Response 204: empty body.
Response 404: error object.

## Error Format (every error uses this shape)
    {
      "timestamp": "2026-11-22T10:20:00+05:30",
      "status": 400,
      "error": "Validation failed",
      "message": "One or more fields are invalid",
      "details": ["name: must be between 3 and 100 characters"]
    }

## Status Codes Used
| Code | Meaning                              |
|------|--------------------------------------|
| 200  | Request succeeded                    |
| 201  | Resource created                     |
| 204  | Succeeded, nothing to return         |
| 400  | Client sent invalid data             |
| 404  | Task with that id does not exist     |
| 500  | Unexpected server error (generic     |
|      | message only, no internal details)   |

## Design Decisions
- /v1 is in the path, so a future breaking change becomes /v2 without
  breaking existing Flutter app versions.
- Plural noun (/tasks), with the HTTP method describing the action.
- Responses never expose database internals or stack traces.
- Clients can never send id, createdAt or updatedAt. The server controls them.
