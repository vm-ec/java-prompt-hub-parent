# Spring Boot Prompt Hub – Copilot Execution Guide

## Purpose

This repository contains a **Prompt Hub** used by **GitHub Copilot (or any LLM agent)** to generate a **single, production-ready Spring Boot project**.

The system is **prompt-driven**, **parameterized**, and **self-healing** (compile → fix → recompile).

Copilot MUST follow the instructions in this file exactly.

---

## Repository Structure (MANDATORY)

.
├── README.md # Execution instructions (this file)
├── input.md # User input (Spring Initializr equivalent)
└── prompts/ # All code-generation prompts
├── 00_system.prompt.md
├── 01_project_metadata.prompt.md
├── 02_orchestrator.prompt.md
├── 03_exception.prompt.md
├── 04_api_response.prompt.md
├── 05_security.prompt.md
├── 06_logging.prompt.md
├── 07_compile_and_fix.prompt.md
└── 08_output_contract.prompt.md


---

## Execution Model

Copilot MUST operate as an **orchestrated agent**, not as a chat assistant.

README.md → controls execution
input.md → provides configuration
prompts/ → contain generation logic


---

## Mandatory Execution Rules (NON-NEGOTIABLE)

Copilot MUST:

1. READ `README.md` first
2. READ `input.md` second
3. LOAD **ALL** prompts from `prompts/`
4. TREAT `input.md` as immutable
5. NOT assume defaults outside `input.md`
6. GENERATE **ONE single Spring Boot project**
7. NOT create multiple modules
8. NOT generate controllers, services, repositories, entities, or business DTOs
9. ENSURE the project compiles successfully
10. FIX compilation errors automatically if they occur

Failure to follow any rule is a **hard failure**.

---

## Step-by-Step Execution Flow

### STEP 1 – Read User Input

Copilot MUST parse `input.md` and extract:

- Build tool
- Java version
- Spring Boot version
- Project metadata
- Security configuration
- Logging configuration
- Build validation rules

`input.md` is the **single source of truth**.

---

### STEP 2 – Load System Constraints

Copilot MUST apply:

prompts/00_system.prompt.md


This establishes:
- Global architecture rules
- Allowed and forbidden generation
- Language and framework constraints

---

### STEP 3 – Orchestrate Project Assembly

Copilot MUST execute:
prompts/02_orchestrator.prompt.md

This guarantees:
- Single-project generation
- Correct folder structure
- Correct package layout
- Correct generation order

NO separate modules are allowed.

---

### STEP 4 – Generate Infrastructure Code

Copilot MUST apply prompts in **this exact order**:

1. `prompts/04_api_response.prompt.md`
2. `prompts/03_exception.prompt.md`
3. `prompts/05_security.prompt.md` (ONLY if enabled in `input.md`)
4. `prompts/06_logging.prompt.md`  (ONLY if enabled in `input.md`)

Rules:
- Each prompt generates COMPLETE Java files
- Package names MUST use `basePackage`
- No partial or placeholder code is allowed

---

### STEP 5 – Compile, Fix, and Recompile (CRITICAL)

Copilot MUST execute:
prompts/07_compile_and_fix.prompt.md

This requires Copilot to:

1. Run `mvn clean compile`
2. If compilation SUCCEEDS:
    - Stop immediately
3. If compilation FAILS:
    - Analyze compiler errors
    - Identify root cause
    - Fix ONLY compilation-related issues
    - Re-run compilation
4. Repeat until:
    - Build succeeds, OR
    - `maxRetry` from `input.md` is reached

Copilot MUST NOT:
- Change architecture
- Modify `input.md`
- Introduce new features

---

### STEP 6 – Enforce Output Contract

Before finalizing output, Copilot MUST enforce:

prompts/08_output_contract.prompt.md

This ensures:
- Java source files only
- No markdown or explanations
- No TODOs
- Project compiles successfully

---

## Expected Output

After successful execution, the repository will contain:

- A **single Spring Boot project**
- Application entry point
- Global exception handling
- Standard API response models
- Security infrastructure (if enabled)
- Logging and trace ID support (if enabled)

The project MUST build successfully using:

mvn clean compile

---

## Forbidden Actions

Copilot MUST NOT:

- Create multiple modules
- Skip build validation
- Leave compilation errors
- Modify `input.md`
- Generate domain/business code

---

## Verification Checklist (Copilot Self-Check)

Copilot MUST confirm ALL of the following before stopping:

- [ ] `input.md` was read and enforced
- [ ] All prompts were executed
- [ ] Single project structure exists
- [ ] No missing imports
- [ ] No compilation errors
- [ ] `mvn clean compile` succeeds

---

## Completion Criteria

Execution is considered **SUCCESSFUL** only when:

✔ All rules in this README are satisfied  
✔ The Spring Boot project compiles without errors

---

## Final Note

This README is an **execution contract**, not documentation.

Copilot MUST follow it **exactly as written**.

Any deviation is incorrect behavior.


