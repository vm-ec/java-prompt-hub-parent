ROLE: SWAGGER / OPENAPI INFRASTRUCTURE ARCHITECT

OBJECTIVE:
Generate Swagger / OpenAPI infrastructure under:
{basePackage}.swagger

This module provides OpenAPI documentation configuration for the application.
It MUST NOT define or depend on any controller implementations.

---

PACKAGE:
{basePackage}.swagger

---

TECHNOLOGY:
- springdoc-openapi (Spring Boot 3 compatible)
- OpenAPI 3 specification

---

GENERATE THE FOLLOWING FILES (ALL REQUIRED):

---

1️⃣ OpenApiConfig.java

PURPOSE:
Central configuration for OpenAPI / Swagger documentation.

RESPONSIBILITIES:
- Define OpenAPI bean
- Configure API metadata:
    - title
    - description
    - version
- Group APIs under a default group
- Enable Swagger UI automatically

CONFIGURATION DETAILS:
- Title → use metadata.name from input.md
- Description → use metadata.description from input.md
- Version → use api.version from input.md

RULES:
- @Configuration class
- Define @Bean of type OpenAPI
- Do NOT reference controllers directly
- Do NOT hardcode environment-specific values
- JavaDocs required for class and all methods

---

2️⃣ SwaggerConstants.java

PURPOSE:
Centralize Swagger-related constants.

FIELDS (EXAMPLES):
- DEFAULT_GROUP_NAME
- API_TITLE
- API_DESCRIPTION
- API_VERSION

RULES:
- final class
- private constructor
- public static final constants only
- JavaDocs required for class and each constant

---

ARCHITECTURAL RULES (CRITICAL):

- Swagger module MUST NOT depend on:
    - client
    - cache
    - security
    - logging
    - exception
    - error
    - response

- Other modules MAY remain completely unaware of Swagger.

- This module MUST be:
    - Passive
    - Infra-only
    - Safe when no controllers exist

---

QUALITY ENFORCEMENT:

- No TODOs
- No placeholders
- No unused imports
- Spring Boot 3 compatible
- Java 17+ compatible
- JavaDocs on:
    - classes
    - methods
    - fields

OUTPUT:
Java source files ONLY.
