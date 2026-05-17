# Awesome AI Prompts for Devs

> A curated collection of high-quality AI coding prompts for developers. Supports Claude Code, Codex, Cline, Roo Code, Cursor, Aider and more.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Contributors](https://img.shields.io/github/contributors/q56983207-ai/awesome-ai-prompts-for-devs.svg)](https://github.com/q56983207-ai/awesome-ai-prompts-for-devs/graphs/contributors)

## Table of Contents

- [About](#about)
- [Quick Start](#quick-start)
- [Prompt Categories](#prompt-categories)
- [Usage Examples](#usage-examples)
- [Supported Tools](#supported-tools)
- [Contributing](#contributing)
- [License](#license)

## About

`awesome-ai-prompts-for-devs` is a comprehensive, community-driven collection of battle-tested AI prompts designed to maximize your productivity when using AI coding assistants. Each prompt is crafted to deliver precise, professional results with minimal iteration.

## Quick Start

1. **Browse categories** — Find the prompt type you need
2. **Copy** — Click the copy button on any prompt
3. **Paste** — Add it to your AI coding tool
4. **Iterate** — Refine based on your specific needs

## Prompt Categories

| Category | Description |
|----------|-------------|
| [Code Review](prompts/code-review.md) | Systematic code analysis and improvement suggestions |
| [Refactoring](prompts/refactoring.md) | Clean code patterns and architectural improvements |
| [Testing](prompts/testing.md) | Comprehensive test generation and strategy |
| [Debugging](prompts/debugging.md) | Systematic issue diagnosis and resolution |
| [Documentation](prompts/documentation.md) | Clear and maintainable documentation creation |
| [Architecture](prompts/architecture.md) | System design and technical decision-making |
| [Performance](prompts/performance.md) | Optimization and efficiency improvements |
| [Security](prompts/security.md) | Vulnerability identification and hardening |
| [Git & Workflow](prompts/git-workflow.md) | Version control and development process automation |
| [Onboarding](prompts/onboarding.md) | Codebase understanding and team collaboration |

## Usage Examples

### Example 1: Code Review

```
As a senior code reviewer, analyze the following code for:
1. Logic errors and edge cases
2. Performance bottlenecks
3. Security vulnerabilities
4. Code smells and maintainability issues
5. Test coverage gaps

Provide a prioritized fix list with code examples.
```

### Example 2: Refactoring

```
Act as a refactoring expert. Given the following code:
1. Identify code smells (duplication, long methods, etc.)
2. Propose specific refactoring patterns
3. Show before/after comparisons
4. Preserve all existing behavior
5. Explain the rationale for each change
```

### Example 3: Testing

```
Generate comprehensive tests for the following code:
- Unit tests for all public methods
- Edge case coverage
- Mock external dependencies
- Include descriptive test names
- Follow [testing framework] conventions
```

## Supported Tools

| Tool | Type | Integration |
|------|------|-------------|
| **Claude Code** | CLI Agent | Native support |
| **Codex** | API | Direct prompt input |
| **Cline** | VS Code Extension | Clipboard paste |
| **Roo Code** | VS Code Extension | Clipboard paste |
| **Cursor** | IDE | Rules feature |
| **Aider** | CLI Chat | `aider --prompt-file` |
| **GitHub Copilot** | IDE Plugin | Inline suggestion trigger |

## How to Contribute

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting.

### Quick Contribution Steps

1. Fork the repository
2. Create a new branch: `git checkout -b prompt/category-name`
3. Add your prompt following the [template](CONTRIBUTING.md#prompt-template)
4. Run linting: `bash scripts/validate.sh`
5. Commit and push
6. Open a Pull Request

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

**Star this repo if you find it useful!** ⭐