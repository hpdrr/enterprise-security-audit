# Contributing to Enterprise Security Auditor

Contributions to expand vulnerability detection patterns, refine SAST/IaC audit checklists, and incorporate updated industry benchmarks are welcome.

## Guidelines

1. **Align with Authoritative Security Standards**:
   - Ground new rules and checks in established frameworks such as **OWASP Top 10**, **OWASP API Security Top 10**, **CWE/SANS Top 25**, **CIS Benchmarks**, or **SLSA**.
   - Emphasize defensive, actionable remediation patterns and low false-positive guidance over theoretical or weaponized payloads.

2. **File Structure & Frontmatter Consistency**:
   - Maintain valid YAML frontmatter in `SKILL.md` (`name`, `description`, `triggers`, `version`, `permissions`).
   - Keep rules concise, specifying clear *sources*, *sinks*, and secure drop-in replacements.

3. **Submitting Changes**:
   - Fork the repository.
   - Create a feature branch (`git checkout -b feature/graphql-security-checks`).
   - Ensure `SKILL.md` passes YAML frontmatter verification.
   - Open a Pull Request detailing the vulnerability class, CWE/OWASP reference, and remediation rationale.
