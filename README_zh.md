
# Rust Axum + PostgreSQL CRUD 应用

这是一个基于 [Rust](https://www.rust-lang.org/)、[Axum](https://github.com/tokio-rs/axum) 和 [PostgreSQL](https://www.postgresql.org/) 构建的简单且稳定的 CRUD 接口应用，使用 [sqlx](https://github.com/launchbadge/sqlx) 实现异步数据库访问。

## 功能特点

- **现代 Rust Web 技术栈：** 使用 Axum 构建高性能异步 API。
- **持久化存储：** 基于 PostgreSQL，数据库结构通过 SQL 管理。
- **完整的 CRUD 功能：** 提供创建、读取、更新、删除任务的接口。
- **灵活配置：** 使用 `.env` 文件管理环境变量。
- **易于扩展：** 代码结构清晰，注释完整，便于后续开发。

## 目录

- [环境要求](#环境要求)
- [项目设置](#项目设置)
- [数据库配置](#数据库配置)
- [运行应用](#运行应用)
- [API 接口说明](#api-接口说明)
- [参与贡献](#参与贡献)
- [开源许可](#开源许可)

## 环境要求

- 安装 [Rust](https://www.rust-lang.org/tools/install)
- 安装 [PostgreSQL](https://www.postgresql.org/download/)

## 项目设置

1. **克隆项目仓库：**
    ```bash
    git clone https://github.com/Ztefan808/Rust-axum-postgres-CRUD-app.git
    cd Rust-axum-postgres-CRUD-app
    ```

2. **构建项目：**
    ```bash
    cargo build
    ```

## 数据库配置

1. **创建 PostgreSQL 用户和数据库：**
    ```sql
    -- 创建用户
    CREATE ROLE axum_postgres WITH LOGIN PASSWORD 'axum_postgres';

    -- 创建数据库并设置所有者
    CREATE DATABASE axum_postgres WITH OWNER = 'axum_postgres';

    -- 连接数据库并创建任务表
    \c axum_postgres
    CREATE TABLE tasks (
      task_id SERIAL PRIMARY KEY,
      name VARCHAR NOT NULL,
      priority INT
    );
    ```

2. **配置环境变量：**

   在项目根目录下创建 `.env` 文件，内容如下：
    ```env
    DATABASE_URL=postgres://axum_postgres:axum_postgres@127.0.0.1:5432/axum_postgres
    SERVER_ADDRESS=127.0.0.1:7878
    ```

## 运行应用

使用以下命令启动 API 服务器：
```bash
cargo run
```
服务器将运行在 `http://127.0.0.1:7878`。

## API 接口说明

- **获取所有任务**
    ```
    GET /tasks
    ```
    返回所有任务的列表。

- **创建新任务**
    ```
    POST /tasks
    Content-Type: application/json

    {
      "name": "任务名称",
      "priority": 1
    }
    ```

- **更新指定任务**
    ```
    PATCH /tasks/{task_id}
    Content-Type: application/json

    {
      "name": "新的任务名称",
      "priority": 2
    }
    ```

- **删除任务**
    ```
    DELETE /tasks/{task_id}
    ```

## 参与贡献

欢迎贡献代码！您可以通过提 issue 或提交 pull request 参与开发。

## 开源许可

本项目使用 [CC0 许可证](LICENSE) 进行开源发布。
