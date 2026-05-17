# Documentation Prompts

Battle-tested prompts for clear, maintainable documentation creation.

## 1. API Documentation

```
Generate comprehensive API documentation for this code/module.

Documentation requirements:
1. **Overview** - What the API does, why it exists
2. **Authentication** - How to authenticate (if applicable)
3. **Endpoints** - Each endpoint with:
   - Purpose
   - HTTP method and path
   - Request parameters (with types, required/optional)
   - Request body schema
   - Response schema (success and error cases)
   - Example request and response
4. **Error codes** - All possible error responses
5. **Usage examples** - Common integration patterns

Format each endpoint as:
```
### [Endpoint Name]
**Purpose:** One sentence description

**Method:** GET/POST/PUT/DELETE
**Path:** /resource/:id

**Parameters:**
| Name | Type | Required | Description |

**Request Body:**
```json
{
  "field": "type" // description
}
```

**Response:** [status code]
```json
{
  "field": "type" // description
}
```

**Example:**
\`\`\`bash
curl -X POST /endpoint -d '{...}'
\`\`\`
```
```

## 2. Code Comment Documentation

```
Review and improve documentation comments in this code.

Documentation standards:
1. **Public APIs** - Every exported function/method
2. **Complex logic** - Non-obvious algorithms or business rules
3. **Edge cases** - Why certain conditions are handled
4. **Decisions** - Why a specific approach was chosen

For each improvement:
- Current comment (if any)
- Problem with current (missing, unclear, outdated)
- Improved version
- Location to add

Comment types:
- **Summary**: What the function does (one sentence)
- **Args**: Parameter descriptions
- **Returns**: What is returned and when
- **Raises**: Exceptions that can be raised
- **Examples**: Usage examples

Follow [JSDoc/numpy-style/sphinx] conventions.
```

## 3. README Generation

```
Create a comprehensive README for this project.

README structure:
1. **Badges** - CI status, version, license, coverage
2. **One-liner** - What this project does
3. **Features** - Key capabilities (3-5 bullets)
4. **Installation** - Quick install steps
5. **Usage** - Basic usage with code examples
6. **Configuration** - Environment variables, options
7. **Examples** - 2-3 common use cases
8. **Contributing** - How to contribute
9. **License** - MIT, Apache, etc.

Writing principles:
- Lead with value proposition
- Use concrete examples, not abstract descriptions
- Assume reader is skilled but new to this project
- Include just enough to get started + link to docs

Provide the complete README content.
```

## 4. Architecture Decision Records (ADR)

```
Document an architectural decision.

ADR template:
1. **Context** - What is the issue? Why is this decision needed?
2. **Decision** - What is the change? What was decided?
3. **Consequences** - What becomes better? What becomes worse?

Include:
- **Status**: Proposed / Accepted / Deprecated / Superseded
- **Date**: When this was decided
- **Deciders**: Who was involved
- **Options considered** (even if rejected)
- **Pros and cons** of each option
- **Reasoning** for final choice
- **Alternatives** considered

Format as Markdown with clear sections. This ADR should be:
- Atomic (one decision per ADR)
- Stable (historical record, not edited)
- Discoverable (linked from code that implements it)

Provide the complete ADR document.
```

## 5. Changelog Generation

```
Generate a changelog from git commit history.

Changelog principles (Keep a Changelog format):
1. **Categories**: Added / Changed / Deprecated / Removed / Fixed / Security
2. **Semantic versioning**: Map changes to MAJOR.MINOR.PATCH
3. **User视角**: What matters to users, not internal details
4. **Link to issues**: Reference ticket numbers

Process:
1. Parse commits since last release
2. Categorize each change
3. Identify breaking changes (MAJOR)
4. Group related changes
5. Write user-friendly descriptions

For each entry:
\`\`\`
- [Description] - [Issue #] (@contributor)
\`\`\`

Format:
\`\`\`markdown
# [Version] - YYYY-MM-DD

## Added
- Feature A with capability X

## Changed
- Improved performance of operation Y

## Fixed
- Bug where Z would fail
\`\`\`

Provide the complete changelog content.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*