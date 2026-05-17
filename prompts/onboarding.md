# Onboarding Prompts

Battle-tested prompts for codebase understanding and team collaboration.

## 1. Codebase Tour

```
Generate a comprehensive codebase tour for new team members.

Tour structure:
1. **Project overview** - What it does, why it exists
2. **Architecture** - High-level components and their relationships
3. **Directory structure** - What each folder contains and why
4. **Key files** - Critical files every developer should know
5. **Tech stack** - Languages, frameworks, tools used
6. **Getting started** - Local development setup

For each major component:
- Purpose and responsibility
- Key files and classes
- How it interacts with other components
- Common tasks and patterns

Must-know for new developers:
- How to run locally
- How to run tests
- How to debug
- Where to find help
- Common pitfalls to avoid

Provide: ASCII architecture diagram, directory tree, key file map.
```

## 2. Architecture Decision Explanation

```
Explain the key architectural decisions in this codebase.

For each major decision:
- **What** - The decision made
- **Why** - Context and constraints that led to it
- **Alternatives considered** - What else was evaluated
- **Trade-offs** - What was prioritized and what was sacrificed
- **Current status** - Is it still the right decision?

Focus on:
- Why the current architecture was chosen
- Key technology selections
- Design patterns used and why
- Known limitations and technical debt
- How the system evolved to this point

For each decision, provide enough context for someone to:
- Understand the current state
- Know why changes are difficult
- Make informed decisions about modifications
- Avoid repeating past mistakes

This should help new team members understand the "why" behind the code.
```

## 3. Development Workflow Guide

```
Document the development workflow for this project.

Workflow steps:
1. **Issue assignment** - How work is assigned and tracked
2. **Branch creation** - Naming, base branch, scope
3. **Development** - Coding standards, IDE setup
4. **Code review** - Process, expectations, feedback culture
5. **Merge and deploy** - Release process, deployment pipeline

For developers:
- First day checklist
- Week one goals
- First PR expectations
- Where to find help

Tools and access:
- Issue tracker
- Repository access
- CI/CD pipeline
- Monitoring/logs
- Communication channels

Common scenarios:
- How to handle merge conflicts
- What to do if tests are failing
- How to request help
- How to escalate blockers

Provide: workflow diagram, cheat sheet, FAQ.
```

## 4. Debugging Guide

```
Create a debugging guide for this codebase.

Common issues and solutions:
1. **Setup issues** - Environment, dependencies, permissions
2. **Runtime errors** - How to diagnose and fix
3. **Test failures** - Understanding and resolving
4. **Performance problems** - Profiling and optimization
5. **Deployment issues** - Rollback and recovery

For each issue type:
- Symptoms to recognize
- Common causes
- Diagnostic steps
- Solution approaches
- Prevention measures

Debugging toolkit:
- Logging configuration
- IDE debugger setup
- Test utilities
- CLI tools and commands
- Monitoring dashboards

Error messages guide:
- Common errors and what they mean
- Where to look for more context
- How to search for solutions

Provide step-by-step troubleshooting flows.
```

## 5. Team Collaboration Guide

```
Document how the team collaborates effectively.

Communication:
- **Sync meetings** - When, who, agenda expectations
- **Async channels** - Slack, email, GitHub comments
- **Documentation** - Where to find and how to update
- **Knowledge sharing** - How to share learning

Code collaboration:
- **PR expectations** - Size, review turnaround, merge criteria
- **Review culture** - Constructive feedback, async by default
- **Pair programming** - When and how
- **Mob programming** - For complex problems

Decision making:
- **Who decides what** - DR原则 (boring architecture vs local decisions)
- **RFC process** - How to propose and discuss changes
- **Escalation path** - When and how to escalate
- **Retrospectives** - How we improve

Onboarding new members:
- Buddy system
- First week structure
- 30-60-90 day expectations
- How to ask questions

Provide: team directory, communication matrix, decision framework.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*