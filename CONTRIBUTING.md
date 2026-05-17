# Contributing to Awesome AI Prompts for Devs

Thank you for your interest in contributing! This project thrives on community contributions.

## Quick Links

- [Code of Conduct](#code-of-conduct)
- [Prompt Template](#prompt-template)
- [Quality Standards](#quality-standards)
- [Submission Process](#submission-process)

## Code of Conduct

Be respectful, constructive, and inclusive. We follow the [Contributor Covenant](https://www.contributor-covenant.org/).

## Prompt Template

```markdown
## [Prompt Name]

Brief description of what this prompt does.

```
[Exact prompt text here - copy-paste ready]
```

**When to use:** [Brief explanation of appropriate use cases]
**Expected output:** [What the AI should produce]
**Tips:** [Any variations or customizations that help]
```

### Example Submission

```markdown
## Systematic Bug Investigation

Use this when you have a bug and need a structured approach to finding the root cause.

```
Apply the scientific method to debugging:

1. **Observe** - Gather error messages, logs, reproduction steps
2. **Hypothesize** - What's causing this based on symptoms?
3. **Test** - Verify or eliminate the hypothesis
4. **Iterate** - Continue until root cause is found

For each hypothesis:
- What you tested
- What you observed
- Conclusion

End with root cause and fix recommendation.
```

**When to use:** New, unfamiliar bugs with unclear cause
**Expected output:** Root cause analysis with fix
**Tips:** Include error messages in your original query for better results
```

## Quality Standards

### Prompt Requirements

1. **Actionable** - Clear instructions that produce results
2. **Complete** - No placeholders, all context provided
3. **Tested** - Should produce good results in practice
4. **Tool-agnostic** - Works across multiple AI coding tools
5. **Scalable** - Useful for both small and large tasks

### Formatting

- Use code blocks for prompt text
- Include use case context
- Add tips for best results
- Keep consistent markdown structure

### What to Avoid

- Prompts requiring confidential/specific codebase context
- Very narrow, one-time-use prompts
- Prompts with unclear expected outputs
- Placeholder text or TODOs

## Categories

| Category | Description |
|----------|-------------|
| `code-review` | Code analysis and feedback |
| `refactoring` | Code quality improvements |
| `testing` | Test generation and strategy |
| `debugging` | Issue diagnosis and resolution |
| `documentation` | Documentation creation |
| `architecture` | System design decisions |
| `performance` | Optimization prompts |
| `security` | Security hardening |
| `git-workflow` | Version control automation |
| `onboarding` | Team collaboration |

## Submission Process

1. **Fork** the repository
2. **Create** a branch: `git checkout -b prompt/your-prompt-name`
3. **Add** your prompt to the appropriate category file
4. **Test** your prompt works well
5. **Commit**: `git commit -m "Add [prompt name] to [category]"`
6. **Push**: `git push origin prompt/your-prompt-name`
7. **Open** a Pull Request

## Pull Request Guidelines

- Title: `Add [prompt name] to [category]`
- Description: What the prompt does and why it's useful
- No more than 5 prompts per PR (easier to review)
- Follow the exact template format

## Questions?

Open an issue for discussion before implementing large contributions.

---

Thank you for making this project better! 🚀