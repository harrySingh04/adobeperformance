# Roman Numeral Converter
### Overview

The Roman Numeral Converter project is a full-stack application with the following features:

1. A backend REST API built using Spring Boot, which converts integers to Roman numerals.
2. A frontend application built using React and Material UI, providing an interactive interface for users.

The project is production-ready with the following added features:

**Spring Boot Actuator**: Enables health checks, metrics, and monitoring for better observability.

**Centralized Logging** : Allows structured and organized logging to monitor backend activities and errors.

**Dockerized Setup** : Simplifies deployment and orchestration using Docker and Docker Compose.


### Project Structure

```
romanconversion/
├── client/                 # React frontend code
│   ├── Dockerfile          # Dockerfile for frontend
│   ├── src/                # React components and app logic
│   ├── package.json        # Frontend dependencies
│   └── ...                 # Other React files
├── server/                 # Spring Boot backend code
│   ├── Dockerfile          # Dockerfile for backend
│   ├── src/                # Java source code
|   ├── logs/               # Log files written here at runtime
│   ├── pom.xml             # Backend dependencies
│   └── ...                 # Other Spring Boot files
├── docker-compose.yml      # Docker Compose file for managing both services
└── README.md               # Documentation
```

### How to Run the Application

#### 1. Prerequisites
   Ensure the following tools are installed on your system:

```
Docker: Install Docker 
Docker Compose: Install Docker Compose
 ```

#### 2. Build and Run the Application
   To start the backend (Spring Boot) and frontend (React) services together, run the following command from the project root directory (romanconversion/):

```
docker-compose up --build
```
This will:

1. Build the backend and frontend Docker images.
2. Start the **Spring Boot API** on port 8080.
3. Start the **React front end app** on port 3000.
4. Access the Application
   Frontend (React UI): Open your browser and navigate to:
    ```
    http://localhost:3000
    ```
   Backend (Spring Boot API): Test the API endpoint:
    ```
    http://localhost:8080/romannumeral?query=1994
    ```
5. Stop the Application
   To stop the containers, run:
    ```
    docker-compose down
    ```
### Backend (Spring Boot)
#### Key Features

1. REST API for Roman numeral conversion.

2. Validates input to ensure numbers are between 1 and 3999.

3. Dockerized using a multi-stage build for production-ready images.
4. Can be started independently using Maven:

```
cd server
mvn spring-boot: run
```


#### API Endpoint

* URL: /romannumeral
* Method: GET
* Query Parameter: query (integer)
* Example Request:
    ```
    GET http://localhost:8080/romannumeral?query=1994
    ```
* Response:
    ```
   {
  "input":"123",
  "output":"CXXIII"
  }
    ```
  
### Frontend (React)
#### Key Features

1. Responsive React app with an input field for numbers and a button to fetch Roman numeral conversions.

2. Dark mode toggle using Material UI's theming capabilities.

3. Hot reloading for development.

4. Used Material UI instead of Adobe React Spectrum.
5. Run front end separately:

```
cd client
npm start

```

Then, open your browser at http://localhost:3000.
Ensure the backend is running by checking http://localhost:8080/actuator/health.

#### Why Material UI

I chose Material UI for this project primarily because I am already familiar with it, which allowed me to develop the frontend efficiently and focus more on implementing the required functionality.

Material UI is an excellent fit for React-based projects because of its:

1. Ease of Use: Material UI provides a vast library of pre-built components that follow Google's Material Design principles. This makes it easy to implement complex features, such as responsive grids, theming, and dark mode, with minimal effort.

2. Seamless React Integration: Since Material UI is built specifically for React, it allows for easy integration with React hooks, state management, and component-based architecture.

3. Customization Options: Material UI offers extensive customization capabilities to match the design requirements of any project while still maintaining consistency across components.

4. Documentation and Community Support: Material UI has clear documentation and a large community, which makes it easier to troubleshoot issues and find best practices.

#### Front End Testing

We have implemented unit and integration tests for the React frontend using:

* Jest: For running JavaScript tests.
* React Testing Library: For testing React components in a user-friendly way.

#### Covered Test Cases:

* Rendering the input field.
* Handling user interactions (e.g., typing, button clicks).
* API calls and validating responses.
* Dark mode toggle functionality.
* Accessibility checks for UI components.

#### Run Tests

Run the following command from the client module:

`npm test -- --watchAll=false`

### Features Added

#### Spring Boot Actuator

The backend uses Spring Boot Actuator to expose health checks, metrics, and more. 
These endpoints provide critical insights into the application's status and performance.

* Health Checks: Monitor the application's overall health and specific components such as disk space, database connectivity, and custom health checks.

* Metrics: Access detailed metrics about JVM performance, memory usage, thread pools, and API request counts.

#### Actuator Endpoints

The below endpoints will be up when the server is running which can be either 
through docker-compose up --build command or going to server module and using maven command line
to start the server (mvn spring-boot:run)

* **http://localhost:8080/actuator** : Shows a list of all available Actuator endpoints.
* **http://localhost:8080/actuator/health** : Displays the application's health status (e.g., UP or DOWN) and component-specific health checks.
* **http://localhost:8080/actuator/metrics** : Provides detailed application metrics (e.g., memory, CPU, JVM stats, HTTP request counts, etc.).
* **http://localhost:8080/actuator/metrics/conversion.success.count** : Custom metrics to track total number of successfully conversions.

#### Centralized Logging

Structured logging has been added to the backend, ensuring:

* Logs are output both to the console and to a log file (logs/romanconversion.log).

* Log levels can be configured dynamically for different components.

* Logs provide detailed debugging, error handling, and API activity insights.









