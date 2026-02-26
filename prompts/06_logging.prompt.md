ROLE: LOGGING INFRASTRUCTURE ARCHITECT

OBJECTIVE:
Generate centralized, production-grade logging infrastructure under:
{basePackage}.logging

The logging system MUST provide:
- Consistent log format
- TraceId correlation
- Clean exception logging
- Zero business logic coupling

---

PACKAGE:
{basePackage}.logging

---

LOGGING FORMAT (MANDATORY):

Logs MUST follow this pattern:

yyyy-MM-dd HH:mm:ss,SSS LEVEL [thread]
logger-name -
exception-message (if any)

Example:
2025-01-14 10:22:45,103 ERROR [main]
com.example.service.DataProcessor -
java.lang.IndexOutOfBoundsException: Index 7 out of bounds for length 5

TraceId MUST be appended when present.

---

GENERATE THE FOLLOWING FILES (ALL REQUIRED):

---

1️⃣ TraceIdFilter.java

PURPOSE:
Ensure every request is associated with a unique traceId.

RESPONSIBILITIES:
- Generate a traceId if not present
- Propagate existing traceId from incoming headers
- Store traceId in MDC
- Make traceId available across the request lifecycle

RULES:
- Extend OncePerRequestFilter
- Header name: X-Trace-Id
- Use UUID when generating new traceId
- Clear MDC after request completion
- No logging inside filter
- JavaDocs required

---

2️⃣ LoggingConstants.java

PURPOSE:
Centralize logging-related constants.

FIELDS (EXAMPLES):
- TRACE_ID
- TRACE_HEADER
- LOG_PATTERN

RULES:
- final class
- private constructor
- public static final constants only
- JavaDocs required

---

3️⃣ LogbackConfiguration.java (or logback-spring.xml)

PURPOSE:
Define the logging configuration and format.

RESPONSIBILITIES:
- Configure log pattern exactly as specified
- Include traceId from MDC
- Enable structured, readable logs
- Configure log levels from input.md

RULES:
- SLF4J + Logback only
- No System.out usage
- No constructor logging
- No hard-coded environment assumptions
- JavaDocs or inline comments required

---

LOGGING BEHAVIOR RULES (CRITICAL):

- Application code logs ONLY via SLF4J Logger
- Exceptions MUST be logged using:
  log.error("Descriptive message", exception)
- Stacktrace MUST be printed automatically by logger
- Logging MUST NOT:
   - modify ApiResponse
   - depend on response module
   - depend on exception module

TraceId usage:
- Logging module owns MDC usage
- Other modules MAY read traceId from MDC
- No module except logging should manage MDC lifecycle

---

DEPENDENCIES (ALLOWED):

- SLF4J
- Spring Web
- MDC

DEPENDENCIES (FORBIDDEN):

- error
- exception
- response
- client
- cache
- security
- swagger
- business logic

---

QUALITY ENFORCEMENT:

- Lombok MAY be used if needed
- JavaDocs required for:
   - classes
   - methods
   - fields
- No TODOs
- No placeholders
- No unused imports
- Spring Boot 3 compatible
- Java 17+ compatible

OUTPUT:
Java source files and/or logging configuration files ONLY.
