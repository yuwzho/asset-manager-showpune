# Modernization Assessment Summary

**Target Azure Services**: Azure Kubernetes Service, Azure App Service, Azure Container Apps

## Overall Statistics

**Total Applications**: 1

**Name: assets-manager-parent**
- Mandatory: 8 issues
- Potential: 4 issues
- Optional: 4 issues

> **Severity Levels Explained:**
> - **Mandatory**: The issue has to be resolved for the migration to be successful.
> - **Potential**: This issue may be blocking in some situations but not in others. These issues should be reviewed to determine whether a change is required or not.
> - **Optional**: The issue discovered is real issue fixing which could improve the app after migration, however it is not blocking.

## Applications Profile

### Name: assets-manager-parent
- **JDK Version**: 17
- **Frameworks**: Spring Boot, Spring
- **Languages**: Java
- **Build Tools**: Maven

**Key Findings**:
- **Mandatory Issues (54 locations)**:
  - <!--ruleid=azure-aws-config-region-02000-->AWS region configuration (5 locations found)
  - <!--ruleid=azure-aws-config-s3-03001-->AWS S3 dependency usage found (2 locations found)
  - <!--ruleid=azure-aws-config-s3-03000-->AWS S3 usage found (11 locations found)
  - <!--ruleid=spring-framework-version-01000-->Spring Framework Version End of OSS Support (8 locations found)
  - <!--ruleid=spring-boot-to-azure-spring-boot-version-01000-->Spring Boot Version is End of OSS Support (11 locations found)
  - <!--ruleid=localhost-jdbc-00002-->Local JDBC Calls (2 locations found)
  - <!--ruleid=dockerfile-00000-->No Dockerfile found (1 location found)
  - <!--ruleid=local-storage-00005-->File system - Java NIO (14 locations found)
- **Potential Issues (14 locations)**:
  - <!--ruleid=azure-database-postgresql-02000-->PostgreSQL database found (5 locations found)
  - <!--ruleid=azure-password-01000-->Password found in configuration file (5 locations found)
  - <!--ruleid=spring-boot-to-azure-port-01000-->Server port configuration found (1 location found)
  - <!--ruleid=spring-boot-to-azure-restricted-config-01000-->Restricted configurations found (3 locations found)
- **Optional Issues (21 locations)**:
  - <!--ruleid=azure-message-queue-amqp-02000-->Spring AMQP dependency found (3 locations found)
  - <!--ruleid=azure-message-queue-config-rabbitmq-01000-->RabbitMQ connection string, username or password found in configuration file (6 locations found)
  - <!--ruleid=azure-message-queue-rabbitmq-01000-->Spring RabbitMQ usage found in code (10 locations found)
  - <!--ruleid=localhost-00004-->Localhost Usage (2 locations found)

## Next Steps

For comprehensive migration guidance and best practices, visit:
- [GitHub Copilot modernization](https://aka.ms/ghcp-appmod)

Have questions or suggestions? [Share your feedback](https://aka.ms/ghcp-appmod/feedback)
