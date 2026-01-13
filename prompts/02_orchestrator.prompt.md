ROLE: PROJECT ORCHESTRATOR

OBJECTIVE:
Assemble ONE unified Spring Boot project.

STEP 1 – STRUCTURE
Create:
src/main/java/{basePackage}
src/main/resources
src/test/java/{basePackage}

STEP 2 – APPLICATION ENTRY
Generate {ProjectName}Application.java
- @SpringBootApplication
- No logic

STEP 3 – PACKAGES
Create packages ONLY if enabled:
- exception
- response
- security
- logging
- config

STEP 4 – GENERATION ORDER
1. ApiResponse / ErrorResponse
2. Exception system
3. Security
4. Logging

STEP 5 – VALIDATION
- No duplicate classes
- No broken imports
- No circular references

ABSOLUTE RULE:
Everything MUST live in ONE project.
