
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

### Code commits

All code changes have been committed to branch `appmod/java-upgrade-20260302035614`, here are the details:
7 files changed, 19 insertions(+), 12 deletions(-)

- d357966 -- Apply OpenRewrite recipe to upgrade Spring Boot to 3.3.x

- 592b47d -- Upgrade Spring Boot to 3.4.5

- 2095436 -- Fix CVE-2025-49146: upgrade postgresql to 42.7.7
### Potential Issues
