
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
| Java | 17 | 21 | Root Module |

#### Removed Dependencies
|   Dependency   | Version | Module |
|----------------|---------|--------|
| org.springframework.boot:spring-boot-starter-thymeleaf | 3.2.1 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-web | 3.2.1 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-amqp | 3.2.1 | assets-manager-web |
| software.amazon.awssdk:s3 | 2.25.13 | assets-manager-web |
| org.springframework.boot:spring-boot-devtools | 3.2.1 | assets-manager-web |
| org.springframework.boot:spring-boot-configuration-processor | 3.2.1 | assets-manager-web |
| org.projectlombok:lombok | 1.18.30 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-test | 3.2.1 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-data-jpa | 3.2.1 | assets-manager-web |
| org.postgresql:postgresql | 42.6.0 | assets-manager-web |
| com.h2database:h2 | 2.2.224 | assets-manager-web |
| org.springframework.boot:spring-boot-starter | 3.2.1 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-amqp | 3.2.1 | assets-manager-worker |
| software.amazon.awssdk:s3 | 2.25.13 | assets-manager-worker |
| org.projectlombok:lombok | 1.18.30 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-test | 3.2.1 | assets-manager-worker |
| com.fasterxml.jackson.core:jackson-databind | 2.15.3 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-data-jpa | 3.2.1 | assets-manager-worker |
| org.postgresql:postgresql | 42.6.0 | assets-manager-worker |

### Code commits

All code changes have been committed to branch `main`, here are the details:
8 files changed, 19 insertions(+), 17 deletions(-)

- 4aa209f -- Apply OpenRewrite recipes to upgrade Spring Boot to 3.3.13 and Java to 21 (Milestone 1)

- ec18759 -- Upgrade Spring Boot from 3.3.13 to 3.4.5 (Milestone 2)

- dbd5f6b -- Fix CVE-2025-49146: upgrade postgresql from 42.7.5 to 42.7.7
### Potential Issues
