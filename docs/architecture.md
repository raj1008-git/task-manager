# Task Manager: Architecture (v1)

## Request Flow
Flutter app
    |  HTTP + JSON
    v
Controller   (receives the request, validates input, returns the response)
    v
Service      (business logic and rules)
    v
Repository   (database access only)
    v
PostgreSQL

## Project Folder Structure
task-manager/
|-- docs/                          requirements, features, ER, architecture
|-- database/
|   `-- schema.sql                 table definitions
|-- backend/                       Spring Boot project (Maven)
|   |-- pom.xml                    dependencies and build config
|   `-- src/
|       |-- main/
|       |   |-- java/com/example/taskmanager/
|       |   |   |-- TaskManagerApplication.java   app entry point
|       |   |   |-- controller/    TaskController.java
|       |   |   |-- service/       TaskService.java
|       |   |   |-- repository/    TaskRepository.java
|       |   |   |-- entity/        Task.java, TaskStatus.java
|       |   |   |-- dto/           CreateTaskRequest.java,
|       |   |   |                  UpdateTaskRequest.java,
|       |   |   |                  TaskResponse.java
|       |   |   `-- exception/     TaskNotFoundException.java,
|       |   |                      ErrorResponse.java,
|       |   |                      GlobalExceptionHandler.java
|       |   `-- resources/
|       |       `-- application.properties        settings (no secrets)
|       `-- test/java/com/example/taskmanager/    automated tests
`-- frontend/                      Flutter app (built after backend)

## Layer Rules
| Layer      | Does                                  | Never does                     |
|------------|---------------------------------------|--------------------------------|
| Controller | HTTP, validation, status codes        | Business logic, database calls |
| Service    | Business rules, coordinates the work  | HTTP details, SQL              |
| Repository | Reads and writes the database         | Business rules                 |
| Entity     | Represents a database row             | Sent directly to the client    |
| DTO        | Shape of request and response JSON    | Contains database logic        |

## Key Decisions
- DTOs are separate from entities, so database changes never leak into the
  API, and clients cannot set fields like id or created_at.
- One GlobalExceptionHandler turns every error into a safe, consistent JSON
  response with no stack traces.
- The database password is never stored in code or Git. It is read from an
  environment variable.
- Adding a future feature (for example, users) means adding new files in each
  layer, not rewriting existing ones.
