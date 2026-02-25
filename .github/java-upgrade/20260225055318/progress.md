# Upgrade Progress

  ### ✅ Generate Upgrade Plan
  - [[View Log]](logs\1.generatePlan.log)

  ### ✅ Confirm Upgrade Plan
  - [[View Log]](logs\2.confirmPlan.log)

  ### ✅ Setup Development Environment
  - [[View Log]](logs\3.setupEnvironment.log)
  
  > There are uncommitted changes in the project before upgrading, which have been stashed.

  ### ✅ PreCheck
  - [[View Log]](logs\4.precheck.log)
  
  <details>
      <summary>[ click to toggle details ]</summary>
  
  - ###
    ### ✅ Precheck - Build project
    - [[View Log]](logs\4.1.precheck-buildProject.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Command
    `mvnw clean test-compile -q -B -fn`
    </details>
  
    ### ✅ Precheck - Validate CVEs
    - [[View Log]](logs\4.2.precheck-validateCves.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### CVE issues
    - Dependency `org.postgresql:postgresql:42.6.0` has **1** known CVEs:
      - [CVE-2024-1597](https://github.com/advisories/GHSA-24rp-q3w6-vc56): org.postgresql:postgresql vulnerable to SQL Injection via line comment generation
        - **Severity**: **CRITICAL**
        - **Details**: # Impact
          SQL injection is possible when using the non-default connection property `preferQueryMode=simple` in combination with application code that has a vulnerable SQL that negates a parameter value.
          
          There is no vulnerability in the driver when using the default query mode. Users that do not override the query mode are not impacted.
          
          # Exploitation
          
          To exploit this behavior the following conditions must be met:
          
          1. A placeholder for a numeric value must be immediately preceded by a minus (i.e. `-`)
          1. There must be a second placeholder for a string value after the first placeholder on the same line. 
          1. Both parameters must be user controlled.
          
          The prior behavior of the driver when operating in simple query mode would inline the negative value of the first parameter and cause the resulting line to be treated as a `--` SQL comment. That would extend to the beginning of the next parameter and cause the quoting of that parameter to be consumed by the comment line. If that string parameter includes a newline, the resulting text would appear unescaped in the resulting SQL.
          
          When operating in the default extended query mode this would not be an issue as the parameter values are sent separately to the server. Only in simple query mode the parameter values are inlined into the executed SQL causing this issue.
          
          # Example
          
          ```java
          PreparedStatement stmt = conn.prepareStatement("SELECT -?, ?");
          stmt.setInt(1, -1);
          stmt.setString(2, "\nWHERE false --");
          ResultSet rs = stmt.executeQuery();
          ```
          
          The resulting SQL when operating in simple query mode would be:
          
          ```sql
          SELECT --1,'
          WHERE false --'
          ```
          
          The contents of the second parameter get injected into the command. Note how both the number of result columns and the WHERE clause of the command have changed. A more elaborate example could execute arbitrary other SQL commands.
          
          # Patch
          Problem will be patched upgrade to 42.7.2, 42.6.1, 42.5.5, 42.4.4, 42.3.9, 42.2.28, 42.2.28.jre7
          
          The patch fixes the inlining of parameters by forcing them all to be serialized as wrapped literals. The SQL in the prior example would be transformed into:
          
          ```sql
          SELECT -('-1'::int4), ('
          WHERE false --')
          ```
          
          # Workarounds
          Do not use the connection property`preferQueryMode=simple`. (*NOTE: If you do not explicitly specify a query mode then you are using the default of `extended` and are not impacted by this issue.*)
    - Dependency `org.postgresql:postgresql:42.6.0` has **1** known CVEs:
      - [CVE-2024-1597](https://github.com/advisories/GHSA-24rp-q3w6-vc56): org.postgresql:postgresql vulnerable to SQL Injection via line comment generation
        - **Severity**: **CRITICAL**
        - **Details**: # Impact
          SQL injection is possible when using the non-default connection property `preferQueryMode=simple` in combination with application code that has a vulnerable SQL that negates a parameter value.
          
          There is no vulnerability in the driver when using the default query mode. Users that do not override the query mode are not impacted.
          
          # Exploitation
          
          To exploit this behavior the following conditions must be met:
          
          1. A placeholder for a numeric value must be immediately preceded by a minus (i.e. `-`)
          1. There must be a second placeholder for a string value after the first placeholder on the same line. 
          1. Both parameters must be user controlled.
          
          The prior behavior of the driver when operating in simple query mode would inline the negative value of the first parameter and cause the resulting line to be treated as a `--` SQL comment. That would extend to the beginning of the next parameter and cause the quoting of that parameter to be consumed by the comment line. If that string parameter includes a newline, the resulting text would appear unescaped in the resulting SQL.
          
          When operating in the default extended query mode this would not be an issue as the parameter values are sent separately to the server. Only in simple query mode the parameter values are inlined into the executed SQL causing this issue.
          
          # Example
          
          ```java
          PreparedStatement stmt = conn.prepareStatement("SELECT -?, ?");
          stmt.setInt(1, -1);
          stmt.setString(2, "\nWHERE false --");
          ResultSet rs = stmt.executeQuery();
          ```
          
          The resulting SQL when operating in simple query mode would be:
          
          ```sql
          SELECT --1,'
          WHERE false --'
          ```
          
          The contents of the second parameter get injected into the command. Note how both the number of result columns and the WHERE clause of the command have changed. A more elaborate example could execute arbitrary other SQL commands.
          
          # Patch
          Problem will be patched upgrade to 42.7.2, 42.6.1, 42.5.5, 42.4.4, 42.3.9, 42.2.28, 42.2.28.jre7
          
          The patch fixes the inlining of parameters by forcing them all to be serialized as wrapped literals. The SQL in the prior example would be transformed into:
          
          ```sql
          SELECT -('-1'::int4), ('
          WHERE false --')
          ```
          
          # Workarounds
          Do not use the connection property`preferQueryMode=simple`. (*NOTE: If you do not explicitly specify a query mode then you are using the default of `extended` and are not impacted by this issue.*)
    </details>
  
    ### ✅ Precheck - Run tests
    - [[View Log]](logs\4.3.precheck-runTests.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Test result
    | Total | Passed | Failed | Skipped | Errors |
    |-------|--------|--------|---------|--------|
    | 1 | 1 | 0 | 0 | 0 |
    </details>
  </details>

  ### ✅ Upgrade project to use `Spring Boot 3.3.x`, `Java 21`
  
  
  <details>
      <summary>[ click to toggle details ]</summary>
  
  - ###
    ### ✅ Upgrade using Agent
    - [[View Log]](logs\5.1.upgradeProjectUsingAgent.log)
    
    - 8 files changed, 18 insertions(+), 17 deletions(-)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Code changes
    - Upgrade Java version to 21
      - Updated java.version property in pom.xml to 21
    - Upgrade Spring Boot to 3.3.13
      - Updated spring-boot-starter-parent version to 3.3.13
    </details>
  
    ### ✅ Build Project
    - [[View Log]](logs\5.2.buildProject.log)
    
    - Build result: 100% Java files compiled
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Command
    `mvnw clean test-compile -q -B -fn`
    </details>
  </details>

  ### ✅ Upgrade project to use `Spring Boot 3.4.x`
  
  
  <details>
      <summary>[ click to toggle details ]</summary>
  
  - ###
    ### ✅ Upgrade using Agent
    - [[View Log]](logs\6.1.upgradeProjectUsingAgent.log)
    
    - 1 file changed, 1 insertion(+), 1 deletion(-)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Code changes
    - Upgrade Spring Boot to 3.4.5
      - Updated spring-boot-starter-parent version from 3.3.13 to 3.4.5
    </details>
  
    ### ✅ Build Project
    - [[View Log]](logs\6.2.buildProject.log)
    
    - Build result: 100% Java files compiled
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Command
    `mvnw clean test-compile -q -B -fn`
    </details>
  </details>

  ### ✅ Validate & Fix
  
  
  <details>
      <summary>[ click to toggle details ]</summary>
  
  - ###
    ### ❗ Validate CVEs
    - [[View Log]](logs\7.1.validateCves.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Checked Dependencies
      - org.springframework.boot:spring-boot-starter-thymeleaf:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-web:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-amqp:3.4.5:jar
      - org.springframework.boot:spring-boot-devtools:3.4.5:jar
      - org.springframework.boot:spring-boot-configuration-processor:3.4.5:jar
      - org.projectlombok:lombok:1.18.38:jar
      - org.springframework.boot:spring-boot-starter-test:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-data-jpa:3.4.5:jar
      - org.postgresql:postgresql:42.7.5:jar
      - com.h2database:h2:2.3.232:jar
      - org.springframework.boot:spring-boot-starter:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-amqp:3.4.5:jar
      - org.projectlombok:lombok:1.18.38:jar
      - org.springframework.boot:spring-boot-starter-test:3.4.5:jar
      - com.fasterxml.jackson.core:jackson-databind:2.18.3:jar
      - org.springframework.boot:spring-boot-starter-data-jpa:3.4.5:jar
      - org.postgresql:postgresql:42.7.5:jar
      - java:*:21
    
    #### CVE issues
    - Dependency `org.postgresql:postgresql:42.7.5` has **1** known CVEs need to be fixed:
      - [CVE-2025-49146](https://github.com/advisories/GHSA-hq9p-pm7w-8p54): pgjdbc Client Allows Fallback to Insecure Authentication Despite channelBinding=require Configuration
        - **Severity**: **HIGH**
        - **Details**: ### Impact
          When the PostgreSQL JDBC driver is configured with channel binding set to `required` (default value is `prefer`), the driver would incorrectly allow connections to proceed with authentication methods that do not support channel binding (such as password, MD5, GSS, or SSPI  authentication). This could allow a man-in-the-middle attacker to intercept connections that users believed were protected by channel binding requirements.
          
          ### Patches
          TBD
          
          ### Workarounds
          
          Configure `sslMode=verify-full` to prevent MITM attacks.
          
          ### References
          
          * https://www.postgresql.org/docs/current/sasl-authentication.html#SASL-SCRAM-SHA-256
          * https://datatracker.ietf.org/doc/html/rfc7677
          * https://datatracker.ietf.org/doc/html/rfc5802
    - Dependency `org.postgresql:postgresql:42.7.5` has **1** known CVEs need to be fixed:
      - [CVE-2025-49146](https://github.com/advisories/GHSA-hq9p-pm7w-8p54): pgjdbc Client Allows Fallback to Insecure Authentication Despite channelBinding=require Configuration
        - **Severity**: **HIGH**
        - **Details**: ### Impact
          When the PostgreSQL JDBC driver is configured with channel binding set to `required` (default value is `prefer`), the driver would incorrectly allow connections to proceed with authentication methods that do not support channel binding (such as password, MD5, GSS, or SSPI  authentication). This could allow a man-in-the-middle attacker to intercept connections that users believed were protected by channel binding requirements.
          
          ### Patches
          TBD
          
          ### Workarounds
          
          Configure `sslMode=verify-full` to prevent MITM attacks.
          
          ### References
          
          * https://www.postgresql.org/docs/current/sasl-authentication.html#SASL-SCRAM-SHA-256
          * https://datatracker.ietf.org/doc/html/rfc7677
          * https://datatracker.ietf.org/doc/html/rfc5802
    </details>
  
    ### ✅ Fix CVE Issues
    - [[View Log]](logs\7.2.fixCveIssues.log)
    
    - 1 file changed, 1 insertion(+), 0 deletions(-)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Code changes
    - Fix CVE-2025-49146 in PostgreSQL JDBC driver
      - Upgraded org.postgresql:postgresql from 42.7.5 to 42.7.7
    </details>
  
    ### ✅ Build Project
    - [[View Log]](logs\7.3.buildProject.log)
    
    - Build result: 100% Java files compiled
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Command
    `mvnw clean test-compile -q -B -fn`
    </details>
  
    ### ✅ Validate CVEs
    - [[View Log]](logs\7.4.validateCves.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Checked Dependencies
      - org.springframework.boot:spring-boot-starter-thymeleaf:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-web:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-amqp:3.4.5:jar
      - org.springframework.boot:spring-boot-devtools:3.4.5:jar
      - org.springframework.boot:spring-boot-configuration-processor:3.4.5:jar
      - org.projectlombok:lombok:1.18.38:jar
      - org.springframework.boot:spring-boot-starter-test:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-data-jpa:3.4.5:jar
      - org.postgresql:postgresql:42.7.7:jar
      - com.h2database:h2:2.3.232:jar
      - org.springframework.boot:spring-boot-starter:3.4.5:jar
      - org.springframework.boot:spring-boot-starter-amqp:3.4.5:jar
      - org.projectlombok:lombok:1.18.38:jar
      - org.springframework.boot:spring-boot-starter-test:3.4.5:jar
      - com.fasterxml.jackson.core:jackson-databind:2.18.3:jar
      - org.springframework.boot:spring-boot-starter-data-jpa:3.4.5:jar
      - org.postgresql:postgresql:42.7.7:jar
      - java:*:21
    </details>
  
    ### ✅ Validate And Fix Code Behavior Changes
    - [[View Log]](logs\7.5.validateBehaviorChanges.log)
  
    ### ✅ Run Tests
    - [[View Log]](logs\7.6.runTests.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Test result
    | Total | Passed | Failed | Skipped | Errors |
    |-------|--------|--------|---------|--------|
    | 1 | 1 | 0 | 0 | 0 |
    </details>
  </details>

  ### ✅ Summarize Upgrade
  - [[View Log]](logs\8.summarizeUpgrade.log)