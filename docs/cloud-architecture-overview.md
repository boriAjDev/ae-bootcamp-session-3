# Cloud Architecture Overview

## System Context

```mermaid
flowchart LR
    user[TODO App User]

    subgraph system[TODO App Monorepo]
        frontend[React Frontend<br/>Browser UI]
        api[Express API<br/>Node.js, port 3030]
        store[(In-Memory SQLite Store)]
    end

    user -->|Manages tasks| frontend
    frontend -->|HTTP /api/tasks| api
    api -->|Reads and writes tasks| store
```

## Create a TODO Sequence

```mermaid
sequenceDiagram
    actor User as TODO App User
    participant Frontend as React Frontend
    participant API as Express API
    participant Store as In-Memory SQLite

    User->>Frontend: Submit task form
    Frontend->>Frontend: Validate required title
    Frontend->>API: POST /api/tasks with task data
    API->>API: Validate request
    API->>Store: Insert task
    Store-->>API: Return new task ID
    API->>Store: Read created task
    Store-->>API: Return created task
    API-->>Frontend: 201 Created with task
    Frontend->>API: GET /api/tasks
    API->>Store: Read task list
    Store-->>API: Return tasks
    API-->>Frontend: 200 OK with tasks
    Frontend-->>User: Display updated task list
```

## Component Responsibilities

- **React frontend:** Presents the task interface and sends task operations to the API. During local development, the React development server proxies `/api` requests to `http://localhost:3030`.
- **Express API:** Provides task create, read, update, completion, and delete endpoints under `/api/tasks`.
- **In-memory store:** Uses an in-memory SQLite database owned by the Express process. Data is process-local and is lost when the API restarts.

The frontend and backend are separate npm workspaces under `packages/frontend` and `packages/backend`. The root workspace starts both applications together with `npm run start`.
