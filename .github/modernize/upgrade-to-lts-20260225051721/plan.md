# Upgrade Plan

## Overview
Upgrade to latest LTS versions (Java 21 and Spring Boot 3.4).

## Objectives
- Migrate to Java 21 (latest LTS version)
- Upgrade Spring Boot to 3.4 (latest LTS version)
- Update Spring Framework to 6.x
- Migrate javax.* to jakarta.* namespace

## Tasks
See `tasks.json` for detailed task breakdown and execution tracking.

## Notes
- Java 21 upgrade must be completed before Spring Boot 3.4 upgrade due to dependency requirements
- Spring Boot 3.x requires Java 17 or higher and uses Jakarta EE 9+ (jakarta.* namespace)
- All breaking changes and deprecations will be addressed during the upgrade process
