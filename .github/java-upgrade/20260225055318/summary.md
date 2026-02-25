
# Upgrade Java Project

## 🖥️ Project Information
- **Project path**: D:\code\ai\samples\repos\asset-manager-showpune-fork
- **Java version**: 21
- **Build tool type**: Maven Wrapper
- **Build tool path**: D:\code\ai\samples\repos\asset-manager-showpune-fork

## 🎯 Goals

- Upgrade Java to 21
- Upgrade Spring Boot to 3.4.x

## 🔀 Changes

### Test Changes
|     | Total | Passed | Failed | Skipped | Errors |
|-----|-------|--------|--------|---------|--------|
| Before | 1 | 1 | 0 | 0 | 0 |
| After | 1 | 1 | 0 | 0 | 0 |
### Dependency Changes


#### Upgraded Dependencies
| Dependency | Original Version | Current Version | Module |
|------------|------------------|-----------------|--------|
| org.springframework.boot:spring-boot-starter-thymeleaf | 3.2.1 | 3.4.5 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-web | 3.2.1 | 3.4.5 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-amqp | 3.2.1 | 3.4.5 | assets-manager-web |
| org.springframework.boot:spring-boot-devtools | 3.2.1 | 3.4.5 | assets-manager-web |
| org.springframework.boot:spring-boot-configuration-processor | 3.2.1 | 3.4.5 | assets-manager-web |
| org.projectlombok:lombok | 1.18.30 | 1.18.38 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-test | 3.2.1 | 3.4.5 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-data-jpa | 3.2.1 | 3.4.5 | assets-manager-web |
| org.postgresql:postgresql | 42.6.0 | 42.7.7 | assets-manager-web |
| com.h2database:h2 | 2.2.224 | 2.3.232 | assets-manager-web |
| org.springframework.boot:spring-boot-starter | 3.2.1 | 3.4.5 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-amqp | 3.2.1 | 3.4.5 | assets-manager-worker |
| org.projectlombok:lombok | 1.18.30 | 1.18.38 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-test | 3.2.1 | 3.4.5 | assets-manager-worker |
| com.fasterxml.jackson.core:jackson-databind | 2.15.3 | 2.18.3 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-data-jpa | 3.2.1 | 3.4.5 | assets-manager-worker |
| org.postgresql:postgresql | 42.6.0 | 42.7.7 | assets-manager-worker |
| Java | 17 | 21 | Root Module |

### Code commits

> There are uncommitted changes in the project before upgrading, which have been stashed.

All code changes have been committed to branch `appmod/java-upgrade-20260225055318`, here are the details:
8 files changed, 19 insertions(+), 17 deletions(-)

- f87f72c -- Upgrade to Java 21 and Spring Boot 3.3.13

- fde0aef -- Upgrade Spring Boot to 3.4.5

- 148b77f -- Fix CVE-2025-49146 by upgrading PostgreSQL JDBC driver to 42.7.7
### Potential Issues
