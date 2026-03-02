# Modernization Summary: 001-upgrade-java-version

## Task: Upgrade Java to version 21 (LTS)

## Changes Made

### `pom.xml` (parent)
- Updated `<java.version>` property from `17` to `21`

## Verification

| Criteria | Result |
|---|---|
| Build passes | ✅ SUCCESS |
| Unit tests pass | ✅ SUCCESS (BUILD SUCCESS) |

## Notes
- Java 21 (Temurin) was already available on the build environment.
- No source code changes were required; the Spring Boot 3.2.1 dependencies are compatible with Java 21.
- The child modules (`assets-manager-web`, `assets-manager-worker`) inherit `java.version` from the parent POM and required no individual changes.
