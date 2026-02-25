# Upgrade Plan

## Overview
This plan upgrades the Java project to the latest LTS versions: Java 21 and Spring Boot 3.4.

## Tasks
See `tasks.json` for the detailed task breakdown and execution plan.

### Task Summary
1. **001-upgrade-java-version**: Upgrade Java to version 21 (LTS)
2. **002-upgrade-spring-boot**: Upgrade Spring Boot to version 3.4 (latest stable) with Spring Framework 6.x

## Notes
- Java 21 is the latest Long-Term Support (LTS) version
- Spring Boot 3.4 requires Java 17+ and includes migration to jakarta.* namespace
- Tasks are executed sequentially with dependencies managed automatically
