Generate exception infrastructure under:
{basePackage}.exception

GENERATE:

1. ApiException extends RuntimeException
    - errorCode
    - message
    - HttpStatus

2. ErrorCode enum:
   SYSTEM_ERROR
   VALIDATION_ERROR
   DATABASE_ERROR
   NETWORK_ERROR
   UNAUTHORIZED
   FORBIDDEN

3. Common Exceptions:
    - DatabaseException
    - NetworkException
    - ServiceException
    - ValidationException

4. GlobalExceptionHandler
    - @RestControllerAdvice
    - Handles:
      MethodArgumentNotValidException
      ApiException
      AccessDeniedException
      Exception
    - Always returns ApiResponse

RULES:
- No business logic
- Centralized handling only
