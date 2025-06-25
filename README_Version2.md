# Rust Axum + PostgreSQL CRUD App

A simple and robust CRUD API application built with [Rust](https://www.rust-lang.org/), [Axum](https://github.com/tokio-rs/axum), and [PostgreSQL](https://www.postgresql.org/), using [sqlx](https://github.com/launchbadge/sqlx) for async database access.

## Features

- **Modern Rust web stack:** Built with Axum for fast, async APIs.
- **Persistent storage:** PostgreSQL database, schema managed via SQL.
- **Full CRUD:** Create, Read, Update, Delete endpoints for tasks.
- **Configurable:** Uses `.env` for environment variables.
- **Easy to extend:** Well-structured and commented codebase.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Database Configuration](#database-configuration)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

- [Rust](https://www.rust-lang.org/tools/install)
- [PostgreSQL](https://www.postgresql.org/download/)

## Setup

1. **Clone the repository:**
    ```bash
    git clone https://github.com/Ztefan808/Rust-axum-postgres-CRUD-app.git
    cd Rust-axum-postgres-CRUD-app
    ```

2. **Build the project:**
    ```bash
    cargo build
    ```

## Database Configuration

1. **Create a PostgreSQL user and database:**
    ```sql
    -- Create user
    CREATE ROLE axum_postgres WITH LOGIN PASSWORD 'axum_postgres';

    -- Create database
    CREATE DATABASE axum_postgres WITH OWNER = 'axum_postgres';

    -- Connect to database and create tasks table
    \c axum_postgres
    CREATE TABLE tasks (
      task_id SERIAL PRIMARY KEY,
      name VARCHAR NOT NULL,
      priority INT
    );
    ```

2. **Set up environment variables:**

    Create a `.env` file in the project root with:
    ```env
    DATABASE_URL=postgres://axum_postgres:axum_postgres@127.0.0.1:5432/axum_postgres
    SERVER_ADDRESS=127.0.0.1:7878
    ```

## Running the Application

Start the API server with:
```bash
cargo run
```
The server will be available at `http://127.0.0.1:7878`.

## API Endpoints

- **Get all tasks**
    ```
    GET /tasks
    ```
    Returns a list of all tasks.

- **Create a new task**
    ```
    POST /tasks
    Content-Type: application/json

    {
      "name": "Task Name",
      "priority": 1
    }
    ```

- **Update an existing task**
    ```
    PATCH /tasks/{task_id}
    Content-Type: application/json

    {
      "name": "New Task Name",
      "priority": 2
    }
    ```

- **Delete a task**
    ```
    DELETE /tasks/{task_id}
    ```

## Contributing

Contributions are welcome! Please open issues or submit pull requests.

## License

This project is licensed under the [CC0 License](LICENSE).