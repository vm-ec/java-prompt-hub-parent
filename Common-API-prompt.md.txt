# Common API Prompt

## Responsibility
Define API standards across the platform.

## Includes
- Standard API response wrapper
- API error model
- API versioning constants
- Correlation ID handling

## Rules
- No Spring annotations except @JsonProperty
- DTOs MUST NOT contain validation annotations
- DTOs MUST include @JsonIgnore where fields are internal

## Output
Generate shared API DTOs usable by all services
