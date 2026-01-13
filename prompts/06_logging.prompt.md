Generate logging under {basePackage}.logging

GENERATE:

1. TraceIdFilter
    - OncePerRequestFilter
    - Generate or propagate traceId
    - Store in MDC
    - Attach to ApiResponse

2. Logging configuration
    - SLF4J
    - Structured logs
    - Include traceId

RULES:
- No System.out
- No constructor logging
