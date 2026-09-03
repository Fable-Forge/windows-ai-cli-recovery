---
name: windows-ai-cli-recovery
description: Use when diagnosing Windows AI CLI or app problems for Codex, Claude Code, npm-installed CLIs, PowerShell command lookup, PATH, execution policy, proxy env files, reconnect loops, Codex Desktop status messages, missing claude/codex commands, WindowsApps or sandbox popups, or verifying local .codex/.claude skills and config on this machine.
---

# Windows AI CLI Recovery

## Overview

Use this skill to restore the simple command the user expects, such as `codex` or `claude`, on Windows PowerShell. Verify the current machine state first, then apply the smallest reversible fix.

For concrete command patterns and decision points, read `references/windows-cli-checks.md` when the task involves PATH, npm global bin, proxy ports, PowerShell profiles, execution policy, or Codex Desktop state.

## Safety Rules

- Prefer read-only checks before edits.
- Do not expose secrets from config files.
- When reading `.env`, show only proxy endpoints or non-secret settings that are needed for the task.
- Before editing profile, PATH, or config files, explain the exact file or setting being changed.
- Preserve the user's preferred command shape when possible. If they want to type `claude`, restore `claude`, not a long command they must memorize.

## Workflow

1. Classify the failure.
   - Command not found: inspect command lookup, npm global bin, PATH, and installed files.
   - PowerShell script blocked: check whether `.cmd` works while `.ps1` is blocked.
   - Reconnect/proxy issue: inspect local proxy listener and Codex `.env`.
   - Codex Desktop message: explain whether it is app state, context compression, review UI, or project file state.

2. Verify current state with narrow commands.
   - Use `Get-Command <name> -All`.
   - Use `npm config get prefix` and inspect the npm global bin directory.
   - Use `Get-Item` / `Test-Path` for expected `.cmd` files.
   - Use `Get-NetTCPConnection` only for local proxy port discovery.

3. Choose the smallest fix.
   - Add the npm global directory to the user PATH when the executable exists but cannot be found.
   - Prefer `<tool>.cmd` when `.ps1` is blocked.
   - Add a PowerShell profile function only when the user explicitly wants the bare command and PATH/execution policy alone does not restore it.
   - For Codex proxy, write or verify `C:\Users\<user>\.codex\.env` only after confirming the local proxy port.

4. Verify the restored workflow.
   - Run the exact command the user wants, such as `claude --version` or `codex --version`.
   - If a new shell is required, provide the one-line temporary PATH refresh and the permanent explanation.

## Output Expectations

End with:

- root cause in one or two sentences
- exact setting or file changed, if any
- verified command output or remaining blocker
- the shortest command the user should use next

## Known Patterns

- npm global CLIs on Windows often install to `%APPDATA%\npm` as `.cmd` and `.ps1` shims.
- PowerShell may block `.ps1` shims while `.cmd` works.
- A new PowerShell window may be required after changing user PATH.
- Codex proxy config belongs in `C:\Users\<user>\.codex\.env` with `HTTP_PROXY` and `HTTPS_PROXY`.
- A Codex "complete content failed to load" review message can be a UI/diff loading problem, not proof that edited files are broken.
- "Automatic context compression" means the app is summarizing a long thread so work can continue; it is not by itself a failure.
