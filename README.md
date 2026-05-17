# Awesome AI Dev Tools

> A monorepo of AI coding tools: prompts and agent rules. Each project is a standalone submodule.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

## Submodules

This repo contains standalone projects as git submodules:

| Project | Repository | Description |
|---------|------------|-------------|
| **prompts** | [q56983207-ai/awesome-ai-prompts](https://github.com/q56983207-ai/awesome-ai-prompts) | Battle-tested AI coding prompts |
| **agent-rules** | [q56983207-ai/awesome-agent-rules](https://github.com/q56983207-ai/awesome-agent-rules) | Rules templates for AI assistants |

## Structure

```
awesome-ai-dev-tools/     # This repo (monorepo)
├── prompts/              # Submodule → awesome-ai-prompts
├── agent-rules/          # Submodule → awesome-agent-rules
├── README.md
├── CONTRIBUTING.md
└── LICENSE
```

## Quick Start

### Clone with submodules

```bash
git clone --recurse-submodules https://github.com/q56983207-ai/awesome-ai-dev-tools.git
```

### Update submodules

```bash
git submodule update --remote
```

## Contributing to Submodules

Each submodule is an independent repo. To contribute:

1. **prompts** → https://github.com/q56983207-ai/awesome-ai-prompts
2. **agent-rules** → https://github.com/q56983207-ai/awesome-agent-rules

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

**Star this repo if you find it useful!** ⭐