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

FAILURES:
- Return ApiResponse on auth errors

NO user entity
NO auth controller

