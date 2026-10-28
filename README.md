# Enterprise Code & Configuration Security Auditor Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill Version](https://img.shields.io/badge/skill-v1.0.0-green.svg)](SKILL.md)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

An authoritative [Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) empowering AI coding assistants to act as a **Principal Application Security Engineer & DevSecOps Auditor**. Performs comprehensive Shift-Left security audits across **SAST**, **SCA**, **Secret Detection**, and **IaC/Configuration Hardening** grounded in the **OWASP Top 10**, **OWASP API Security**, **CWE/SANS Top 25**, and **CIS Benchmarks**.

---

## What It Does

When an AI coding assistant reviews a pull request, audits a repository, or evaluates infrastructure configurations, this skill enforces a structured 4-phase security methodology:

1. **Credential & Secret Detection**: Scans source code, environment files (`.env*`), application configs, and CI/CD pipelines for hardcoded API keys, JWTs, OAuth secrets, private keys, cloud credentials, and plaintext database URIs, while validating `.gitignore` and `.dockerignore` coverage.
2. **Static Application Security Testing (SAST)**: Traces untrusted data from *source* to *sink* to detect Injection flaws (SQLi, NoSQLi, Command/LDAP Injection), Broken Access Control (IDOR/BOLA, missing RBAC/ABAC), XSS, Insecure Deserialization, Cryptographic Failures, SSRF, and Mass Assignment.
3. **Configuration & IaC Hardening**: Audits web servers and application configs (Debug mode, CORS, HSTS/CSP headers, Cookie flags), Container definitions (`Dockerfile`, `docker-compose`), Kubernetes manifests (`securityContext`, resource limits), Terraform/Cloud policies (public buckets, open security groups, wildcard IAM), and CI/CD workflows (script injection, `permissions`, pinned SHAs).
4. **Software Composition Analysis (SCA)**: Evaluates dependency manifests (`package.json`, `requirements.txt`, `go.mod`, `pom.xml`, `composer.json`, `Cargo.toml`) and verifies lockfile integrity to prevent supply-chain and dependency confusion risks.
5. **Actionable Drop-in Remediations**: Produces a standardized **Project Security Audit Report** complete with severity classification, CWE/OWASP mapping, context-aware false-positive filtering, and framework-specific drop-in code fixes.

---

## Audit Coverage Matrix

| Audit Phase | Target Scope | Key Vulnerabilities & Misconfigurations | Standards & Benchmarks |
| :--- | :--- | :--- | :--- |
| **Phase 1: Secret Detection** | Source files, `.env*`, configs, CI/CD, `.gitignore` | Hardcoded API keys, private keys, cloud credentials (`AKIA...`), plaintext DB URIs | OWASP Top 10 (A02/A07), CWE-798 |
| **Phase 2: SAST (Code & API)** | `.js`, `.ts`, `.py`, `.go`, `.java`, `.php`, `.rb`, `.cs`, `.rs` | SQLi/NoSQLi, Command Injection, IDOR/BOLA, XSS, Deserialization, Weak Crypto, SSRF, Mass Assignment | OWASP Top 10, OWASP API Security Top 10, CWE Top 25 |
| **Phase 3: IaC & Config** | `Dockerfile`, `docker-compose`, K8s, `.tf`, Nginx/Apache, GitHub Actions / GitLab CI | Root containers, `:latest` tags, K8s `privileged: true`, open ports (`0.0.0.0/0`), wildcard IAM, CI script injection, permissive CORS | CIS Benchmarks, NSA/CISA K8s Hardening, GitHub Actions Security |
| **Phase 4: SCA & Supply Chain** | `package.json`, `requirements.txt`, `go.mod`, `pom.xml`, `composer.json`, `Cargo.toml` | Missing lockfiles, dependency confusion vectors, deprecated packages, known high-profile CVEs | OWASP Top 10 (A06), SLSA / Supply Chain Security |

---

## Severity Classification

| Severity | Classification Criteria |
| :--- | :--- |
| 🔴 **CRITICAL** | Remote Code Execution (RCE), full database compromise (SQLi), leaked production credentials/private keys, or unauthenticated admin access. |
| 🟠 **HIGH** | Unauthorized cross-tenant data access (IDOR/BOLA), SSRF to internal/metadata networks, Stored XSS, `privileged` containers, or publicly exposed database ports. |
| 🟡 **MEDIUM** | Overly permissive CORS (`*` with credentials), weak password hashing (MD5/SHA-1) or PRNGs (`Math.random()`), missing auth rate limiting, Reflected XSS, or root containers. |
| 🔵 **LOW / INFO** | Missing secondary HTTP security headers, unpinned `:latest` container tags, mildly verbose error responses, or non-exploitable defense-in-depth gaps. |

---

## Installation

### Method 1: Ask Your Agent (Recommended)

Paste this into your AI coding assistant (Gemini CLI, Antigravity, Claude Code, Cursor, Codex):

Clone or copy the directory into your skills folder, and verify it is registered.
```text
Install the enterprise-security-auditor skill from https://github.com/hpdrr/enterprise-security-auditor.git
```

Your agent will inspect its own configuration and register the skill.

### Method 2: Manual Installation

Clone this repository into your agent's skill directory:

#### For Antigravity / Gemini CLI:
```bash
# Global installation (available across all workspaces)
git clone https://github.com/hpdrr/enterprise-security-auditor.git ~/.gemini/config/skills/enterprise-security-auditor
```

#### For Claude Code:
```bash
# Workspace only
git clone https://github.com/hpdrr/enterprise-security-auditor.git your-project/.claude/skills/enterprise-security-auditor

# User-level (all workspaces)
git clone https://github.com/hpdrr/enterprise-security-auditor.git ~/.claude/skills/enterprise-security-auditor
```

#### For Other Agent Frameworks:
Copy `SKILL.md` or clone the repository into your agent's configured skills path (such as `.agent/skills/` or `~/.agents/skills/`).

---

## Usage Examples

Once installed, the skill activates automatically when you request security reviews, vulnerability scans, or configuration audits. You can also trigger it explicitly:

### 1. Full Repository Security Audit
> "Run a comprehensive security audit on this repository using the enterprise-security-auditor skill and generate a full Project Security Audit Report."

### 2. API & Backend SAST Review
> "Check our Express/TypeScript API routes for IDOR/BOLA, mass assignment, and injection vulnerabilities."

### 3. Infrastructure & Container Hardening
> "Audit our Dockerfile, Kubernetes manifests, and GitHub Actions workflows for privilege escalation, secret leakage, and CI script injection risks."

---

## Repository Contents

```text
enterprise-security-auditor/
├── .github/
│   ├── workflows/
│   │   └── validate.yml          # Frontmatter and Markdown validation CI
│   └── pull_request_template.md  # PR checklist for security rules
├── .gitignore                    # OS, editor, and temporary file ignores
├── CONTRIBUTING.md               # Guidelines for expanding audit rules and benchmarks
├── LICENSE                       # MIT License
├── README.md                     # Documentation and quickstart guide
└── SKILL.md                      # Core security auditor skill instructions and report template
```

---

## Contributing

Contributions expanding detection rules, language-specific SAST sinks, cloud/IaC benchmarks, or supply-chain checks are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## License

This project is licensed under the [MIT License](LICENSE).
