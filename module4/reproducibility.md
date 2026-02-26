---
title: Reproducibility in SAST for Python
short_title: Reproducibility
---


Reproducibility is essential in Static Application Security Testing (SAST) of Python code to ensure that findings are reliable, verifiable and comparable over time.

A reproducible environment ensures that the test can be repeated under the same technical conditions. This includes using a clearly defined Python version and a controlled dependency setup (for example, via a virtual environment or container). Without environmental consistency, results may vary due to changes in interpreter behaviour or library versions.

Tests must be repeatable by other team members or external auditors or researchers. This requires documented setup steps and automated dependency installation (e.g. via a `requirements.txt`, lock file or environment specification). The objective is that another person can execute the same SAST process and obtain equivalent results.

It is critical to collect and retain version information for all software components involved in the SAST test. This includes:

* Python interpreter version
* All installed Python packages and their versions
* SAST tool name and version
* Operating system (where relevant)

Capturing this information ensures traceability, supports audits and enables accurate comparison of results across different testing cycles.


:::{note} 
[**Python Code Audit**](https://nocomplexity.com/codeaudit/) is created with reproducibility in mind. 
For every test the used version number is reported, as well as other crucial meta data. 
:::
