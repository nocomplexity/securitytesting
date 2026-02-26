---
title: Checking used libraries with of Python Code Audit 
short_title: Checking Python dependencies
---


## Introduction

Security vulnerabilities in Python applications are frequently introduced through third-party libraries rather than through custom code. Each additional dependency:

* May contain known vulnerabilities
* May introduce insecure defaults
* May depend on other vulnerable packages
* Increases overall maintenance complexity

A high dependency count increases the likelihood that at least one component has a known CVE or unpatched issue.

:::{admonition} Scope: Python Dependencies
:class: attention

Please note that Python applications often incorporate non-Python dependencies (created in C/CPP/Rust/GOlang/etc). While the security validation of these external components typically requires specialised tools, a practical approach to identifying vulnerabilities in Python packages—whether they are pure Python or contain code written in other languages is to:

- Audit included non-Python components: Check for known security issues within bundled libraries or binaries.

- Consult vulnerability databases: Search for documented vulnerabilities in a reputable database. For more in-depth information on available search options, refer to the [Security Reference Architecture](https://nocomplexity.com/documents/securityarchitecture/protection/vulnerabilities-search.html#find-vulnerabilities).
:::

## Checking the Number of Used Libraries in a Python Package

Understanding how many third-party libraries a Python package depends on is an important part of security testing. The more dependencies a package has, the larger its attack surface and the higher the potential supply chain risk.

To check the number of libraries used by a package published on PyPI, use:

```bash
codeaudit overview <package-name>
```

Example:

```bash
codeaudit overview requests
```

This command analyses the specified package (as published on PyPI) and provides an overview of:

* Direct dependencies
* Indirect (transitive) dependencies
* Total number of required libraries

### Checking for known vulnerabilities in Python packages

The Python Code Audit `modulescan` command creates a report with valuable security information on used modules.

The `modulescan` command option works per file or package present on PyPI.org

To use `modulescan` feature do:

Generate a module vulnerability report for a Python file::

```bash
codeaudit modulescan <packagename> [yourreportname.html]
```

Example:
```bash
codeaudit modulescan requests
```
With this command all known vulnerabilities for **this package** are reported that are present in the OSV Vulnerability database.

### Checking for known vulnerabilities in a Python file 

```bash
codeaudit modulescan mypythonfile.py
```

With this command **all external libraries** used in this Python file are examined and checked against the OSV Vulnerability database.


When running `codeaudit modulescan` detailed vulnerability information is determined for a Python package or file on:
* **Known** Vulnerability information (**if available**). 
The OSV (Open Source Vulnerability Data is used) for retrieving vulnerability information. OSV is a Google FOSS project to improve the security of FOSS projects. See the [Open Security Architecture](https://nocomplexity.com/documents/securityarchitecture/references/vulnerabilitydatabases.html#vulnerability-databases) for more information.


## Python Security Testing in Practice

As part of a Python security audit:

1. Identify the total dependency footprint using `codeaudit overview`.
2. Assess whether all dependencies are truly necessary.
3. Review high-risk or rarely maintained libraries.
4. Follow up with a vulnerability scan of the detected packages.

Reducing unnecessary dependencies is often one of the simplest and most effective ways to improve the security posture of a Python project.
