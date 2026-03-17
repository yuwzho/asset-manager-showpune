# Modernization Summary: Upgrade Java 21 and Spring Boot 3.4

## Task ID
`001-upgrade-java-spring-boot`

## Status
✅ Completed

## Changes Made

### `pom.xml` (root)
- **Spring Boot**: `3.2.1` → `3.4.7` (latest 3.4.x)
- **Java version**: `17` → `21`

All transitive Spring Framework (6.x), Spring Data, Spring AMQP, and Hibernate dependencies are automatically managed via the Spring Boot BOM at 3.4.7.

## Migration Notes

### javax.* → jakarta.* Namespace
No changes were required. The codebase already used `jakarta.persistence.*` in both the `web` and `worker` modules' model classes. The remaining `javax.imageio.*` usage in `AbstractFileProcessingService.java` is from the JDK standard library (not Jakarta EE) and remains under `javax.imageio` in Java 21.

### Dependency Version Changes (via Spring Boot BOM)
| Dependency | Previous (3.2.1 BOM) | New (3.4.7 BOM) |
|---|---|---|
| Spring Framework | 6.1.x | 6.2.x |
| Hibernate ORM | 6.4.x | 6.6.x |
| Spring AMQP | 3.1.x | 3.2.x |
| Spring Data JPA | 3.2.x | 3.4.x |

## Build & Test Results

| Check | Result |
|---|---|
| `web` module build | ✅ PASS |
| `worker` module build | ✅ PASS |
| Unit tests (`web`) | ✅ PASS (1/1) |
| Integration tests | ⚠️ N/A (excluded per success criteria: `passIntegrationTests=false`) |
| Spring Boot version at test runtime | 3.4.7 |
