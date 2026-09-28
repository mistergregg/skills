---
name: intellij-spring-boot
description: >-
  Workflow for Java and Spring Boot development using the connected JetBrains IntelliJ IDEA MCP server (`jetbrains`).
  Activate this skill whenever working on Java, Kotlin, or Spring Boot projects to leverage IntelliJ's incremental compiler,
  AST inspections, symbol refactoring, JVM debugger (`xdebug_*`), run configurations, and built-in database tools.
---

# IntelliJ IDEA & Spring Boot Workflow

When working on Java or Spring Boot projects, prefer the `jetbrains` MCP server tools over raw shell commands or text-based regex replacements.

## 1. Always Pass `projectPath`
Every `jetbrains` MCP tool accepts a `projectPath` argument. Always pass the workspace/project root path as `projectPath` explicitly—especially when multiple IntelliJ windows are open—to avoid ambiguity errors.

## 2. Compilation, Diagnostics & Inspections
Instead of spawning cold Maven/Gradle processes for every syntax check:
- **Incremental Build:** Call `build_project` (optionally scoped to `paths`) to compile via IntelliJ's warm JPS/Gradle incremental compiler.
- **Inspect Errors & Warnings:** Call `get_file_problems` or `lint_files` to retrieve live compiler diagnostics, Spring bean wiring warnings, and static analysis inspections directly from IntelliJ's PSI index.

## 3. Navigation, Call Hierarchy & Safe Refactoring
- **Symbol Lookup:** Use `search_symbol` and `get_symbol_info` to inspect class signatures, Spring stereotypes, and library types (including decompiled bytecode in external JARs).
- **Call Hierarchy:** Use `analyze_calls` to trace callers/callees across controllers, services, and repositories before changing method contracts.
- **Renames:** Always use `rename_refactoring` when renaming classes, records, methods, or fields so IntelliJ updates all references, Spring annotations, and config properties safely.
- **Formatting:** Run `reformat_file` after edits to match the project's `.editorconfig` / IntelliJ code style.

## 4. Running Apps, JUnit Tests & JVM Debugging
- **Run Configurations:** Use `get_run_configurations` and `execute_run_configuration` to run Spring Boot services or JUnit test configurations configured in the IDE.
- **Live JVM Debugging (`xdebug_*`):** When diagnosing runtime failures or complex test state:
  1. Set breakpoints with `xdebug_set_breakpoint`.
  2. Start or attach via `xdebug_start_debugger_session`.
  3. Inspect stack frames (`xdebug_get_stack`, `xdebug_get_frame_values`) and evaluate expressions/bean state at runtime (`xdebug_evaluate_expression`).
  4. Step or resume using `xdebug_control_session` / `xdebug_run_to_line`.

## 5. Database & JPA Schema Inspection
Use IntelliJ's bundled Database MCP tools (`list_database_connections`, `list_database_schemas`, `introspect_schema`, `preview_table_data`, `execute_sql_query`) to verify table definitions, Flyway/Liquibase migrations, and query results before authoring JPA entities or `@Query` methods.
