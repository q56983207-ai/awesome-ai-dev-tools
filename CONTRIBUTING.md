# Contributing to Awesome AI Dev Tools

This is a monorepo with standalone submodules. Each project has its own repository.

## Projects

| Project | Repo | Description |
|---------|------|-------------|
| **prompts** | [awesome-ai-prompts](https://github.com/q56983207-ai/awesome-ai-prompts) | AI coding prompts |
| **agent-rules** | [awesome-agent-rules](https://github.com/q56983207-ai/awesome-agent-rules) | AI assistant rules |

## How to Contribute

### To a Submodule Project

Each submodule is an independent repository. Submit contributions directly to the relevant repo:

1. **Prompts**: Fork and PR to [q56983207-ai/awesome-ai-prompts](https://github.com/q56983207-ai/awesome-ai-prompts)
2. **Agent Rules**: Fork and PR to [q56983207-ai/awesome-agent-rules](https://github.com/q56983207-ai/awesome-agent-rules)

### To This Monorepo

For the monorepo itself (docs, issue triage, etc.):

1. Fork this repository
2. Create a branch
3. Make your changes
4. Submit a PR

## Working with Submodules

### Clone with submodules

```bash
git clone --recurse-submodules https://github.com/q56983207-ai/awesome-ai-dev-tools.git
```

### Pull latest changes

```bash
git submodule update --remote
```

### Make changes to a submodule

```bash
cd prompts  # or agent-rules
git checkout -b feature/my-feature
# make changes, commit, push
cd ..
git add prompts
git commit -m "Update prompts submodule"
git push
```

---

Thank you for contributing! 🚀