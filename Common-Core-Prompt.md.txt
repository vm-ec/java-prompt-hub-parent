# Common Core Prompt

## Responsibility
Provide foundational abstractions shared across all services.

## Includes
- BaseEntity (id, createdAt, updatedAt)
- BaseResponse
- Pagination models
- Common constants
- ApplicationContext holder

## Rules
- No business logic
- No REST
- No persistence queries
- Must be dependency-free (except Lombok)

## Output
Generate Java classes under:
com.platform.common.core
