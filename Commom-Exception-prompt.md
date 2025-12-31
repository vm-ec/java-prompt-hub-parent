# Common Exception Prompt

## Responsibility
Centralized exception framework.

## Includes
- BasePlatformException
- BusinessException
- TechnicalException
- ErrorCode enum
- Global error response structure

## Rules
- No controller advice here
- Exceptions must be immutable
- Error codes must be hierarchical

## Output
Exception classes under:
com.platform.common.exception
