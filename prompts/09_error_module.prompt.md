ROLE: ERROR MODULE ARCHITECT

OBJECTIVE:
Generate a centralized error policy module under:
{basePackage}.error

This module defines WHAT errors mean.
It MUST NOT handle exceptions or HTTP mechanics.

---

PACKAGE:
{basePackage}.error

---

GENERATE THE FOLLOWING FILES:

---

1) ErrorCode.java

PURPOSE:
Canonical list of error codes used across the platform.

RULES:
- Enum only
- No logic
- No dependencies

VALUES:
- SYSTEM_ERROR
- VALIDATION_ERROR
- DATABASE_ERROR
- NETWORK_ERROR
- UNAUTHORIZED
- FORBIDDEN

JavaDocs:
- Enum-level description
- JavaDoc for each value explaining usage

---

2) ErrorCategory.java

PURPOSE:
High-level classification of errors.

VALUES:
- SYSTEM
- VALIDATION
- DATABASE
- NETWORK
- SECURITY

RULES:
- Enum only
- No logic
- JavaDocs required

---

3) ErrorDefinition.java

PURPOSE:
Immutable definition describing an error.

FIELDS:
- ErrorCode errorCode
- ErrorCategory category
- String defaultMessage
- int httpStatus

RULES:
- Lombok:
    - @Data
    - @Builder
- No setters
- Immutable semantics
- JavaDocs for class and all fields

---

4) ErrorCatalog.java

PURPOSE:
Static registry mapping ErrorCode → ErrorDefinition.

RESPONSIBILITIES:
- Hold predefined ErrorDefinition objects
- Act as SINGLE SOURCE OF TRUTH

METHODS:
- ErrorDefinition get(ErrorCode errorCode)

RULES:
- Static, unmodifiable map
- Throw IllegalArgumentException for unknown codes
- No Spring annotations
- JavaDocs required

---

5) ErrorMapper.java

PURPOSE:
Utility for safely resolving ErrorDefinition.

METHODS:
- ErrorDefinition resolve(ErrorCode errorCode)

RULES:
- No logging
- No exception translation
- No Spring annotations
- Pure utility
- JavaDocs required

---

ARCHITECTURAL RULES (CRITICAL):

- error module MUST NOT depend on:
    - exception
    - response
    - logging
    - security
    - client
    - cache
    - swagger

- Other modules MAY depend on error.

- This module defines POLICY only.
- No HTTP handling.
- No exception handling.
- No business logic.

OUTPUT:
Java source files ONLY.
