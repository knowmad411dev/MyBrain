---
tags:
- docker
video-url: https://www.youtube.com/watch?v=HGKfE-cn9y4&list=WL&index=13
---

## **Master Docker Compose

### Docker Compose Tutorial Overview

This is a detailed walkthrough of a YouTube tutorial on how to use Docker Compose to set up a Ruby on Rails web application along with a PostgreSQL database, allowing for seamless interaction between these services. Let's break it down into several core sections, including a step-by-step explanation of the key concepts, Docker Compose setup, how services interact, and code examples to get started with Docker Compose in a practical Rails application.

### Overview of Docker Compose

Docker Compose is an amazing tool that allows you to run multiple containers as part of a single application. By defining all services and configurations in a single file (`docker-compose.yml`), you can quickly set up and run an entire stack, such as a web server and a database, with just one command. This tutorial illustrates setting up a Rails web server (Puma) and PostgreSQL database using Docker Compose, showcasing how these services interact.

### Goals of This Tutorial

1. Understand how to use Docker Compose to spin up multiple services.
2. Create a Docker Compose file for a simple Ruby on Rails application.
3. Set up Rails to use a PostgreSQL database, ensuring they can communicate effectively.
4. Store data outside of the containers to ensure persistence.
5. Explore Docker Compose commands and how to use them in practice.

### Steps to Follow

#### 1. Create a New Rails Application

First, you need to create a new Rails application. The command to create this project, specifying PostgreSQL as the database, is:

```bash
rails new docker_compose_app --database=postgresql
```

This command generates a new Rails project named `docker_compose_app` and uses PostgreSQL for the database.

#### 2. Writing the Docker Compose File

The Docker Compose configuration file, typically named `docker-compose.yml` or `compose.yml`, allows you to define your services in YAML. In this example, the goal is to have both a web server (Rails, using Puma) and a database server (PostgreSQL) communicate smoothly.

**Create the `docker-compose.yml` file in the base directory of your Rails application**. Here's a simplified version of the complete `docker-compose.yml` file used in the tutorial:

```yaml
version: '3.9'  # Specify the version of Docker Compose

services:
  db:
    image: postgres:16  # Use PostgreSQL image version 16
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - pgdata:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER}"]
      interval: 10s
      timeout: 5s
      retries: 5

  web:
    build: .
    command: bundle exec rails s -b '0.0.0.0'
    volumes:
      - .:/rails
    ports:
      - "3000:3000"
    depends_on:
      db:
        condition: service_healthy
    environment:
      DATABASE_HOST: db
      DATABASE_USERNAME: ${POSTGRES_USER}
      DATABASE_PASSWORD: ${POSTGRES_PASSWORD}

volumes:
  pgdata:  # Persist the PostgreSQL data
```

#### 3. Breaking Down the `docker-compose.yml` File

##### **Services Definition**

The `docker-compose.yml` file begins with defining multiple services under the `services:` section:

- **db**: This is the PostgreSQL service.
  - `image: postgres:16` indicates that this service uses the PostgreSQL 16 image.
  - `environment:` defines environment variables for this container. `POSTGRES_USER` and `POSTGRES_PASSWORD` are set using values from the `.env` file (for security).
  - `volumes:` ensure data persistence even if the container stops, mapping to a local volume `pgdata`.
  - `healthcheck:` runs a command (`pg_isready`) to check if the database is available.
- **web**: This is the Rails application service.
  - `build: .` tells Docker Compose to build the image from the Dockerfile in the current directory.
  - `command:` specifies the command to run Rails.
  - `volumes:` mounts the current directory to `/rails` inside the container, allowing for changes in the code to reflect immediately without rebuilding the image.
  - `ports:` forwards port 3000 of the container to port 3000 of the host machine.
  - `depends_on:` specifies that the `web` service depends on the `db` service and waits for it to be healthy before running.

##### **Environment Variables**

- The `.env` file stores secrets such as the `POSTGRES_USER` and `POSTGRES_PASSWORD`. Docker Compose loads these values at runtime, improving security by keeping them out of your version control system.

