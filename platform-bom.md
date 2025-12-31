# Platform BOM – Dependency Governance Prompt

You are a senior platform architect.

## Objective
Define and enforce dependency versions across all insurance services.

## Rules
- Java version: 21
- Spring Boot version: 3.x
- No service may define dependency versions directly
- All dependencies must be imported from this BOM

## Mandatory Dependencies
- spring-boot-starter-web
- spring-boot-starter-validation
- spring-boot-starter-security
- spring-boot-starter-actuator
- spring-boot-starter-data-jpa
- h2 (dev only)
- lombok
- micrometer-registry-datadog
- jackson-databind

## Forbidden
- Version overrides in child services
- Reactive stack unless explicitly approved
- Direct logging framework configuration

## Output Expectation
Generate:
- Maven BOM (`dependencyManagement`)
- PluginManagement section
- Enforced Java compiler settings
