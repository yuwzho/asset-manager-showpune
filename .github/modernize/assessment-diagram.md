# Application Architecture Diagram

## Assets Manager - Architecture Overview

```mermaid
flowchart TD
    User["User / Browser"]

    subgraph WebModule["Web Module (assets-manager-web)"]
        WebApp["Spring MVC Web App\nSpring Boot 3.2.1 / Java 17"]
        ThymeleafUI["Thymeleaf UI\nPresentation Layer"]
        S3Ctrl["S3 Controller\nFile Upload / Download / Delete"]
        HomeCtrl["Home Controller"]
        StorageSvc["Storage Service\nAwsS3Service / LocalFileStorageService"]
        MsgPublisher["Message Publisher\nRabbitTemplate"]
        JpaWeb["Spring Data JPA\nImageMetadata Repository"]
    end

    subgraph WorkerModule["Worker Module (assets-manager-worker)"]
        WorkerApp["Worker Application\nSpring Boot 3.2.1 / Java 17"]
        MsgConsumer["RabbitMQ Listener\nimage-processing queue"]
        FileProcessor["File Processor\nS3FileProcessingService / LocalFileProcessingService"]
        JpaWorker["Spring Data JPA\nImageMetadata Repository"]
    end

    subgraph ExternalServices["External Services"]
        S3["AWS S3\nObject Storage"]
        RabbitMQ["RabbitMQ\nMessage Broker"]
        PostgreSQL["PostgreSQL\nMetadata Database"]
    end

    User -->|HTTP requests| ThymeleafUI
    ThymeleafUI --> S3Ctrl
    ThymeleafUI --> HomeCtrl
    S3Ctrl --> StorageSvc
    StorageSvc -->|Upload / Download / Delete files| S3
    StorageSvc --> MsgPublisher
    MsgPublisher -->|Publish image-processing message| RabbitMQ
    StorageSvc --> JpaWeb
    JpaWeb -->|Store and query metadata| PostgreSQL

    MsgConsumer -->|Consume image-processing message| RabbitMQ
    MsgConsumer --> FileProcessor
    FileProcessor -->|Download original and upload thumbnail| S3
    FileProcessor --> JpaWorker
    JpaWorker -->|Update thumbnail metadata| PostgreSQL
```

## Technology Stack

| Layer | Technology |
|-------|-----------|
| Language | Java 17 |
| Framework | Spring Boot 3.2.1 |
| Presentation | Spring MVC, Thymeleaf |
| Messaging | Spring AMQP, RabbitMQ |
| Object Storage | AWS SDK 2.25.13, Amazon S3 |
| Data Access | Spring Data JPA, Hibernate |
| Database | PostgreSQL (production), H2 (testing) |
| Serialization | Jackson (JSON) |
| Build Tool | Maven |

## Module Descriptions

### Web Module (`assets-manager-web`)
Handles HTTP requests for file uploads, listing, viewing, and deletion. Stores files in AWS S3, persists metadata in PostgreSQL, and publishes image-processing messages to RabbitMQ after each upload. Supports a local file storage profile (`dev`) for development.

### Worker Module (`assets-manager-worker`)
Consumes image-processing messages from RabbitMQ. Downloads the original image from AWS S3, generates a thumbnail, uploads the thumbnail back to S3, and updates the image metadata in PostgreSQL.

## External Dependencies

| Service | Purpose |
|---------|---------|
| AWS S3 | Stores original uploaded files and generated thumbnails |
| RabbitMQ | Decouples upload (web) from thumbnail generation (worker) via `image-processing` queue |
| PostgreSQL | Persists file metadata including S3 keys, URLs, and thumbnail references |
