# Upgrade Plan

## Overview
Upgrade to the latest LTS versions: Java 21 and Spring Boot 3.4.

## Tasks
See `tasks.json` for detailed task breakdown.

### 001 - Upgrade Java and Spring Boot
- **Target Java**: 21 (LTS)
- **Target Spring Boot**: 3.4
- **Target Spring Framework**: 6.x
- Migrate `javax.*` to `jakarta.*` namespaces as required
- Update all related dependencies for compatibility
