Generate security under {basePackage}.security

COMMON RULES:
- Spring Security 6
- Stateless sessions
- OWASP headers
- /auth/** and /actuator/health permitted

JWT (if enabled):
- SecurityConfig
- JwtAuthenticationFilter
- JwtTokenProvider
- AuthenticationEntryPoint
- BCryptPasswordEncoder bean

OAuth (if enabled):
- OAuth2 resource server config

CSRF:
- Enabled/disabled from input

CONFIGURATION RULE:
- JWT secrets, expiry, issuer, and algorithms MUST be defined ONLY in application.properties
- DO NOT specify default values in Java code
- Use @Value or @ConfigurationProperties WITHOUT fallbacks

FAILURES:
- Return ApiResponse on auth errors

NO user entity
NO auth controller

