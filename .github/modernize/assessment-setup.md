# AppCAT Assessment Setup Instructions

## Status: MCP Tools Not Configured

The AppCAT assessment for this Java project requires the following MCP tools which are not currently configured in this environment:

- `appmod-precheck-assessment`
- `appmod-run-assessment`

## How to Set Up AppCAT Assessment

To run a full AppCAT assessment for this Java project, configure the AppCAT MCP server in your Copilot agent environment:

1. **Install the AppCAT MCP Server**

   Follow the setup instructions at the [Azure Migrate AppCAT documentation](https://learn.microsoft.com/en-us/azure/migrate/appcat/java).

2. **Configure the MCP Server**

   Add the MCP server to your agent configuration so that the `appmod-precheck-assessment` and `appmod-run-assessment` tools become available.

3. **Re-run the Assessment**

   Once the MCP tools are configured, re-trigger the assessment by asking the agent to:
   > "Assess the application using the assessment skill"

   The assessment will:
   - Clean previous data from `.github/modernize/appcat/`
   - Run AppCAT analysis via the MCP server
   - Generate a report at `.github/modernize/report.json`

## Application Summary (Manual Analysis)

Based on static analysis of the project, the following key facts were identified:

| Property | Value |
|----------|-------|
| Project Type | Java (Maven multi-module) |
| Java Version | 17 |
| Spring Boot Version | 3.2.1 |
| Modules | `web`, `worker` |
| AWS SDK Version | 2.25.13 |
| Message Broker | RabbitMQ (Spring AMQP) |
| Database | PostgreSQL (Spring Data JPA) |
| Object Storage | Amazon S3 |

### Potential Migration Considerations

- **AWS S3 SDK**: Uses AWS SDK v2 (`software.amazon.awssdk:s3:2.25.13`). Consider migrating to Azure Blob Storage.
- **RabbitMQ**: Self-managed RabbitMQ broker. Consider migrating to Azure Service Bus.
- **PostgreSQL**: Self-managed PostgreSQL instance. Consider migrating to Azure Database for PostgreSQL.
- **Java 17**: Eligible for LTS upgrade to Java 21.
- **Spring Boot 3.2.1**: Consider upgrading to a more recent Spring Boot 3.x LTS release.
