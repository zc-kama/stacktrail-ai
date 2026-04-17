# StackTrail

Trace the stack. Ship the change.

StackTrail is a portable AI development workflow for real application projects. It helps coding agents act like execution developers: read the project memory, trace the path through the stack, make the smallest complete change, verify the touched layers, and record durable project facts.

It is designed for full-stack and production-shaped work where a request may cross UI components, API clients, controllers, DTOs, services, repositories or mappers, database tables, files, logs, environment config, and deployment.

## Why StackTrail

Most AI coding failures start the same way: the agent edits the visible file without tracing the actual project path.

StackTrail fixes that habit:

```text
UI/component
 -> API/client helper
 -> route/controller
 -> request DTO/schema
 -> service/use-case
 -> repository/mapper/storage
 -> response DTO/schema
 -> UI state
```

The goal is not more ceremony. The goal is fewer broken contracts, fewer guessed deployment fixes, and more changes that actually run.

## What Is Included

- `skills/stacktrail/` - Codex skill version.
- `prompts/universal.md` - tool-agnostic prompt.
- `prompts/claude-code.md` - Claude Code / `CLAUDE.md` version.
- `prompts/openclaw.md` - OpenClaw and generic coding-agent version.
- `docs/name-research.md` - short notes on the name choice.

## Install For Codex

Copy the skill folder into your Codex skills directory:

```bash
cp -R skills/stacktrail ~/.codex/skills/stacktrail
```

On Windows PowerShell:

```powershell
Copy-Item -Recurse .\skills\stacktrail "$env:USERPROFILE\.codex\skills\stacktrail"
```

Then invoke it:

```text
Use $stacktrail to implement, verify, and document this project change end to end.
```

## Use With Other Agents

Paste one of the prompt variants into the relevant project instruction file:

- Claude Code: `prompts/claude-code.md` into `CLAUDE.md`
- OpenClaw: `prompts/openclaw.md`
- Other tools: `prompts/universal.md`

## Core Rules

- Read project memory and current code before deciding.
- Classify the request and affected layer.
- Trace cross-layer features end to end before editing.
- Preserve existing contracts unless redesign is explicit.
- Implement the smallest complete solution.
- Verify by the layers touched.
- Update durable project memory when facts change.

## License

MIT
