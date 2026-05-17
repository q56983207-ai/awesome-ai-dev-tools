# Git & Workflow Prompts

Battle-tested prompts for version control and development process automation.

## 1. Git History Cleanup

```
Clean up git history for a more maintainable project.

Tasks:
1. **Identify issues** - Large files, sensitive data, merge artifacts
2. **Rewrite history** - Use filter-branch or filter-repo
3. **Squash commits** - Group related changes meaningfully
4. **Enforce conventions** - Commit message format, branch naming

Cleanup operations:
1. **Remove sensitive data** - API keys, passwords, credentials
2. **Compress large files** - Git LFS for binaries
3. **Fix commit messages** - Amend or reword poorly written messages
4. **Consolidate WIP commits** - Group "work in progress" into coherent units

Before/after:
- Number of commits: X → Y
- Repository size: A → B
- Largest commit: C → D

Safety measures:
- Work on a backup branch
- Document all changes
- Test after each operation
- Force push only to feature branch (never main)

Provide step-by-step commands for each cleanup operation.
```

## 2. Branch Strategy Implementation

```
Implement a Git branching strategy for: [team size, deployment cadence]

Common strategies:
1. **GitFlow** - Production branches, feature branches, release management
2. **Trunk-based** - Short-lived features, continuous deployment
3. **Forking** - External contributions, open source

For this team/project:
- Branch naming conventions
- When to create branches
- How to merge (PR, rebase, squash)
- Release process
- Hotfix handling

Branch lifecycle:
1. Create from [base branch]
2. Make changes
3. Keep updated with [base]
4. Code review process
5. Merge strategy
6. Delete after merge

Automation opportunities:
- Branch creation hooks
- CI on PR
- Auto-delete merged
- Protected branches

Provide workflow diagram and implementation scripts.
```

## 3. Automated Changelog

```
Set up automated changelog generation from git history.

Requirements:
1. **Semantic commits** - Conventional Commits format
2. **Automated parsing** - Extract changes from commit messages
3. **Categorization** - Group by type (feat, fix, docs, etc.)
4. **Version bumping** - Automatic based on commit types

Configuration:
\`\`\`yaml
# changelog.yaml
types:
  - type: feat
    label: Added
    semver: minor
  - type: fix
    label: Fixed
    semver: patch
  - type: docs
    label: Changed
    semver: none
  - type: break
    label: Breaking
    semver: major
\`\`\`

Process:
1. Enforce commit message format via git hooks
2. On release tag, generate changelog
3. Include: PR numbers, authors, issue references

CI integration:
- Validate commit messages on push
- Generate changelog on release
- Post to GitHub release notes

Provide setup commands and hook scripts.
```

## 4. Git Hooks Setup

```
Set up Git hooks to automate quality checks.

Available hooks:
- **pre-commit** - Before each commit
- **commit-msg** - Validate commit messages
- **pre-push** - Before push (slower checks)
- **post-commit** - After commit (notifications)
- **pre-rebase** - Before rebase

Implementations:
1. **Pre-commit** - Run linters, formatters, tests
2. **Commit-msg** - Enforce conventional commits
3. **Pre-push** - Full test suite, security scan

Hook examples:
\`\`\`bash
#!/bin/sh
# pre-commit
npm test
npm run lint
\`\`\`

Safety measures:
- Fail fast on errors
- Provide clear error messages
- Skip hooks with --no-verify (use sparingly)
- Keep hooks fast (under 30 seconds)

Provide hook implementations and installation instructions.
```

## 5. Release Process Automation

```
Design an automated release process.

Process steps:
1. **Version bump** - Detect and increment version
2. **Changelog generation** - Compile changes since last release
3. **Build** - Compile, bundle, create artifacts
4. **Testing** - Run integration/e2e tests
5. **Sign** - Sign artifacts (if needed)
6. **Publish** - Push to registry, create GitHub release
7. **Notify** - Slack, email, release notes

Tools to use:
- semantic-release / release-it
- GitHub Actions
- GitHub Releases

For each step:
- What happens
- How to customize
- What can go wrong
- Rollback procedure

CI/CD configuration:
\`\`\`yaml
on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm test
      - run: npm run build
      - run: npm publish
\`\`\`

Provide complete workflow file and documentation.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*