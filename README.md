[English](README.md) | [简体中文](README.zh-CN.md)

<div align="center">

# ⚒️ Windows AI CLI Recovery

**Diagnose and recover Codex, Claude Code, and npm AI CLI failures on Windows.**

> 诊断并恢复 Windows 上 Codex、Claude Code 与 npm AI CLI 的安装和连接问题。

<p>
  <a href="https://github.com/Fable-Forge/windows-ai-cli-recovery/blob/main/LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-0969da"></a>
  <img alt="Maturity: beta" src="https://img.shields.io/badge/maturity-beta-8250df">
  <img alt="Agents: Codex and Claude Code" src="https://img.shields.io/badge/agents-Codex_%C2%B7_Claude_Code-1f883d">
</p>

</div>

**[Use cases](#use-cases) · [Quick install](#quick-install) · [Compatibility](#compatibility) · [Validation](#validation) · [Contact](#contact)**

---

<a id="use-cases"></a>
## When to use it

Ask your Agent to load this repository's `SKILL.md` when your task matches the outcome above. `SKILL.md` is the authority for triggers, boundaries, and the complete workflow.

<a id="quick-install"></a>
## Quick install

Give this instruction to an Agent with command-line access:

```text
Install windows-ai-cli-recovery: https://raw.githubusercontent.com/Fable-Forge/windows-ai-cli-recovery/main/docs/install.md
```

Or use the Agent Skills CLI:

```bash
npx skills add Fable-Forge/windows-ai-cli-recovery
```

Read the [installation guide](docs/install.md) first. See [update](docs/update.md) and [uninstall](docs/uninstall.md) for lifecycle instructions.

<a id="compatibility"></a>
## Compatibility

- Supported: Codex · Claude Code · Agent Skills
- Maturity: `beta`
- GitHub Topics: `windows`, `codex`, `claude-code`, `cli`, `troubleshooting`

Compatibility means the repository format and installation paths cover these Agents. It does not guarantee that an already-running session will hot-load the skill. Verify a natural-language trigger in a fresh session after installation.

## Repository layout

- `SKILL.md`: triggers, boundaries, and primary workflow
- `agents/openai.yaml`: Codex display metadata
- `references/`: detailed material loaded on demand, when present
- `scripts/`: reusable tools and repository validator, when present
- `docs/`: install, update, and uninstall guides

<a id="validation"></a>
## Validation boundary

Structural validation, installation visibility, real triggering, and final output quality are separate claims. Passing CI proves only the repository structure and static rules; a real Agent trigger still requires its own acceptance test.

<a id="contact"></a>
## Contact and collaboration

- 📚 All skills: [FableForge Agent Skills](https://github.com/Fable-Forge/fableforge-agent-skills)
- 📧 Email: [53815263@qq.com](mailto:53815263@qq.com)
- 🐛 Bugs and feature requests: [windows-ai-cli-recovery Issues](https://github.com/Fable-Forge/windows-ai-cli-recovery/issues)
- 💬 Usage questions and business collaboration: [FableForge Discussions](https://github.com/Fable-Forge/fableforge-agent-skills/discussions) or email

## License

[MIT](LICENSE) © 2026 FableForge
