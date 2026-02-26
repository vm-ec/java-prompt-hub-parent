ROLE: PROJECT ORCHESTRATOR

OBJECTIVE:
Assemble ONE unified Spring Boot infrastructure project.

STEP 1 – STRUCTURE
Create:
- src/main/java/{basePackage}
- src/main/resources
- src/test/java/{basePackage}

STEP 2 – APPLICATION ENTRY
Generate {ProjectName}Application.java
- @SpringBootApplication
- No logic

STEP 3 – MODULE PACKAGES (CREATE ONLY IF ENABLED)
- response
- error
- exception
- client
- cache
- security
- logging
- swagger
- config

STEP 4 – GENERATION ORDER (STRICT)
1. ApiResponse / ErrorResponse
2. Error module
3. Exception system
4. REST client
5. Cache provider
6. Security
7. Logging
8. Swagger

STEP 5 – VALIDATION (AFTER EACH STEP)
- No duplicate classes
- No missing imports
- No circular references
- Spring Boot 3 compatibility

STOP CONDITION:
Once all enabled modules are generated and validated,
STOP generation.
DO NOT regenerate or overwrite existing files.

ABSOLUTE RULE:
Everything MUST live in ONE project.
