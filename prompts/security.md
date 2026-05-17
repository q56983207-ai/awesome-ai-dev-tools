# Security Prompts

Battle-tested prompts for vulnerability identification and hardening.

## 1. Security Assessment

```
Perform a security assessment of this code.

Assessment scope:
1. **Input validation** - How is user input handled?
2. **Authentication** - How are users authenticated?
3. **Authorization** - How are permissions checked?
4. **Data protection** - How is sensitive data handled?
5. **Dependencies** - Are there known vulnerabilities?

For each finding:
- Vulnerability type (OWASP Top 10 mapping)
- Location in code
- CVSS severity (1-10)
- Exploitation scenario
- Impact if exploited
- Remediation with code

Security checklist:
- [ ] All user input sanitized/validated
- [ ] SQL queries use parameterized inputs
- [ ] Output encoding for XSS prevention
- [ ] Authentication tokens are secure
- [ ] Authorization checked on every request
- [ ] Sensitive data not logged
- [ ] Cryptographic operations use current best practices
- [ ] Dependencies are up to date

Risk summary: Critical/High/Medium/Low findings with count.
```

## 2. Penetration Testing

```
Design penetration test scenarios for: [describe the target]

Test scenarios:
1. **Authentication bypass** - Can we gain unauthorized access?
2. **Injection attacks** - SQL, XSS, CSRF, command injection
3. **Data exposure** - Can we access other users' data?
4. **Privilege escalation** - Can we gain higher permissions?
5. **API abuse** - Rate limiting, parameter tampering

For each scenario:
- Attack vector
- Preconditions
- Steps to reproduce
- Expected outcome
- Severity rating

Tools to use:
- Burp Suite / OWASP ZAP for web
- sqlmap for SQL injection
- nmap for network scanning
- [application-specific tools]

Reporting format:
```
### [Attack Name]
- Severity: [Critical/High/Medium/Low]
- CVSS: [score]
- Location: [URL/Endpoint/Code]
- Reproduction: [steps]
- Impact: [what could happen]
- Fix: [recommendation]
```
```

## 3. Secure Coding Review

```
Review this code for secure coding violations.

Security patterns to check:
1. **Input validation** - Never trust user input
2. **Output encoding** - Context-appropriate escaping
3. **Authentication** - Secure password handling, token management
4. **Secrets management** - No hardcoded credentials
5. **Error handling** - Don't leak internal details

For each violation:
- CWE category (CWE-79, CWE-89, etc.)
- Code location
- Why it's vulnerable
- Secure alternative
- Test case to verify fix

Remediation priorities:
- P0: Direct exploitation possible
- P1: Could lead to data breach
- P2: Violation of security best practice
- P3: Defense-in-depth improvement

Provide corrected code for each issue.
```

## 4. Secrets Management

```
Audit this codebase for exposed secrets and design remediation.

Secrets to find:
1. **API keys** - Cloud provider, third-party services
2. **Passwords** - Database, service credentials
3. **Tokens** - JWT secrets, session keys
4. **Certificates** - Private keys, CA bundles
5. **Encryption keys** - Symmetric, asymmetric keys

Scanning approach:
1. Search for patterns (regex for API keys, etc.)
2. Check environment variable usage
3. Review configuration files
4. Verify .gitignore coverage

For each found secret:
- Location
- Secret type
- Exposure severity
- Rotation needed: Yes/No

Remediation plan:
1. Immediate rotation for exposed secrets
2. Move to secure storage (vault, env vars, secrets manager)
3. Add detection to prevent future exposure
4. Update documentation with correct usage

Prevention: Add pre-commit hooks, CI checks, documentation.
```

## 5. Dependency Vulnerability Audit

```
Audit dependencies for known vulnerabilities.

Audit process:
1. **Dependency inventory** - All direct and transitive deps
2. **Vulnerability scan** - Check against CVE databases
3. **Severity assessment** - CVSS scores for found issues
4. **Exploitability** - Is there a known exploit?
5. **Remediation path** - Upgrade or mitigate

For each vulnerable dependency:
- Package name and version
- CVE ID and severity
- Description of vulnerability
- Current exploit status
- Fix version
- Upgrade path (breaking changes?)

Report format:
| Package | Current | Vulnerable | Severity | Fix |
|---------|---------|------------|----------|-----|
| [name]  | [ver]   | [CVE]      | [score]  | [ver] |

Priority: Critical/High vulnerabilities requiring immediate action.
```

---

*Contributing? Add prompts to this file following the [template](../CONTRIBUTING.md#prompt-template).*