##### **Volumes**

- **Data Persistence**: Docker containers are ephemeral by nature, meaning data could be lost if they are restarted. To mitigate this, volumes are defined to persist data even if the container is removed. In this case:
  - **pgdata**: This volume is mapped to PostgreSQL’s data storage directory to ensure the database data is not lost.

#### 4. Running the Setup

After defining your `docker-compose.yml` file, navigate to the directory where it's located and run:

```bash
docker-compose up
```

This command will:

1. Pull the PostgreSQL image if it’s not available locally.
2. Build the web image from the Dockerfile in the current directory.
3. Start both the PostgreSQL and Rails web services.

To run the services in detached mode (in the background), use:

```bash
docker-compose up -d
```

#### 5. Check Health and Logs

- **Health Check**: The PostgreSQL service uses `pg_isready` to confirm that it’s running correctly. This health check is crucial to avoid errors in multi-service environments, ensuring the Rails application does not start before the database is ready.
- **Logs**: You can check the logs for both services by running:
  ```bash
  docker-compose logs
  ```

  To follow the logs for a specific service in real-time:

  ```bash
  docker-compose logs -f db
  ```

#### 6. Interacting with the Services

You can execute commands within a running container to interact with the service. For instance, to enter the web service:

```bash
docker-compose exec web bash
```

This command opens a Bash shell inside the web container, allowing you to execute Rails commands.

#### 7. Setting Up a Rails Application with a Database

Once the services are up and running, navigate to the Rails application on your browser:

- Visit `http://localhost:3000` to see the Rails splash screen.
- You can generate models, controllers, and run database migrations using commands like:
  ```bash
  docker-compose exec web bin/rails generate scaffold Post title:string content:text
  docker-compose exec web bin/rails db:migrate
  ```

  These commands generate and migrate a scaffold for a `Post` model with fields `title` and `content`.

#### 8. Testing Communication Between Rails and PostgreSQL

With Docker Compose, services can easily communicate using their service names as hostnames thanks to the internal Docker network and DNS. The Rails app accesses the PostgreSQL database via the hostname `db`, which Docker resolves to the appropriate container’s IP address.

To verify the services are talking to each other:

1. Open a Bash shell in the web service:
   ```bash
   docker-compose exec web bash
   ```
2. Use `curl` to test connectivity:
   ```bash
   curl db:5432
   ```

   This command verifies that the Rails service can access the PostgreSQL service.

#### 9. Application Logic

Finally, let's test the app functionality:

- **Create Blog Posts**: Visit `http://localhost:3000/posts` in your browser. You should be able to create, edit, and delete posts.
- When you create a post, the Rails application communicates with the PostgreSQL database container to store and retrieve the data.

### Summary of How-to Instructions

1. **Create Rails Application**:
   ```bash
   rails new docker_compose_app --database=postgresql
   ```
2. **Write Docker Compose File** (`docker-compose.yml`):
   - Define services (`db` and `web`).
   - Set up environment variables, volumes, and health checks.
   - Use a Dockerfile to build a Rails image for the web service.
3. **Run Docker Compose**:
   ```bash
   docker-compose up
   ```
4. **Check Logs and Health**:
   - Logs: `docker-compose logs`
   - Health Check: `docker-compose ps`
5. **Interact with Services**:
   - Enter container: `docker-compose exec web bash`
6. **Generate Rails Scaffold**:
   ```bash
   docker-compose exec web bin/rails generate scaffold Post title:string content:text
   docker-compose exec web bin/rails db:migrate
   ```
7. **Visit Application**: Navigate to `http://localhost:3000` to interact with the Rails application and verify everything is working correctly.

### Conclusion

This overview provides a comprehensive guide on how to use Docker Compose to set up a Rails application with a PostgreSQL database. Docker Compose simplifies managing multiple services by using an easy-to-understand configuration in YAML format, allowing for reliable and repeatable development environments. The detailed explanations, combined with the practical setup steps and Docker commands, should give you a solid foundation for working with Docker Compose.

[[Docker]]
