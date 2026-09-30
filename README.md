# claude-serena-skill

Claude Code skill for [Serena MCP](https://github.com/oraios/serena) — code intelligence for precise symbol lookup, semantic reference tracking, and surgical code edits.

Invoke with `/serena` or by saying **「使用serena掃描專案」**. The skill acts as an agent: it detects your current environment, installs what's missing, and gets Serena running — no manual configuration needed.

---

## Installation patterns

### A. New project (use as template)

```bash
git clone https://github.com/JHcool-CSC/claude-serena-skill.git .
```

Then open the project in Claude Code and say `/serena`. The skill will:
1. Check if `serena.exe` is installed
2. Auto-create `.mcp.json` with the correct paths
3. Tell you to restart Claude Code
4. After restart, auto-run onboarding to index your codebase

### B. Existing project (skill drop-in)

Copy the skill directory into your project:

```bash
cp -r .claude/skills/tools/serena /your-project/.claude/skills/tools/serena
```

Open the project in Claude Code and say `/serena` or **「使用serena掃描專案」**. Same auto-setup flow as above.

---

## What the skill does automatically

| Condition | Action |
|-----------|--------|
| `serena.exe` not found | Tells you to install (`uv tool install ...`) |
| `.mcp.json` missing/incomplete | Auto-creates or updates it with correct paths |
| MCP not connected this session | Tells you to restart Claude Code |
| No `.serena/` directory | Auto-runs `onboarding` to index the codebase |
| Everything ready | Proceeds directly to your code task |

---

## Prerequisites

- [Claude Code](https://claude.com/claude-code)
- [uv](https://github.com/astral-sh/uv) (`winget install astral-sh.uv` or `pip install uv`)

Serena itself is installed automatically by the skill (via `uv tool install`).

---

## Files

```
.claude/
  skills/
    tools/
      serena/
        SKILL.md          ← the skill (entry point for everything)
.mcp.json.example         ← reference for manual configuration
.gitignore                ← excludes .mcp.json and .serena/
```

`.mcp.json` and `.serena/` are gitignored because they contain machine-specific paths and auto-generated index data.
