# Project Overview

This project is a web application built using React for the frontend and Spring Boot for the backend. It uses Maven for dependency management, and Yarn/NPM for managing JavaScript dependencies. The application demonstrates how data is fetched from a database, processed by services, and presented on a webpage.

## Table of Contents

1. [Project Setup](#project-setup)
2. [Data Flow](#data-flow)
3. [Services](#services)
4. [Web Production](#web-production)
5. [ORM Principles](#orm-principles)

## Project Setup

### Prerequisites

- Java 11 or higher
- Maven
- Node.js and npm or Yarn
- IDE (IntelliJ IDEA recommended)

### Backend Setup

1. Clone the repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Navigate to the backend directory:
    ```sh
    cd backend
    ```

3. Build the project using Maven:
    ```sh
    mvn clean install
    ```

4. Run the Spring Boot application:
    ```sh
    mvn spring-boot:run
    ```

### Frontend Setup

1. Navigate to the frontend directory:
    ```sh
    cd frontend
    ```

2. Install dependencies using Yarn or npm:
    ```sh
    yarn install
    # or
    npm install
    ```

3. Start the development server:
    ```sh
    yarn start
    # or
    npm start
    ```

## Data Flow

1. **Database**: The application uses a relational database to store data. The database schema is defined using JPA (Java Persistence API) entities.

2. **Repository Layer**: JPA repositories are used to interact with the database. These repositories provide CRUD operations and custom queries.

3. **Service Layer**: Services contain business logic and interact with repositories to fetch and process data.

4. **Controller Layer**: REST controllers expose endpoints for the frontend to consume. They use services to get data and return it as JSON.

5. **Frontend**: React components fetch data from the backend using HTTP requests (e.g., Axios or Fetch API) and render it on the webpage.

## Services

Services in the Spring Boot application are responsible for handling business logic. They interact with repositories to fetch data and perform operations. Below is an example of a service class:

```java
@Service
public class ExampleService {

    @Autowired
    private ExampleRepository exampleRepository;

    public List<ExampleEntity> getAllExamples() {
        return exampleRepository.findAll();
    }

    public ExampleEntity getExampleById(Long id) {
        return exampleRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Example not found"));
    }

    public ExampleEntity createExample(ExampleEntity example) {
        return exampleRepository.save(example);
    }

    public void deleteExample(Long id) {
        exampleRepository.deleteById(id);
    }
}
