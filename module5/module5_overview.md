---
title: Python Security Testing with Python Code Audit 
short_title: Module 5
---




Security testing is a fundamental part of developing robust and resilient Python applications. Writing functional code is not enough — software must also be designed, reviewed, and tested with security in mind. In this section of the course, we focus on practical techniques to identify vulnerabilities early in the development lifecycle using automated analysis tools.

You will learn how to integrate **Static Application Security Testing (SAST)** into your Python workflow and how to interpret the results from a security perspective. The following sub-sections are covered:

* **Install a SAST for Python**
  Learn how to select and install the best FOSS Static Application Security Testing tool for Python projects and prepare your environment for secure code analysis.

* **Checking Python Dependencies**
  Understand how third-party packages can introduce security risks and how to analyse dependencies for known vulnerabilities.

* **Complexity Check**
  Explore how code complexity impacts security. You will learn how to measure and interpret complexity metrics to identify high-risk files that require closer inspection.

* **SAST Scan**
  Perform a full static security scan of a Python project, analyse findings, prioritise issues, and understand how to remediate them effectively.

By the end of this section, you will be able to systematically analyse Python applications for security weaknesses and integrate automated security testing into your development process.

:::{attention} 
This section uses **Python Code Audit**.
:::

**Python Code Audit** is a Static Application Security Testing (SAST) tool designed to identify security weaknesses in Python source code.

It is a modern Python security analysis tool built on a zero-trust mindset. The tool focuses on detecting security risks, hidden behaviour, and trust boundary violations directly in the source code — without executing it.

:::{important}
Using Python Code Audit is a crucial step when performing security testing on Python applications.
:::
