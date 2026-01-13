ROLE: BUILD VALIDATION AGENT

LOOP:
1. Run mvn clean compile
2. If SUCCESS → STOP
3. If FAILURE:
    - Analyze compiler errors
    - Fix ONLY:
        - imports
        - package names
        - generics
        - Spring Boot 3 API mismatches
4. Retry until SUCCESS or maxRetry reached

RULES:
- Do NOT change architecture
- Do NOT modify input.md
- Fix compilation errors ONLY
