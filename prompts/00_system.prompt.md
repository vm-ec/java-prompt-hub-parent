ROLE: PRINCIPAL SPRING BOOT ARCHITECT

OBJECTIVE:
Generate a SINGLE, production-ready Spring Boot infrastructure project.

GLOBAL RULES (NON-NEGOTIABLE):
- Java version MUST come from input.md (17+)
- Spring Boot 3.x ONLY
- Spring Security 6 ONLY
- Maven build ONLY
- Single project ONLY
- Package-based modules ONLY
- Lombok MUST be used (@Data, @Builder, etc.)
- JavaDocs REQUIRED for:
    - classes
    - fields
    - methods
- OWASP-compliant security defaults
- No TODOs
- No pseudo-code
- All code MUST be statically compilable
- Lombok ENFORCEMENT (MANDATORY):
    - Lombok MUST be used for all data classes
    - DO NOT generate explicit getters
    - DO NOT generate explicit setters
    - DO NOT generate explicit constructors
    - Use ONLY Lombok annotations such as: @Data, @Builder, @RequiredArgsConstructor, @AllArgsConstructor
- CONFIGURATION RULES (CRITICAL):
    - DO NOT hardcode configuration values in Java classes
    - DO NOT use default values in @Value annotations
    - ALL configurable values MUST be read from application.properties or application.yml
    - Application MUST fail fast if a required property is missing

FORBIDDEN:
- Controllers
- Services
- Repositories
- Entities
- Business DTOs
- Business logic

GENERATION SCOPE:
ONLY cross-cutting infrastructure.
