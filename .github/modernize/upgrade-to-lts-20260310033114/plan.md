# Upgrade Plan

## Overview
Upgrade the Java project to the latest LTS versions: Java 21 and Spring Boot 3.4.

## Tasks
See `tasks.json` for detailed task breakdown.

### 001 - Upgrade Java & Spring Boot
- **Target Java**: 21 (LTS)
- **Target Spring Boot**: 3.4
- **Target Spring Framework**: 6.x
- **Key changes**: Migrate `javax.*` to `jakarta.*` namespace, update all Spring ecosystem dependencies to Spring Boot 3.4-compatible versions, and address deprecated APIs.
