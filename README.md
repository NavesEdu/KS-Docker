# To-Do API with Java, Spring Boot, and Docker

This is a simple demonstration project of a RESTful To-Do List API built with Java and Spring Boot. The entire environment, including the application and its PostgreSQL database, is containerized and managed using Docker Compose.

This project serves as a practical example of how to "dockerize" a Java application and manage a multi-container setup for local development.

## Tech Stack

* **Backend:** Java 17, Spring Boot 3, Spring Web, Spring Data JPA
* **Database:** PostgreSQL
* **Build Tool:** Maven
* **Containerization:** Docker & Docker Compose
* **Utilities:** Lombok

## Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

You need to have the following software installed on your machine:
* [Maven](https://maven.apache.org/download.cgi)
* [Docker](https://www.docker.com/get-started/) and Docker Compose
    * On Windows, it is recommended to use Docker through **WSL 2 (Windows Subsystem for Linux)**.

### Running the Application

1.  **Clone the repository and enter the directory:**

    ```bash
    git clone https://github.com/NavesEdu/KS-Docker.git
    cd KS-Docker
    ```

2.  **Compile and package the application:**

    This command builds the application's JAR file. It skips the tests, as they would require a separate test-specific database configuration.

    ```bash
    mvn clean package -DskipTests
    ```

3.  **Run the environment with Docker Compose:**

    This command will build the API's Docker image and start both the API and the PostgreSQL database containers in detached mode.
    *Note: If you are inside a WSL environment, you may need to start the Docker service first with `sudo service docker start`.*

    ```bash
    docker compose up --build -d
    ```

4.  **Verify that the containers are running:**

    You should see both `todo_api` and `postgres_db` containers with the status `Up`.

    ```bash
    docker ps
    ```
    The API will be available at `http://localhost:8080`.

## API Endpoints

You can use `curl` or any API client like Postman or Insomnia to interact with the API.

### Create a Task

* **Method:** `POST`
* **URL:** `/tasks`
* **Body (JSON):**

    ```json
    {
      "description": "My new task description",
      "done": false
    }
    ```

* **Example `curl` command:**
    ```bash
    curl -X POST http://localhost:8080/tasks \
    -H "Content-Type: application/json" \
    -d '{"description": "Learn how to use Docker", "done": false}'
    ```

### List All Tasks

* **Method:** `GET`
* **URL:** `/tasks`
* **Example `curl` command:**
    ```bash
    curl http://localhost:8080/tasks
    ```

* **Example Response:**
    ```json
    [
      {
        "id": 1,
        "description": "Learn how to use Docker",
        "done": false
      }
    ]
    ```

## Shutting Down

To stop and remove all the containers, network, and volumes created by Compose, run:
```bash
docker compose down