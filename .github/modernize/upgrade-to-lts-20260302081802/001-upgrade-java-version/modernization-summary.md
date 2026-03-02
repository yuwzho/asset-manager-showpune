# Modernization Summary: 001-upgrade-java-version

## Task Information
- **Task ID**: 001-upgrade-java-version
- **Description**: Upgrade Java to version 21 (LTS)
- **Skill Used**: `migration-java-version-upgrade` (built-in)
- **Working Branch**: `appmod/java-upgrade-20260302083624`

## Overview

The project (`assets-manager-parent`) was upgraded from **Java 17** to **Java 21** (LTS). The upgrade was performed using the OpenRewrite recipe `org.openrewrite.java.migrate.UpgradeToJava21` from the `rewrite-migrate-java:2.31.1` library. The build and all tests pass successfully after the upgrade.

## Changes Made

### 1. Build Configuration (`pom.xml`)
| Property | Before | After |
|----------|--------|-------|
| `java.version` | `17` | `21` |

### 2. Source Code Changes

#### `web/src/main/java/com/microsoft/migration/assets/service/LocalFileStorageService.java`
- Replaced wildcard import `java.nio.file.*` with explicit imports (`Files`, `Path`, `StandardCopyOption`) for better clarity
- Replaced deprecated `Paths.get(storageDirectory)` with the modern `Path.of(storageDirectory)` API

#### `worker/src/main/java/com/microsoft/migration/assets/worker/service/LocalFileProcessingService.java`
- Removed unused `java.nio.file.Paths` import
- Replaced deprecated `Paths.get(storageDirectory)` with the modern `Path.of(storageDirectory)` API

### Summary of File Changes
```
3 files changed, 6 insertions(+), 5 deletions(-)
  pom.xml
  web/src/main/java/com/microsoft/migration/assets/service/LocalFileStorageService.java
  worker/src/main/java/com/microsoft/migration/assets/worker/service/LocalFileProcessingService.java
```

## Success Criteria Results

| Criterion | Status |
|-----------|--------|
| `passBuild` | ✅ PASS — Build succeeded with Java 21 |
| `passUnitTests` | ✅ PASS — 1/1 tests passed (same as before upgrade) |
| `generateNewUnitTests` | N/A — Not required |
| `generateNewIntegrationTests` | N/A — Not required |
| `passIntegrationTests` | N/A — Not required |
| `securityComplianceCheck` | N/A — Not required |

## Test Results

|  | Total | Passed | Failed | Skipped | Errors |
|--|-------|--------|--------|---------|--------|
| Before Upgrade | 1 | 1 | 0 | 0 | 0 |
| After Upgrade | 1 | 1 | 0 | 0 | 0 |

## Known Issues / Observations

> ⚠️ A pre-existing **CRITICAL** CVE was detected in a transitive dependency — **not introduced by this upgrade**:
>
> - **CVE-2024-1597** (`org.postgresql:postgresql:42.6.0`): SQL Injection via line comment generation  
>   See: [GHSA-24rp-q3w6-vc56](https://github.com/advisories/GHSA-24rp-q3w6-vc56)
>
> This vulnerability existed before the Java upgrade and is outside the scope of this task. It is recommended to upgrade `org.postgresql:postgresql` to `42.7.x` or later in a separate task.

## Behavioral Impact Assessment

All code changes made during this upgrade are functionally equivalent:

- `Path.of(str)` and `Paths.get(str)` delegate to the same underlying `FileSystem` implementation — identical runtime behavior
- Import refactoring (wildcard → explicit) has no runtime impact

**No critical or major behavioral regressions were identified.**
