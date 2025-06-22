# Freight Trust and Connectivity System (FTCS) - Backend

This is the backend server for the FTCS platform, a comprehensive system for managing transportation, finance, and related services. It is built with Java and the Spring Boot framework, following a modular monolithic architecture.

## ✨ Key Features

- **Authentication & Authorization**: Secure user login and access control using JWT.
- **Account Management**: Handles user profiles, roles, and data.
- **Transportation Service**: Manages trip creation, routing, and logistics using GraphHopper for route optimization.
- **Real-time Service**: Provides real-time communication (e.g., location tracking) using Socket.IO.
- **Finance & Payments**: Integrates with VietQR for seamless QR code payments.
- **Balance Management**: Manages user wallet balances.
- **Rating System**: Allows users to rate services.
- **Voucher & Bonus System**: Manages promotional vouchers and user bonuses.
- **File Storage**: Uses MinIO for object storage (e.g., user avatars, documents).

---

## 🛠️ Technologies Used

- **Framework**: Spring Boot 3.2.4
- **Language**: Java 17
- **Build Tool**: Maven
- **Database**: Microsoft SQL Server
- **Authentication**: JSON Web Tokens (JWT)
- **Real-time Communication**: Socket.IO
- **Containerization**: Docker
- **External APIs**:
  - GraphHopper API (Routing)
  - Goong API (Geocoding/Mapping)
  - VietQR API (Payments)

---

## 🚀 Getting Started

Follow these instructions to get a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

- [Git](https://git-scm.com/)
- [Java Development Kit (JDK) 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- [Apache Maven](https://maven.apache.org/download.cgi)
- [Docker](https://www.docker.com/products/docker-desktop/) (Optional, for containerized deployment)

### Installation & Setup

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/QuocLe2308/FTCS_BE.git
    cd FTCS_BE
    ```

2.  **Configure Environment Variables:**
    This project uses the `application.properties` file located in `main/src/main/resources/`. For security and flexibility, it is highly recommended to override these properties using environment variables or a profile-specific configuration file (`application-dev.properties`).

    Create an `application-dev.properties` file in the same directory and activate the `dev` profile by setting the `spring.profiles.active=dev` environment variable.

    See the [Configuration](#-configuration) section below for a full list of required variables.

3.  **Build the project:**
    Use Maven to compile the code and package it into a `.jar` file.
    ```sh
    mvn clean package -DskipTests
    ```
    This command skips running tests during the build process.

4.  **Run the application:**
    Once the build is complete, you can run the application with the following command:
    ```sh
    java -jar main/target/main-1.0-SNAPSHOT.jar
    ```
    The server will start on the port configured in your properties file (default is `8080`).

---

## 🐳 Running with Docker

You can also build and run the application using the provided `Dockerfile`.

1.  **Build the Docker image:**
    ```sh
    docker build -t ftcs-be:latest .
    ```

2.  **Run the Docker container:**
    Make sure to pass all the required environment variables to the container.
    ```sh
    docker run -p 8080:8080 -p 9090:9090 \
      -e SPRING_PROFILES_ACTIVE=prod \
      -e SPRING_DATASOURCE_URL="..." \
      -e SPRING_DATASOURCE_USERNAME="..." \
      -e SPRING_DATASOURCE_PASSWORD="..." \
      -e JWT_SECRET="..." \
      # ... add all other required variables
      ftcs-be:latest
    ```

---

## ⚙️ Configuration

The following environment variables are required to run the application. You can set them in your operating system or in a profile-specific `.properties` file.

| Variable                            | Description                                        | Example                                                              |
| ----------------------------------- | -------------------------------------------------- | -------------------------------------------------------------------- |
| `SERVER_PORT`                       | Port for the main HTTP server.                     | `8080`                                                               |
| `JWT_SECRET`                        | 32-byte secret key for signing JWTs.               | `your-very-strong-and-long-jwt-secret`                               |
| `JWT_TOKEN_EXPIRATION`              | Expiration time for access tokens in milliseconds. | `86400000` (24 hours)                                                |
| `SPRING_DATASOURCE_URL`             | JDBC URL for the SQL Server database.              | `jdbc:jtds:sqlserver://localhost;databaseName=ftcs`                  |
| `SPRING_DATASOURCE_USERNAME`        | Database username.                                 | `sa`                                                                 |
| `SPRING_DATASOURCE_PASSWORD`        | Database password.                                 | `yourStrong(!)Password`                                              |
| `SPRING_MAIL_HOST`                  | SMTP server host for sending emails.               | `smtp.gmail.com`                                                     |
| `SPRING_MAIL_PORT`                  | SMTP server port.                                  | `587`                                                                |
| `SPRING_MAIL_USERNAME`              | Email account username.                            | `your-email@example.com`                                             |
| `SPRING_MAIL_PASSWORD`              | Email account password or app-specific password.   | `your-email-password`                                                |
| `INTERNAL_MINIO_ACCESS`             | Access key for MinIO storage.                      | `minioadmin`                                                         |
| `INTERNAL_MINIO_SECRET`             | Secret key for MinIO storage.                      | `minioadmin`                                                         |
| `INTERNAL_MINIO_API`                | Public-facing URL for MinIO content.               | `https://your-minio-domain.com`                                      |
| `INTERNAL_MINIO_ENDPOINT`           | Internal endpoint for the MinIO server.            | `https://minio:9000`                                                 |
| `GRAPHHOPPER_API_KEY`               | API key for the GraphHopper service.               | `your-graphhopper-api-key`                                           |
| `GOONG_API_KEY`                     | API key for the Goong mapping service.             | `your-goong-api-key`                                                 |
| `SOCKET_SERVER_PORT`                | Port for the Socket.IO server.                     | `9090`                                                               |
| `VIETQR_API_URL`                    | URL for the VietQR API.                            | `https://api.vietqr.io/v2/generate`                                  |
| `VIETQR_BANK_ACCOUNT`               | Bank account number for QR generation.             | `123456789`                                                          |
| `VIETQR_BANK_HOLDER`                | Bank account holder name.                          | `NGUYEN VAN A`                                                       |
| `VIETQR_BANK_ID`                    | ACQ ID of the bank.                                | `970436`                                                             |

---


