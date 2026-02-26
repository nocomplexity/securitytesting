---
title: Verification Without Runtime Execution
short_title: Verification Techniques
---

This section introduces methods for verifying security without necessarily executing the application at runtime. You will learn how to:

* Apply static verification approaches
* Use automated analysis tools
* Perform structured manual reviews
* Distinguish between technical security testing and compliance-oriented verification


Verification without runtime execution refers to analysing Python code and related artefacts **without running the application**. The objective is to identify weaknesses, insecure patterns, and compliance gaps through static inspection and structured review.

In the context of security testing, this approach is commonly known as *static analysis* or *static verification*.

It is particularly valuable because it:

* Detects vulnerabilities early in the development lifecycle
* Does not require a fully deployed environment
* Can be automated and integrated into CI/CD pipelines
* Scales across large codebases



When verifying without execution, you typically assess:

* Source code
* Dependency definitions (e.g. `requirements.txt`, `pyproject.toml`)
* Configuration files
* Infrastructure-as-code templates
* Security policies and documentation

The focus is on identifying structural and logical weaknesses rather than runtime behaviour.



## Typical Verification Steps

### 1. Define Scope and Criteria

* Determine which repositories, modules, or services are in scope
* Define the security baseline or framework to test against
* Identify regulatory or organisational requirements

Clear criteria are essential. Without them, verification becomes inconsistent and subjective.



### 2. Static Code Analysis

Use automated tools to detect insecure coding patterns such as:

* Hard-coded secrets
* Unsafe deserialisation
* Insecure use of cryptography
* Injection risks
* Improper error handling

Common tools include:

* `Python Code Audit` – Security-focused static analysis for Python

This tools analyse Python source code without executing it.



### 3. Dependency and Supply Chain Verification

Review third-party dependencies for known vulnerabilities and licensing risks.

Typical tools include:

* `pip-audit` – Checks installed packages against known vulnerability databases

This step addresses supply chain security risks, which are increasingly relevant in Python ecosystems.



### 4. Configuration Review

Manually or automatically verify:

* Debug mode is not enabled in production
* Secure cookie settings are enforced
* TLS configuration is correct
* Logging does not expose sensitive data
* Environment variables are handled securely

Misconfiguration is a frequent cause of security incidents.

---

### 5. Secrets and Credential Scanning

Identify accidental exposure of:

* API keys
* Private keys
* Passwords
* Tokens

Tools such as `gitleaks` or `trufflehog` scan repositories for embedded secrets.

---

### 6. Manual Code Review

Automated tools are effective but limited. A structured manual review helps detect:

* Business logic flaws
* Insecure architectural decisions
* Authorisation weaknesses
* Misuse of frameworks

Manual review is essential for deeper security assurance.

---

## Advantages of Non-Execution Verification

* Safe (no risk of damaging environments)
* Repeatable and automatable
* Suitable for early development stages
* Cost-effective compared to late-stage remediation

However, it does not reveal runtime issues such as:

* Memory behaviour
* Race conditions
* Real authentication flows
* Deployment-specific misconfigurations

For that, dynamic testing is required.

---

## Security Testing vs Formal Audit (ISO / NEN)

It is important to distinguish between **security testing** and a **formal compliance audit**.

## Security Testing Perspective

Security testing:

* Is technically focused
* Seeks to identify real vulnerabilities
* Often uses automated tools
* Produces actionable remediation findings
* Can be continuous and iterative

Its primary goal is risk reduction through technical improvement.

---

## Formal Audit Perspective (e.g. ISO or NEN)

A formal audit under standards such as ISO or NEN:

* Evaluates whether processes comply with defined control frameworks
* Reviews documentation, governance, and evidence
* Assesses whether policies are implemented and followed
* Focuses on assurance rather than vulnerability discovery

An auditor may review whether:

* Secure development policies exist
* Code reviews are mandated
* Vulnerability management procedures are documented
* Responsibilities are clearly assigned

However, auditors typically do not perform deep technical exploitation or detailed code-level analysis unless explicitly scoped.

---

## Key Differences

| Aspect    | Security Testing             | Formal Audit (ISO/NEN)             |
| --------- | ---------------------------- | ---------------------------------- |
| Focus     | Technical weaknesses         | Process and control compliance     |
| Depth     | Code and configuration level | Governance and documentation level |
| Frequency | Continuous or periodic       | Periodic (e.g. annually)           |
| Output    | Vulnerability findings       | Compliance status and audit report |
| Objective | Risk reduction               | Assurance and certification        |

---

## Complementary, Not Competing

Verification without runtime execution plays a role in both domains:

* In security testing, it identifies vulnerabilities and weaknesses.
* In formal audits, it can serve as evidence that secure development practices are in place.

However, passing an ISO or NEN audit does **not** guarantee that the Python application is secure. It indicates that processes exist and are followed.

Conversely, performing static security testing does not automatically prove compliance with a formal standard.

A mature organisation integrates both:

* Continuous technical verification
* Structured governance and compliance frameworks

Together, they provide stronger assurance than either approach alone.
