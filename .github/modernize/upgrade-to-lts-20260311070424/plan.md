# Upgrade Plan

## Overview

Upgrade the Java project to the latest LTS versions: **Java 21** and **Spring Boot 3.4**.

This includes updating the JDK, Spring Framework to 6.x, and migrating `javax.*` to `jakarta.*` namespaces where required. All Spring ecosystem dependencies (Spring Security, Spring Data, Spring Cloud, etc.) will be aligned to versions compatible with Spring Boot 3.4.

## Tasks

See [tasks.json](./tasks.json) for the detailed task breakdown.

| ID | Description | Status |
|----|-------------|--------|
| 001-upgrade-java-spring-boot | Upgrade to Java 21 and Spring Boot 3.4 | Completed |
