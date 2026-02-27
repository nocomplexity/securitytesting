---
title: Installation of security test tools 
short_title: Installation of test tools 
---


Proper installation of security testing tools is a critical first step in any Python security assessment workflow. Mistakes at this stage can introduce vulnerabilities, compromise test results, or even contaminate the testing environment itself.


Security testing tools must be installed with the same rigor applied to production systems. A poorly installed or unverified tool can invalidate test results, introduce vulnerabilities, and undermine the credibility of the assessment.

Secure installation of test tools is not optional — it is part of the security testing process itself.


## Always Install in a Secure Environment

Always install security testing tools in an isolated and controlled environment:

* Use **virtual environments** (`venv` or use [`conda`](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)) for project-level isolation.
* Prefer **dedicated test machines** or hardened virtual machines.
* Never install security testing tools directly on production systems.
* Ensure your operating system and Python interpreter are up to date with security patches.

Isolation prevents dependency conflicts and reduces the risk of exposing sensitive systems to unstable or malicious packages.

See the [section on importance of a secure test environment](isolation) for a recap.



## Use Only `pip` for Python Test Tools

Many security testing tools for Python are written in Python, sometimes with extensions in other languages.

For Python-based tools, that can be installed with `pip`:

:::{important}
**Install packages exclusively via `pip` from the official Python Package Index (PyPI.org):**
:::

```bash
python -m venv venv
source venv/bin/activate   # or venv\Scripts\activate on Windows
pip install toolname
```


Avoid:

* Installing directly from Git repositories (`pip install git+https://...`)
* Downloading and running arbitrary setup scripts
* Executing unverified installation commands from blogs or forums

Using `pip` ensures:

* Standardized installation processes
* Dependency management
* Version control
* Traceability



## Never Install Tools Directly from Git

Installing directly from Git repositories introduces significant risks:

* Code may not be reviewed or stable
* Commits may change without notice
* You may unknowingly install malicious or untested code

Only install officially released versions published to PyPI.org. If a tool is not available via `pip`, reconsider whether it meets quality and security standards.



## Validate Tools Before Installation (QA Aspects)

:::{tip}
See also section on [Selecting a Python Security Testing Tool](/module2/toolselection)
:::

Before installing any security testing tool, validate:

* **Maintainer reputation** and activity
* Recent updates and release history
* Open issues and unresolved security concerns
* License compliance
* Community adoption and trust level
* Dependency list and transitive dependencies

Security tools themselves must meet high security standards. A vulnerable testing tool can compromise your testing infrastructure.



## Document Every Step

Documentation is part of professional security practice. Is is also a key requirement for reproducible testing. See section on [Reproducibility](reproducibility).

Always record:

* Exact installation commands used
* Python version
* Operating system details
* Tool versions installed (`pip freeze > requirements.txt`)
* Hashes if applicable

Example:

```bash
pip freeze > requirements.txt
```

This ensures:

* Reproducibility
* Auditability
* Compliance readiness
* Easier troubleshooting

`pip freeze` is a simple tool that for creating an output of installed packages in requirements format(`txt`).
  


## Document Installed Versions

Never rely on “latest” versions or automatic updates in professional testing environments. Explicitly specify versions when performing security testing that must be 100% reproducible:

```bash
pip install toolname==1.4.2
```

Version pinning:

* Prevents unexpected breaking changes
* Improves stability
* Ensures consistent test results across environments

:::{tip}
If you do use `pip install -U <package-name>` always make sure to record the exact installed version!
:::


## Checklist 

| Step    | Action                                  | Why?                                       |
| ------- | --------------------------------------- | ------------------------------------------ |
| Verify  | Validate tool reputation and QA.        | Ensures tool reliability.                  |
| Isolate | Create a fresh virtual environment.     | Prevents system-wide contamination.        |
| Install | Use `pip install [package]==[version]`. | Ensures standardized, vetted code.         |
| Log     | Record versions and installation steps. | Provides an audit trail for your findings. |
