# Modernization Summary: 001-upgrade-java-version

## Task Description
Upgrade Java from version 17 to version 21 (LTS).

## Changes Made

### `pom.xml` (root/parent)
- Updated `<java.version>` property from `17` to `21`.

## Build & Test Results
- **Build**: SUCCESS
- **Unit Tests**: PASSED (1 test in `assets-manager-web`, 0 in `assets-manager-worker`)
- Java compiler now targets Java 21 (`javac [debug release 21]`)

## Notes
- No deprecated API or breaking changes were identified in the existing source code when upgrading from Java 17 to Java 21.
- The warning about dynamic agent loading (`byte-buddy-agent`) is a known JVM advisory for Java 21 and does not affect correctness. It can be suppressed by adding `-XX:+EnableDynamicAgentLoading` to JVM args if desired.
- Both `web` and `worker` modules compile and run successfully under Java 21.
