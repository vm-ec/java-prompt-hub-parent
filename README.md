# Insurance Platform – Parent Prompt Library

## Purpose
This repository is a **centralized prompt hub** for building an enterprise-grade Insurance Platform
using Java 21 and Spring Boot 3.x.

It defines:
- Platform-wide architectural standards
- Dependency governance
- Security, observability, audit, and compliance rules
- Reusable common modules
- Copilot Agent–ready prompts for consistent code generation

## Usage with GitHub Copilot Agent
Each `prompt.md` file represents a **module-level instruction**.
Copilot Agent must:
- Read the relevant prompt
- Generate code ONLY within that module’s responsibility
- Never duplicate logic across modules
- Always comply with platform-bom constraints

## Non-Goals
- This repository does NOT contain application code
- This repository does NOT contain generated outputs
- This repository defines **HOW code must be generated**

## Target Stack
- Java 21
- Spring Boot 3.x
- Maven (BOM-driven)
- H2 (local/dev)
- PostgreSQL (future)
- REST-first architecture
- Event-ready design
