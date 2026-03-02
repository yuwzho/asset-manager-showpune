# Modernization Summary: Upgrade Java 21 & Spring Boot 3.4

**Task ID**: 001-upgrade-java-spring-boot  
**Working Branch**: `appmod/java-upgrade-20260302024357`  
**Date**: 2026-03-02  

---

## Overview

This task upgraded the **asset-manager** multi-module Maven project from Java 17 + Spring Boot 3.2.1 to **Java 21 + Spring Boot 3.4.5**, fixing a HIGH-severity CVE in the PostgreSQL driver along the way.

---

## Upgrade Goals

| Component | Before | After |
|-----------|--------|-------|
| Java (JDK) | 17 | **21** |
| Spring Boot | 3.2.1 | **3.4.5** |
| Spring Framework | 6.1.x (managed) | **6.2.x (managed)** |

---

## What Changed

### 1. Root `pom.xml`

| Change | Details |
|--------|---------|
| `spring-boot-starter-parent` version | `3.2.1` → `3.4.5` |
| `java.version` property | `17` → `21` |
| `postgresql.version` override | *(new)* `42.7.7` (overrides BOM-managed `42.7.5` to fix CVE) |

### 2. Dependency Upgrades (transitively via Spring Boot BOM)

| Dependency | Before | After |
|------------|--------|-------|
| `org.springframework.boot:*` | 3.2.1 | 3.4.5 |
| `org.postgresql:postgresql` | 42.6.0 | 42.7.7 |
| `com.h2database:h2` | 2.2.224 | 2.3.232 |
| `org.projectlombok:lombok` | 1.18.30 | 1.18.38 |
| `com.fasterxml.jackson.core:jackson-databind` | 2.15.3 | 2.18.3 |

### 3. Code Changes (Applied via OpenRewrite)

OpenRewrite recipes `UpgradeSpringBoot_3_3` and `UpgradeToJava21` were applied and produced the following minor, behavior-preserving changes:

| File | Change | Severity |
|------|--------|----------|
| `web/.../config/AwsS3Config.java` | Removed redundant `public` on `@Bean` method | Minor |
| `web/.../config/RabbitConfig.java` | Removed redundant `public` on `@Bean` methods | Minor |
| `web/.../controller/S3Controller.java` | `@RequestParam("file")` → `@RequestParam` (name inferred from param) | Minor |
| `web/.../service/LocalFileStorageService.java` | `Paths.get(…)` → `Path.of(…)`; wildcard import → explicit imports | Minor |
| `worker/.../config/AwsS3Config.java` | Removed redundant `public` on `@Bean` method | Minor |
| `worker/.../config/RabbitConfig.java` | Removed redundant `public` on `@Bean` methods | Minor |
| `worker/.../service/LocalFileProcessingService.java` | `Paths.get(…)` → `Path.of(…)`; removed unused `Paths` import | Minor |

> All code changes are functionally equivalent. No behavioral changes were introduced.

---

## Security Fixes

| CVE | Dependency | Severity | Fix |
|-----|------------|----------|-----|
| [CVE-2025-49146](https://github.com/advisories/GHSA-hq9p-pm7w-8p54) | `org.postgresql:postgresql` | **HIGH** | Upgraded from `42.7.5` → `42.7.7` via `postgresql.version` property override in root `pom.xml` |

---

## Jakarta Migration

No Jakarta EE namespace migration (`javax.*` → `jakarta.*`) was required. The project was already using Spring Boot 3.x (Jakarta EE 10 based) and had no legacy `javax.persistence.*` or `javax.servlet.*` imports. The only `javax.*` usage (`javax.imageio.*`) is part of the Java SE standard library and does **not** need migration.

---

## Build & Test Results

| | Before | After |
|-|--------|-------|
| Build status | ✅ Passing | ✅ Passing |
| Unit tests | 1 passed, 0 failed | 1 passed, 0 failed |
| Integration tests | N/A | N/A |

---

## Upgrade Milestones

The upgrade was executed in two milestones to reduce risk:

1. **Milestone 1** – Upgrade to Spring Boot 3.3.x + Java 21 (via OpenRewrite `UpgradeSpringBoot_3_3` + `UpgradeToJava21` recipes)
2. **Milestone 2** – Upgrade to Spring Boot 3.4.5 (manual `pom.xml` version bump)

### Commits

| Commit | Message |
|--------|---------|
| `28a2333` | Apply OpenRewrite recipes for Spring Boot 3.3 and Java 21 upgrade |
| `58f1a65` | Upgrade Spring Boot to 3.4.5 |
| `460cead` | Upgrade postgresql to 42.7.7 to fix CVE-2025-49146 |
| `c975967` | fix issues |

---

## Success Criteria

| Criterion | Status |
|-----------|--------|
| `passBuild` | ✅ Pass |
| `passUnitTests` | ✅ Pass |
| `generateNewUnitTests` | N/A (not required) |
| `generateNewIntegrationTests` | N/A (not required) |
| `passIntegrationTests` | N/A (not required) |
| `securityComplianceCheck` | N/A (not required) |
