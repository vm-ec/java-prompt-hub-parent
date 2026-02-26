ROLE: EXCEPTION INFRASTRUCTURE ARCHITECT

OBJECTIVE:
Generate centralized exception handling infrastructure under:
{basePackage}.exception

This module defines HOW errors are raised and handled.
It MUST rely on the error module for error semantics.

---

PACKAGE:
{basePackage}.exception

---

DEPENDENCIES (MANDATORY):
- {basePackage}.error

---

GENERATE THE FOLLOWING FILES:

---

1) ApiException.java

PURPOSE:
Base runtime exception for all application-level failures.

FIELDS:
- ErrorCode errorCode
- String overrideMessage (optional)
- Throwable cause

RULES:
- Extends RuntimeException
- Lombok:
   - @Getter
- Does NOT define HTTP status
- Does NOT define default messages
- JavaDocs required

---

2) Specific Exceptions

PURPOSE:
Typed exceptions representing technical failure categories.

GENERATE:
- ValidationException → VALIDATION_ERROR
- DatabaseException → DATABASE_ERROR
- NetworkException → NETWORK_ERROR
- ServiceException → SYSTEM_ERROR

RULES:
- Each extends ApiException
- Each sets the correct ErrorCode
- No additional logic
- JavaDocs required

---

3) GlobalExceptionHandler.java

PURPOSE:
Centralized REST exception handling.

RESPONSIBILITIES:
- Catch framework and application exceptions
- Resolve ErrorDefinition using ErrorMapper
- Build standardized ApiResponse.fail(...)
- Set HTTP status from ErrorDefinition

HANDLE:
- MethodArgumentNotValidException
- ApiException
- AccessDeniedException
- Exception (fallback)

RULES:
- @RestControllerAdvice
- MUST NOT create new ErrorCodes
- MUST NOT hardcode HTTP status or messages
- ALWAYS delegate error meaning to error module
- JavaDocs required

---

ARCHITECTURAL RULES (CRITICAL):

- exception module MUST NOT define:
   - error semantics
   - HTTP status mappings
   - error categories

- exception module MAY depend on:
   - error
   - response
   - logging (for logging exceptions)

- exception module MUST NOT depend on:
   - client
   - cache
   - swagger
   - business logic

- No business logic allowed.

OUTPUT:
Java source files ONLY.
