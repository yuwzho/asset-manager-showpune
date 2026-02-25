# Modernization Summary: 001-upgrade-java-version

## Task
Upgrade Java to version 21 (latest LTS)

## Changes Made

### `pom.xml` (root)
- Updated `<java.version>` property from `17` to `21`

This single change propagates to both child modules (`assets-manager-web` and `assets-manager-worker`) via the Spring Boot parent POM, which uses `java.version` to set both `maven.compiler.source` and `maven.compiler.target`.

## Verification

- **Build**: `BUILD SUCCESS` with Java 21 (`javac [debug release 21]`)
- **Unit Tests**: 1 test passed (`AssetsManagerApplicationTests`)
- **Integration Tests**: Not run (not required per success criteria)

## Success Criteria

| Criterion              | Result  |
|------------------------|---------|
| passBuild              | ✅ true  |
| generateNewUnitTests   | ✅ false |
| generateNewIntegrationTests | ✅ false |
| passUnitTests          | ✅ true  |
| passIntegrationTests   | ✅ false (not run) |
