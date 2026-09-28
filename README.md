# VS Code + IntelliJ MCP Setup (Java & Spring Boot)

## Files Included
- **`.github/copilot-instructions.md`** & **`AGENTS.md`**: Always-on Principal Engineer directives for Java LTS, Spring Boot, and preferring IntelliJ MCP tools.
- **`.github/skills/intellij-spring-boot/SKILL.md`**: Agent skill for IntelliJ MCP incremental compilation, inspections, refactoring, JVM debugging (`xdebug_*`), and database introspection.
- **`.github/skills/java-springboot/SKILL.md`**: Spring Boot architecture, `@ConfigurationProperties`, REST controllers, JPA, validation, and exception handling best practices.
- **`.github/skills/spring-boot-testing/SKILL.md`** (+ `references/`): Complete Spring Boot slice testing guide (`@WebMvcTest`, `@DataJpaTest`, `@RestClientTest`, `MockMvcTester`, `@MockitoBean`, AssertJ, and Testcontainers).
- **`.vscode/mcp.json`**: Connects VS Code Agent Mode to IntelliJ IDEA's built-in MCP Server (`http://localhost:64342/sse`).

## Setup at Work
1. **Enable IntelliJ MCP Server:**
   - In IntelliJ IDEA, go to **Settings (`Ctrl+Alt+S`) > Tools > MCP Server** and check **Enable MCP Server**.
2. **Enable Agent Skills in VS Code:**
   - In VS Code `settings.json`, add:
     ```json
     "chat.useAgentSkills": true
     ```
3. **Apply to a Project or Globally:**
   - **Per-Project:** Copy `.github/`, `.vscode/`, and `AGENTS.md` into your repository root.
   - **Global (All Projects without committing to work repos):**
     - Copy `.github/skills/intellij-spring-boot` to `~/.copilot/skills/intellij-spring-boot`.
     - In VS Code (`Ctrl+Shift+P` -> **MCP: Open User Configuration**), paste the contents of `.vscode/mcp.json`.
     - In VS Code Settings, point `github.copilot.chat.codeGeneration.instructions` to `copilot-instructions.md`.
