ROLE: REST CLIENT INFRASTRUCTURE ARCHITECT

OBJECTIVE:
Generate a centralized, reusable REST client infrastructure under:
{basePackage}.client

This module MUST be the SINGLE way the application communicates
with external / third-party APIs.

Child code MUST NOT use WebClient or RestTemplate directly.

---

PACKAGE:
{basePackage}.client

---

PROGRAMMING MODEL DECISION (MANDATORY):

Read programmingModel.reactive from input.md.

IF programmingModel.reactive == true:
- Use Spring WebClient
- Implement a BLOCKING FACADE over the reactive client

IF programmingModel.reactive == false:
- Use RestTemplate
- Implement a STANDARD blocking client

ONLY ONE implementation MUST be generated.
DO NOT generate both.

---

TECHNOLOGY GUARANTEES:

- Spring Boot 3 compatible APIs ONLY
- Stateless and thread-safe design
- Synchronous API exposed to callers
- No reactive types exposed to child code

---

GENERATE THE FOLLOWING FILES (ALL REQUIRED):

---

1️⃣ ExternalRestClient.java

PURPOSE:
Public facade exposed to child modules for making external HTTP calls.

RESPONSIBILITIES:
- Provide simple, generic methods for ALL HTTP methods:
  - GET
  - POST
  - PUT
  - DELETE
  - PATCH
  - HEAD
  - OPTIONS
- Delegate execution to an internal executor
- Enforce consistent error handling, logging, and traceId propagation

METHODS (ALL REQUIRED):

- <T> T get(String url, Map<String,String> headers, Class<T> responseType)
- <T> T post(String url, Map<String,String> headers, Object body, Class<T> responseType)
- <T> T put(String url, Map<String,String> headers, Object body, Class<T> responseType)
- <T> T delete(String url, Map<String,String> headers, Class<T> responseType)
- <T> T patch(String url, Map<String,String> headers, Object body, Class<T> responseType)
- <T> T head(String url, Map<String,String> headers, Class<T> responseType)
- <T> T options(String url, Map<String,String> headers, Class<T> responseType)

RULES:
- Lombok @RequiredArgsConstructor ONLY
- DO NOT generate explicit constructors
- No WebClient or RestTemplate logic inside this class
- No try/catch except for exception translation
- JavaDocs required for class and all methods

---

2️⃣ HttpMethodExecutor.java (or Executor implementation)

PURPOSE:
Internal executor that performs actual HTTP calls.

RESPONSIBILITIES:
- Build HTTP requests
- Attach headers
- Serialize request bodies
- Deserialize responses
- Handle HTTP status codes
- Convert failures into ApiException using ErrorCode

CORE METHOD (MANDATORY):

<T> T execute(
    HttpMethod method,
    String url,
    Map<String,String> headers,
    Object body,
    Class<T> responseType
)

ERROR MAPPING (MANDATORY):
- 4xx → VALIDATION_ERROR / UNAUTHORIZED / FORBIDDEN
- 5xx → SYSTEM_ERROR
- IO / timeout → NETWORK_ERROR

RULES:
- Package-private visibility
- No direct exposure to child code
- No duplicated logic
- JavaDocs required

---

3️⃣ RestClientConfig.java

PURPOSE:
Spring configuration for REST client.

RESPONSIBILITIES:
- Configure WebClient OR RestTemplate based on programmingModel.reactive
- Configure timeouts (connect / read)
- Configure codecs / message converters
- Configure default headers

RULES:
- @Configuration class
- NO hard-coded values
- ALL values MUST come from application.properties
- No default values in Java code
- JavaDocs required

---

4️⃣ ExternalCallExceptionTranslator.java

PURPOSE:
Translate low-level client exceptions into ApiException.

RESPONSIBILITIES:
- Centralize exception translation
- Map low-level exceptions to ErrorCode
- Preserve original cause

RULES:
- Pure utility
- No logging
- No Spring annotations
- JavaDocs required

---

DEPENDENCIES (ALLOWED):

- error module
- exception module
- response module (ApiResponse only if required)
- logging module (traceId via MDC)

DEPENDENCIES (FORBIDDEN):

- security
- cache
- swagger
- business logic

---

ARCHITECTURAL RULES (CRITICAL):

- Child code MUST ONLY interact with ExternalRestClient
- Underlying client MUST NOT be exposed
- All methods MUST be synchronous from caller perspective
- All failures MUST be translated to ApiException with ErrorCode
- TraceId MUST be propagated via headers if present in MDC

---

QUALITY ENFORCEMENT:

- Lombok usage mandatory
- NO getters / setters / explicit constructors
- JavaDocs for classes, methods, and parameters
- No TODOs
- No placeholders
- No unused imports
- Spring Boot 3 compatible APIs only

OUTPUT:
Java source files ONLY.
