---
title: Protecting your findings after security testing
short_title: Securing your findings
---

## Overview 

The protection of security test findings is a critical, yet often overlooked, aspect of Python security testing. SAST results, vulnerability reports and analysis artefacts frequently contain sensitive technical information, including internal file paths, configuration details, dependency versions and potentially exploitable weaknesses. If exposed, this information may significantly lower the effort required for an attacker to compromise the system.

Security findings should therefore be treated as sensitive information and handled accordingly.


## Why Security Data is High-Risk

When testing Python applications on security weaknesses, your findings often contain:

- Hardcoded Secrets: API keys or database credentials discovered during static analysis (SAST).

- Tracebacks: Detailed error messages that reveal internal file structures and library versions.

- Exploit Payloads: The specific strings or scripts used to trigger a vulnerability (e.g., a specific SQL injection string).

- PII/Sensitive Data: Real user data accidentally captured during dynamic testing (DAST).

-  Identified vulnerabilities and their locations in the source code
-  Dependency weaknesses and known CVEs
- Architectural or configuration details
- Information about internal infrastructure

If such information is leaked, it can provide attackers with a roadmap to exploit the system before remediation has taken place.

## Good Practice Recommendations

Securing your results requires a "defense-in-depth" approach, ensuring the data is protected while at rest, in transit, and during the reporting phase.

To protect test findings, the following measures are recommended:

### Access Control

* Restrict access to security reports on a need-to-know basis.
* Store reports in access-controlled repositories or secure document management systems.
* Avoid distributing findings via unsecured email attachments.


### Encrypt Everything
Never store vulnerability reports in plain text on a local machine or a shared drive.

- At Rest: Use full-disk encryption or encrypted containers (like Veracrypt) for storing local logs.

- In Transit: If you are sending a report to a developer, never use standard email. Use encrypted communication channels or password-protected, end-to-end encrypted file-sharing services.


### Secure Storage

* Encrypt stored reports where appropriate.
* Ensure backups containing security findings are equally protected.
* Avoid storing sensitive results on unmanaged local machines.

### Sanitize Your Reports
Before a report leaves your "secure zone," scrub it of unnecessary sensitive data.

- Masking: If a finding shows a leaked API key, replace the middle characters with asterisks (e.g., AKIA...****...789).

- Redaction: Remove actual PII (names, emails, credit card numbers) that may have been caught in a request/response log. Use placeholder data to demonstrate the flaw instead.

### Implement Strict Access Control
The "Principle of Least Privilege" applies here. Not everyone in the organization needs to see the full security audit.

- Need-to-Know: Limit access to the specific developers responsible for the fix and the security team.

- Audit Logs: Use a centralized vulnerability management platform (like DefectDojo or Jira with restricted permissions) that tracks who accessed the report and when.


### Controlled Communication

* Share findings through secure collaboration platforms.
* Clearly label reports as confidential.
* Avoid including sensitive vulnerability details in public issue trackers.




### Retention and Disposal

:::{tip}
Automate Data Retention Policies
:::

Security findings have a shelf life. Once a vulnerability is patched and verified, the detailed "how-to-exploit" data becomes a liability.

- Purge Cycles: Establish a policy to delete raw scan logs and exploit POCs (Proofs of Concept) after a set period (e.g., 90 days).
* Define retention periods for security reports.
* Securely delete outdated findings that are no longer required.
* Ensure exported artefacts from SAST tools are removed from temporary directories.


### Audit and Traceability

* Keep records of who accessed or modified security reports.
* Maintain version control for updated findings to ensure accountability.

## Additional Considerations

When using third-party SAST tools or cloud-based platforms, verify how findings are stored and processed. Ensure that data protection requirements, contractual obligations and regulatory standards are met.

In summary, conducting security testing is only part of the responsibility. Protecting the results of that testing is equally important to prevent introducing new security risks while attempting to identify and mitigate existing ones.
