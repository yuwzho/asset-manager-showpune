
# Upgrade Java Project

## 🖥️ Project Information
- **Project path**: D:\code\ai\samples\repos\asset-manager-showpune-fork
- **Java version**: 21
- **Build tool type**: Maven Wrapper
- **Build tool path**: D:\code\ai\samples\repos\asset-manager-showpune-fork

## 🎯 Goals

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
| org.springframework.boot:spring-boot-starter-thymeleaf | 3.2.1 | 3.4.3 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-web | 3.2.1 | 3.4.3 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-amqp | 3.2.1 | 3.4.3 | assets-manager-web |
| org.springframework.boot:spring-boot-devtools | 3.2.1 | 3.4.3 | assets-manager-web |
| org.springframework.boot:spring-boot-configuration-processor | 3.2.1 | 3.4.3 | assets-manager-web |
| org.projectlombok:lombok | 1.18.30 | 1.18.36 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-test | 3.2.1 | 3.4.3 | assets-manager-web |
| org.springframework.boot:spring-boot-starter-data-jpa | 3.2.1 | 3.4.3 | assets-manager-web |
| org.postgresql:postgresql | 42.6.0 | 42.7.7 | assets-manager-web |
| com.h2database:h2 | 2.2.224 | 2.3.232 | assets-manager-web |
| org.springframework.boot:spring-boot-starter | 3.2.1 | 3.4.3 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-amqp | 3.2.1 | 3.4.3 | assets-manager-worker |
| org.projectlombok:lombok | 1.18.30 | 1.18.36 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-test | 3.2.1 | 3.4.3 | assets-manager-worker |
| com.fasterxml.jackson.core:jackson-databind | 2.15.3 | 2.18.2 | assets-manager-worker |
| org.springframework.boot:spring-boot-starter-data-jpa | 3.2.1 | 3.4.3 | assets-manager-worker |
| org.postgresql:postgresql | 42.6.0 | 42.7.7 | assets-manager-worker |

### Code commits

All code changes have been committed to branch `main`, here are the details:
6 files changed, 13 insertions(+), 12 deletions(-)

- eb9376a -- Upgrade Spring Boot from 3.2.1 to 3.3.x using OpenRewrite

- 789a6e7 -- Upgrade Spring Boot from 3.3.13 to 3.4.3

- 078504b -- Fix CVE-2025-49146: Upgrade postgresql driver to 42.7.7
### Potential Issues
