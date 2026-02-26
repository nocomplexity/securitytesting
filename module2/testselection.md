# Use the right tool for the right test


## Selecting a tool for security testing of Python code

In essence, the following security tests are commonly applied to Python code:

- {ref}`subsection1`

- {ref}`subsection2`

- {ref}`subsection3`

- {ref}`subsection4`: Focuses on implementation and design decisions, often combined with a secure code review using SAST tools.

- {ref}`subsection5`:Evaluates the system architecture, including the context in which the system is developed, deployed, and maintained, from a security perspective.

:::{admonition} **There is no single “perfect” security test.** 
:class: important

Security testing can and should be done on different aspects, based on your risk assessment.
However, there are straightforward automated test solutions for common cybersecurity challenges that are effective.

**There is no single ‘magic’ tool capable of automatically validating all risks.**

The best testing solutions are open source and meet minimum quality standards, such as the [OpenSSF Best Practices requirements](https://www.bestpractices.dev/en).
:::


The most reliable cybersecurity solutions are open and accessible to everyone. Good solutions are based on proven practices rather than hype.

Ultimately, the most effective way to ensure a Python program is secure is to validate both its design or architecture and its implementation.


(subsection1)=
### Static Application Security Testing (SAST)

* **Definition:** SAST analyses source code, bytecode, or binaries **without running the program**.

* **Purpose:** It detects vulnerabilities in the Python code itself, such as input validation issues, hard-coded secrets, or unsafe function usage.
* **How it works:**

  * Scans the code for patterns known to be insecure.
  * Often integrated into development pipelines (CI/CD).

**Example:** Detecting Python calls that can cause security vulnerabilities in Python code before deployment.


(subsection2)=
### Dynamic Application Security Testing (DAST)

* **Definition:** DAST tests an **Python application while it is running** to identify security vulnerabilities.
* **Purpose:** It simulates real-world attacks to check how the application behaves under malicious input or unexpected conditions.
* **How it works:**

  * Sends test inputs or HTTP requests to the running application.
  * Monitors responses for signs of vulnerabilities like XSS, SQL injection, or authentication flaws.

**Example:** Testing a Python web application by sending malicious form inputs to check for cross-site scripting or insecure redirects.

![SAST versus DAST](/images/sast_vs_dast.png)

(subsection3)=
### Supply chain vulnerability checks (dependencies)


**Supply Chain Vulnerability Checks (Dependencies) for Python Software**:

**Definition:**
Supply chain vulnerability checks focus on identifying security risks in the **third-party libraries and dependencies** your Python software relies on. In Python, these are usually packages installed via tools like `pip` or listed in `requirements.txt` or `pyproject.toml`.

**Why it matters:**

* Most Python applications use multiple external libraries.
* A vulnerability in a single dependency can **compromise the entire application**, even if your own code is secure.
* Attackers often target widely used libraries because this gives them access to many projects (“**supply chain attacks**”).

**How it works:**

* Automated tools scan your project’s dependencies.
* They check for known vulnerabilities reported in databases like **PyPI advisories** or the **CVE (Common Vulnerabilities and Exposures) database**.
* They may also identify outdated packages that could introduce risk.

**Examples:**

* Using an outdated version of `requests` with a known remote code execution vulnerability.
* A maliciously altered package in PyPI (e.g., a typosquatted package designed to inject malware).



Even if your Python code is perfect, your software is only as secure as the packages it depends on. Supply chain checks help **ensure all dependencies are safe and up to date**.


:::{danger} 
A check against known vulnerabilities is a historical assessment—it only evaluates past threats. This approach is intrinsically limited when addressing modern supply chain attacks , which can introduce malicious code during the build or deployment process, bypassing checks based on static lists of known flaws.
:::

:::{tip}
In practice you should be careful with Python packages that have lots of dependencies and also non Python artefacts in the builds. A supply chain attack on a pure Python Package is possible when a project has no QA and strong governance procedures, so *mr.malware* can get commit rights and packages with malware can be uploaded to PyPI. But also mind the risk that a build machine can be compromised or build is created using a malicious CI pipeline.
:::

![supply chain security](/images/supplychainsecurity.png)

:::{tip}
A simple way to discover **Python** dependencies for a package can be done using **Python Code Audit**. 

In module 4 you will learn how this feature can be used.
:::

(subsection4)=
### Secure design review

Use when:

- Designing new features

- Making architectural or implementation changes

- Before major releases

Purpose:

- Review design decisions and implementation choices

- Often combined with SAST and human inspection

Best for:
- Preventing structural security weaknesses

(subsection5)=
### Security Architecture Review

A security architecture helps in the continuous process of optimizing and controlling your security risks.

Use when:

- Designing or redesigning system architecture

- Before major platform or infrastructure changes

- During compliance or risk assessments

Purpose:

- Evaluate overall system architecture

- Assess deployment, operational context, and trust boundaries

Best for:
- Ensuring systemic and long-term security resilience