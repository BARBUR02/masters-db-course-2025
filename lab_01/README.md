# Database Lab Setup

This project sets up three different database systems (PostgreSQL, Microsoft SQL Server, and SQLite) using Docker containers and provides tasks to initialize them with the Northwind sample database.

## Overview

This setup includes:

- **PostgreSQL**: A powerful open-source relational database
- **Microsoft SQL Server**: Using Azure SQL Edge for ARM64 compatibility (developed on ARM based Mac)
- **SQLite**: A lightweight file-based database

All three databases are pre-configured with Docker Compose and can be initialized with the Northwind sample dataset.

## Requirements

To use this setup, you need:

1. **Docker and Docker Compose**: To run the database containers
2. **Go Task**: To run the task commands (`go install github.com/go-task/task/v3/cmd/task@latest`). Or alternatively just run the commands from the `Taskfile` directly.

## Setup Instructions

1. Clone this repository to your local machine
2. Run the following command to start all databases and initialize them with the Northwind dataset:

```bash
task setup:databases
```

This command will:
- Start all the needed Docker containers
- Create the required database schemas
- Import the Northwind data into each database

## Database Connection Details

### PostgreSQL

- **Host**: localhost
- **Port**: 5432
- **Database**: lab01_db
- **Username**: lab01_user
- **Password**: lab01_password
- **Connection String**: `postgresql://lab01_user:lab01_password@localhost:5432/lab01_db`

### Microsoft SQL Server

- **Host**: localhost
- **Port**: 1433
- **Database**: lab01_db
- **Username**: sa
- **Password**: lab_01_password
- **Connection String**: `sqlserver://sa:lab_01_password@localhost:1433/lab01_db`

### SQLite

- **Database File**: ./sqlite_data/lab01.db
- **No authentication needed**
- **Connection String**: `sqlite:./sqlite_data/lab01.db`

## Available Tasks

- `task setup:databases` - Start and set up all databases
- `task clear:databases` - Clear all databases and shut down containers
- `task setup:postgres` - Set up only PostgreSQL
- `task setup:mssql` - Set up only MSSQL
- `task setup:sqlite` - Set up only SQLite
- `task clear:postgres` - Clear only PostgreSQL
- `task clear:mssql` - Clear only MSSQL
- `task clear:sqlite` - Clear only SQLite

## Files Structure

- `docker-compose.yml` - Docker Compose configuration
- `Taskfile.yml` - Task definitions
- `Northwind_psql/` - PostgreSQL initialization scripts
- `Northwind_mssql/` - MSSQL initialization scripts
- `Northwind_sqlite/` - SQLite initialization scripts

## Troubleshooting

- If you encounter issues with database connectivity, ensure all containers are running with `docker compose ps`
- For issues with script execution, check the container logs with `docker compose logs <container-name>`
- If you receive "orphaned containers" warnings, use the `--remove-orphans` flag (already included in the tasks)
