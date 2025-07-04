# TODO API in Go with PostgreSQL

A simple TODO REST API written in Go using the Gorilla Mux router and PostgreSQL to store data.  
It supports basic CRUD operations and soft delete functionality for TODO items.

---

## API Endpoints

| Method | Endpoint        | Description         |
|--------|------------------|---------------------|
| GET    | /todos           | List all todos      |
| POST   | /todos           | Create a new todo   |
| GET    | /todos/{id}      | Get todo by ID      |
| PUT    | /todos/{id}      | Update a todo       |
| DELETE | /todos/{id}      | Soft delete a todo  |

---

## Database Setup

Start PostgreSQL and create the database and table:

```sql
CREATE DATABASE tododb;
\c tododb

CREATE TABLE todos (
  id SERIAL PRIMARY KEY,
  title TEXT NOT NULL,
  completed BOOLEAN DEFAULT false,
  deleted BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
````

---

## How to Run

1. Clone the project:

```bash
git clone https://github.com/sanyam-harness/todo-api-go-with-postgre.git
cd todo-api-go-with-postgre
```

2. Update the PostgreSQL password in `db.go`:

```go
dsn := "postgres://postgres:<your_password>@localhost:5432/tododb"
```

3. Install dependencies:

```bash
go mod tidy
```

4. Run the app:

```bash
go run main.go handler.go service.go db.go todo.go
```

---

## How to Test Using curl

> Open a second terminal window while the app is running on [http://localhost:8080](http://localhost:8080)

### Create a todo

```bash
curl -X POST http://localhost:8080/todos \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn Go"}'
```

### List all todos

```bash
curl http://localhost:8080/todos
```

### Get todo by ID

```bash
curl http://localhost:8080/todos/1
```

### Update a todo

```bash
curl -X PUT http://localhost:8080/todos/1 \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn Go in depth", "completed": true}'
```

### Soft delete a todo

```bash
curl -X DELETE http://localhost:8080/todos/1
```

### Confirm it was deleted (should no longer appear)

```bash
curl http://localhost:8080/todos
```

---

## Project Files

* `main.go` - Starts the server
* `db.go` - Connects to the PostgreSQL database
* `handler.go` - Defines HTTP handlers for each route
* `service.go` - Contains the business logic
* `todo.go` - Data model for a todo item

```

---

