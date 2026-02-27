# Asset Manager - Architecture Diagram

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Browser["Web Browser"]
    end

    subgraph WebModule["Web Module - assets-manager-web (Spring Boot 3.2.1 / Java 17)"]
        Thymeleaf["Thymeleaf Templates\n(UI / HTML Views)"]
        Controllers["Spring MVC Controllers\n(HomeController, S3Controller)"]
        StorageSvc["Storage Service\n(AwsS3Service / LocalFileStorageService)"]
        MsgPublisher["Message Publisher\n(BackupMessageProcessor)"]
        WebJPA["Spring Data JPA\n(ImageMetadataRepository)"]
    end

    subgraph WorkerModule["Worker Module - assets-manager-worker (Spring Boot 3.2.1 / Java 17)"]
        MsgConsumer["Message Consumer\n(AbstractFileProcessingService)"]
        ThumbnailGen["Thumbnail Generator\n(javax.imageio - 600px max)"]
        WorkerStorage["File Processing Service\n(S3FileProcessingService / LocalFileProcessingService)"]
        WorkerJPA["Spring Data JPA\n(ImageMetadataRepository)"]
    end

    subgraph ExternalServices["External Services"]
        RabbitMQ["RabbitMQ\nimage-processing queue\n(AMQP)"]
        S3["AWS S3\n(Object Storage)"]
        PostgreSQL["PostgreSQL\n(Relational Database)"]
        LocalFS["Local Filesystem\n(dev profile)"]
    end

    Browser -->|"HTTP requests"| Thymeleaf
    Thymeleaf --> Controllers
    Controllers --> StorageSvc
    StorageSvc -->|"Upload files"| S3
    StorageSvc -->|"dev profile"| LocalFS
    StorageSvc --> MsgPublisher
    MsgPublisher -->|"Publish messages"| RabbitMQ
    Controllers --> WebJPA
    WebJPA -->|"Store metadata"| PostgreSQL

    RabbitMQ -->|"Consume messages"| MsgConsumer
    MsgConsumer --> ThumbnailGen
    ThumbnailGen --> WorkerStorage
    WorkerStorage -->|"Store thumbnails"| S3
    WorkerStorage -->|"dev profile"| LocalFS
    MsgConsumer --> WorkerJPA
    WorkerJPA -->|"Update metadata"| PostgreSQL
```

## Architecture Overview

The **Asset Manager** is a Spring Boot multi-module Java application with two independently deployable services:

### Modules

| Module | Purpose | Port |
|--------|---------|------|
| `assets-manager-web` | Handles file uploads, listing, viewing, and deletion | 8080 |
| `assets-manager-worker` | Asynchronously processes images and generates thumbnails | 8081 |

### Technology Stack

| Layer | Technology |
|-------|-----------|
| Language | Java 17 |
| Framework | Spring Boot 3.2.1 |
| Web UI | Thymeleaf |
| Messaging | Spring AMQP / RabbitMQ |
| Storage | AWS S3 (SDK v2.25.13) |
| Database | PostgreSQL (JPA/Hibernate) |
| Image Processing | javax.imageio |
| Code Generation | Lombok |

### Key Data Flows

1. **File Upload**: Browser → Web Controller → Storage Service → AWS S3 + PostgreSQL → RabbitMQ message published
2. **Thumbnail Generation**: RabbitMQ message consumed → Worker → Download from S3 → Generate thumbnail (600px max) → Upload thumbnail to S3 → Update PostgreSQL
3. **File Viewing**: Browser → Web Controller → Storage Service → Retrieve from S3 → Stream to browser

### External Dependencies

- **AWS S3**: Primary object storage for uploaded files and generated thumbnails
- **RabbitMQ**: Message broker for decoupling upload (web) from processing (worker)
- **PostgreSQL**: Relational database for file metadata (`ImageMetadata` entity)
- **Local Filesystem**: Used as a fallback in `dev` Spring profile

### Deployment Profiles

- **Default**: Uses AWS S3 for storage
- **`dev` profile**: Uses local filesystem instead of S3
- **`backup` profile**: Activates additional message monitoring consumer in web module
