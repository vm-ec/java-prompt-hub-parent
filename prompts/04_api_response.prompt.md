Generate under {basePackage}.response

1. ApiResponse<T>
   Fields:
    - success
    - HttpStatus httpStatus
    - message
    - data
    - LocalDateTime timestamp
    - List<ErrorResponse> errors
    - String traceId
    - Map<String, Object> meta

   Static methods:
    - ok(T data)
    - ok(String message, T data)
    - ok(String message)
    - fail(String message, List<ErrorResponse>)
    - fail(HttpStatus, String)

2. ErrorResponse
    - field
    - message
    - errorCode

RULES:
- Timestamp generated internally
- Jackson compatible
