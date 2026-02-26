---
title: Checklist for Selecting a Python Security Testing Tool
short_title: Tool Selection Checklist
---

## Essential Checklist for Selecting a Python Security Testing Tool

Selecting a FOSS (Free and Open Source Software) tool for Python security testing isn't just about finding one that works—it's about ensuring the tool itself meets strict quality, maintenance, and reliability constraints.

A Python security testing tool should meet the following criteria:

* **FOSS-licensed:** The product must be released under a valid FOSS licence, preferably one approved by the Open Source Initiative (OSI).
* **Local-first deployment:** The tool should run locally or on a server within your own security perimeter. Avoid SaaS-only solutions where you cannot control the execution environment or data handling.
* **Actively maintained:** The project should be active and demonstrate an acceptable level of quality, including regular updates and issue management.
* **Public version control repository:** The source code must be publicly accessible in a version-controlled repository with a clear and verifiable URL.

Ideally, projects should also meet the minimum requirements outlined by the [OpenSSF Best Practices Badge](https://www.bestpractices.dev/en) Program. However, despite significant effort from the community, this programme is still not widely recognised or adopted.

In practice, you will use a long list when selecting test software for Python.
For each tool, you should use a proven checklist that helps you choose a suitable FOSS testing tool for your purpose.

## Selecting a Static Application Security Test (SAST) Tool for Python

Use a FOSS tool. Free and Open Source Software (FOSS) makes it easier to comply with the proven cybersecurity principle: “Never Trust, Always Verify.” Be cautious of commercial vendors who market their tools as FOSS—too often this is only a marketing claim.


- **Prefer a local-first solution.** Security is critical—especially when dealing with security tools themselves. Avoid relying on remote solutions you cannot control.

+++

- **Validations on the Python Standard Library (PSL).** Ensure that the tool performs crucial security validations on all modules that are part of the PSL that can cause vulnerabilities, and that these checks are enabled by default.

+++


- Choose a **Python dedicated scanner**. General-purpose SAST tools often **miss** vulnerabilities specific to Python. Since Python has unique syntax and constructs, only scanners designed for Python can effectively detect potential security issues in Python code well.

+++


- Look for the [OpenSSF Best Practices Badge](https://www.bestpractices.dev/en). Projects that have earned the Open Source Security Foundation (OpenSSF) best practices badge show evidence of a structured self-assessment. While the process is self-reported, it indicates that the maintainers have considered important security practices relevant for t**rustworthy software**.

+++


For example, when selecting a SAST tool for Python, you can use the following selection criteria in combination with above mentioned checks:


![toolselection](/images/selectioncriteria.png)