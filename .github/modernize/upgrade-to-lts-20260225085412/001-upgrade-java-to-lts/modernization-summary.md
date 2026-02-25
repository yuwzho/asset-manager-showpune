# Modernization Summary: 001-upgrade-java-to-lts

## Task Description
Upgrade Java to version 21 (LTS)

## Changes Made

### `pom.xml` (root)
- Updated `<java.version>` property from `17` to `21`

## Verification

| Criterion | Result |
|-----------|--------|
| Build passes | ✅ Pass |
| Unit tests pass | ✅ Pass |
| Generate new unit tests | N/A (not required) |
| Generate new integration tests | N/A (not required) |
| Integration tests pass | N/A (not required) |
| Security compliance check | N/A (not required) |

## Notes
- Java 21 (Eclipse Temurin) was already available in the environment (`/usr/lib/jvm/temurin-21-jdk-amd64`).
- The Spring Boot parent version `3.2.1` is fully compatible with Java 21.
- Both the `assets-manager-web` and `assets-manager-worker` modules compiled and their tests passed successfully with Java 21.
- No source-level code changes were required — the single property change in the root `pom.xml` was sufficient.
