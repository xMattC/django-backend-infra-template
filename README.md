# Backend App API

A **Dockerised Django backend starter project** with PostgreSQL,
testing, linting, and CI already configured.

This repository provides a clean foundation for building backend APIs
without repeating the initial infrastructure setup. The goal is to
handle common setup tasks so development can focus on **models, business
logic, and API endpoints**.

------------------------------------------------------------------------

## Features

-   Django backend framework
-   PostgreSQL database
-   Dockerised development environment
-   Docker Compose service orchestration
-   Flake8 linting
-   GitHub Actions CI
-   Custom Django management command for database readiness
    (`wait_for_db`)
-   Clean project structure ready for API development

------------------------------------------------------------------------

## Tech Stack

  |Component               |Technology
  |----------------------- |----------------
  |Backend                 |Django
  |Database                |PostgreSQL
  |Containerisation        |Docker
  |Service orchestration   |Docker Compose
  |Linting                 |Flake8
  |CI/CD                   |GitHub Actions

------------------------------------------------------------------------

## Project Structure

    app/
     ├── core/
     │   ├── management/
     │   │   └── commands/
     │   │       └── wait_for_db.py
     │   ├── models.py
     │   ├── admin.py
     │   └── tests/
     │
     ├── app/
     │   ├── settings.py
     │   ├── urls.py
     │   └── wsgi.py
     │
     └── manage.py

    docker-compose.yml
    Dockerfile
    requirements.txt
    requirements.dev.txt

------------------------------------------------------------------------

## Requirements

The project runs fully inside Docker.

You only need:

-   Docker
-   Docker Compose

No local Python installation is required.

------------------------------------------------------------------------

## Running the Application

Start the development environment:

``` bash
docker-compose up
```

This will:

1.  Start the PostgreSQL container
2.  Build and start the Django container
3.  Wait for the database to become available
4.  Run migrations
5.  Start the development server

Open the application in your browser:

http://localhost:8000

------------------------------------------------------------------------

## Rebuilding Containers

If dependencies change or the Dockerfile is updated, rebuild the image:

``` bash
docker-compose up --build
```

------------------------------------------------------------------------

## Running Tests

Execute the Django test suite:

``` bash
docker-compose run --rm app sh -c "python manage.py test"
```

------------------------------------------------------------------------

## Running Linting

Run flake8 to check code style:

``` bash
docker-compose run --rm app sh -c "flake8"
```

Linting configuration is located in:

    app/.flake8

------------------------------------------------------------------------

## Database Setup

The project uses **PostgreSQL running in Docker**.

A custom Django management command ensures the application waits until
the database is ready before starting.

Example:

``` bash
python manage.py wait_for_db
```

This command retries the database connection until it succeeds.

------------------------------------------------------------------------

## Useful Development Commands

Run Django management commands inside Docker:

``` bash
docker-compose run --rm app sh -c "python manage.py <command>"
```

Example:

``` bash
docker-compose run --rm app sh -c "python manage.py migrate"
```

------------------------------------------------------------------------

## Continuous Integration

GitHub Actions runs automatically on push and pull requests.

The pipeline performs:

-   flake8 linting
-   Django test execution

This helps maintain code quality and prevents broken changes.

------------------------------------------------------------------------

## Custom Management Commands

Django automatically exposes custom CLI commands placed in:

    <app_name>/management/commands/

Each file becomes available through:

``` bash
python manage.py <command_name>
```

Example included in this project:

    wait_for_db

Used to ensure database readiness when starting Docker containers.

------------------------------------------------------------------------

## Future Development

This project is intended as a **backend project starter template**.

Typical next steps include:

-   adding application models
-   creating REST API endpoints
-   integrating Django REST Framework
-   implementing authentication
-   adding business logic and services

------------------------------------------------------------------------

## Author

Created by **Matt C**

GitHub: https://github.com/xMattC
