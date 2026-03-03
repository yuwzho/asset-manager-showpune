# Modernization Summary: Upgrade Java 17 → 21 & Spring Boot 3.2 → 3.4

## Task ID
`001-upgrade-java-spring-boot`

## Description
Upgrade JDK from 17 to 21 and Spring Boot from 3.2.1 to 3.4.13 (latest 3.4.x).

## Changes Made

### `pom.xml` (root)
| Property | Before | After |
|---|---|---|
| `spring-boot-starter-parent` version | `3.2.1` | `3.4.13` |
| `java.version` | `17` | `21` |

### Jakarta Namespace
No changes required — the codebase already uses `jakarta.*` imports (Jakarta EE 9+), which is the correct namespace for Spring Boot 3.x. Standard Java SE `javax.imageio.*` APIs are not subject to the Jakarta EE namespace migration and remain unchanged.

### Deprecations
No deprecated API usages found that require code changes for the 3.2 → 3.4 upgrade path.

## Dependency Impact
| Dependency | Notes |
|---|---|
| Spring Boot BOM (all managed deps) | Automatically upgraded via parent POM bump to 3.4.13 |
| `software.amazon.awssdk:s3` | Remains at `2.25.13`; compatible with Java 21 and Spring Boot 3.4 |
| `org.projectlombok:lombok` | Version managed by Spring Boot BOM; compatible with Java 21 |

## Build & Test Results
| Criterion | Result |
|---|---|
| `passBuild` | ✅ PASS — `BUILD SUCCESS` with `javac [release 21]` |
| `passUnitTests` | ✅ PASS — `Tests run: 1, Failures: 0, Errors: 0, Skipped: 0` |
| `passIntegrationTests` | N/A (not required) |
| `generateNewUnitTests` | N/A (not required) |
| `securityComplianceCheck` | N/A (not required) |

## Notes
- Java 21 is the current LTS release (Temurin 21.0.10).
- Spring Boot 3.4.13 ships with Spring Framework 6.2.x, which aligns with the Spring Framework 6.x requirement.
- The `Dynamic loading of agents will be disallowed by default in a future release` warning is a known JVM notice from Spring's test support on Java 21 and does not affect functionality.
