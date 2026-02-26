# Spring Boot Project Input Specification

All project generation MUST be driven ONLY by this file.

---

## 1. Project Configuration

project:
    buildTool: Maven                  # Maven | Gradle
    packaging: Jar                    # Jar | War | POM
    language: Java                    # Java | Kotlin | Groovy

---

## 2. Spring Boot Configuration

springBoot:
    version: 3.5.9
    configurationType: properties     # properties | yaml

---

## 3. Java Configuration

java:
version: 21                       # 17 | 21 | 25

---

## 4. Project Metadata

metadata:
group: com.example
artifact: demo
name: demo
description: Demo project for Spring Boot
basePackage: com.example.demo

---

## 5. Dependencies

dependencies:
selected: []                      # example: spring-web, spring-security

---

## 6. Security Configuration

security:
enabled: true
type: jwt                         # jwt | oauth | both | none
enableCsrf: false

---

## 7. API Configuration

api:
version: v1

---

## 8. Logging Configuration

logging:
enabled: true
includeTraceId: true
level: INFO                       # TRACE | DEBUG | INFO | WARN | ERROR

---

## 9. Programming Model

programmingModel:
  reactive: true   # true = WebClient, false = RestTemplate

---

## 10. Exception Configuration

exceptions:
enableGlobalHandler: true
includeCommonExceptions: true

---

## 11. Build Validation

buildValidation:
autoCompile: true
autoFix: true
maxRetry: 5

---

## RULES

- Do NOT assume defaults outside this file
- Generate ONE single Spring Boot project
- Generated code MUST compile
