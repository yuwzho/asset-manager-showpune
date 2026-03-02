# Java Upgrade Plan - Latest LTS Versions

## Overview

This plan upgrades the Java project to the latest Long-Term Support (LTS) versions:
- **Java 21** (latest LTS)
- **Spring Boot 3.4** (latest stable)
- **Updated dependencies** compatible with the latest ecosystem

## Migration Path

The upgrade is structured in three phases to minimize risk:

1. **Java Version Upgrade** - Migrate to Java 21 LTS
2. **Spring Boot Upgrade** - Update to Spring Boot 3.4 with Spring Framework 6.x and jakarta.* namespace
3. **Dependency Updates** - Upgrade all dependencies to latest compatible versions

## Tasks

See `tasks.json` for detailed task breakdown, dependencies, requirements, and success criteria.

## Key Changes

- Java language level: Java 21
- Spring Boot: 3.4.x
- Spring Framework: 6.x
- Namespace migration: javax.* → jakarta.*
- Build tools and plugins updated to latest stable versions

## Prerequisites

- JDK 21 installation
- Maven 3.9+ or Gradle 8.5+
- Updated IDE support for Java 21 and Spring Boot 3.4
