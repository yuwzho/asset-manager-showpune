# Upgrade Progress

  ### ✅ Generate Upgrade Plan
  - [[View Log]](logs\1.generatePlan.log)

  ### ✅ Confirm Upgrade Plan
  - [[View Log]](logs\2.confirmPlan.log)

  ### ✅ Setup Development Environment
  - [[View Log]](logs\3.setupEnvironment.log)

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

  ### ✅ Upgrade project to use `Java 21`
  
  
  <details>
      <summary>[ click to toggle details ]</summary>
  
  - ###
    ### ✅ Upgrade using Agent
    - [[View Log]](logs\5.1.upgradeProjectUsingAgent.log)
    
    - 3 files changed, 6 insertions(+), 5 deletions(-)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Code changes
    - Upgrade Java version to 21
      - Updated java.version property in parent pom.xml to 21
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

  ### ✅ Validate & Fix
  
  
  <details>
      <summary>[ click to toggle details ]</summary>
  
  - ###
    ### ✅ Validate CVEs
    - [[View Log]](logs\6.1.validateCves.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Checked Dependencies
      - java:*:21
    </details>
  
    ### ✅ Validate And Fix Code Behavior Changes
    - [[View Log]](logs\6.2.validateBehaviorChanges.log)
  
    ### ✅ Run Tests
    - [[View Log]](logs\6.3.runTests.log)
    
    <details>
        <summary>[ click to toggle details ]</summary>
    
    #### Test result
    | Total | Passed | Failed | Skipped | Errors |
    |-------|--------|--------|---------|--------|
    | 1 | 1 | 0 | 0 | 0 |
    </details>
  </details>

  ### ✅ Summarize Upgrade
  - [[View Log]](logs\7.summarizeUpgrade.log)