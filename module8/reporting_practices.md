---
title: Prioritisation for Managers and CEOs
short_title: Risk-Based Reporting 
---

Severity alone does not determine priority. Risk-based reporting connects technical vulnerabilities to business impact.
This module teaches you to think beyond “High, Medium, Low” and instead communicate in terms executives understand: risk exposure and risk reduction.


## Prioritisation for Managers and CEOs

:::{hint} 
Executives are concerned with **risk, cost, and reputation**, not stack traces.
:::


### Translate Technical Risk into Business Impact

Instead of:

> “Improper deserialisation allows arbitrary object instantiation.”

Say:

> “An attacker could gain full control of our customer data platform.”

Focus on:
* Financial impact
* Legal exposure
* Reputational damage
* Operational disruption
* Customer trust

### Risk-Based Prioritisation Model

Combine:
* CVSS score
* Asset value
* Data sensitivity
* Exploit likelihood
* Public exposure

Example categories:
| Priority | Description |
| -------- | ----------------------------------------------------- |
| Critical | Internet-facing, exploitable, sensitive data exposure |
| High | Privileged access required but significant impact |
| Medium | Limited exposure or partial impact |
| Low | Defence-in-depth or hard-to-exploit |

Provide:
* A ranked summary table
* Estimated remediation effort
* Suggested remediation timeline
This enables informed decision-making at board level.


### Developer-Friendly Feedback

Security testing should enable developers, not antagonise them.

Principles:
* Avoid blame (“The developer failed to…”)
* Be precise and technical
* Provide working secure examples
* Reference Pythonic best practice

Good Developer Feedback Example:

Instead of:

> “Input validation is broken.”

Provide:
* Explanation of the flaw
* Minimal vulnerable snippet
* Secure rewrite
* Link to framework guidance
* Suggested unit test case

Example:

**Issue**: Direct string interpolation in SQL query.

**Fix**: Use parameterised queries.

```python
# Vulnerable
cursor.execute(f"SELECT * FROM users WHERE id = {user_id}")
# Secure
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
```

Developers appreciate:
* Reproducible evidence
* Clear remediation patterns
* Alignment with existing architecture
* Practical, incremental fixes
Security becomes collaborative rather than adversarial.


### Driving Remediation

Reporting is only the beginning. Effective testers ensure findings are resolved.
Recommended Follow-Up Strategies:
1. **Remediation Tracking**
* Log issues in Jira/Azure DevOps
* Assign owners
* Set realistic deadlines
2. **Retesting**
* Validate fixes
* Confirm no regression
* Update severity if risk posture changes
3. **Remediation SLAs**
* Critical: e.g. 7–14 days
* High: 30 days
* Medium: 60–90 days
* Low: next release cycle
4. **Trend Analysis**
* Recurring vulnerability types
* Framework misuse patterns
* Training gaps
5. **Security Enablement**
* Targeted developer workshops
* Secure coding guidelines
* Pre-commit security tooling
* CI/CD integration with SAST/DAST tools
6. **Executive Reporting Dashboards**
* Open vs closed vulnerabilities
* Mean time to remediate (MTTR)
* Risk reduction over time


## Key Takeaways

Effective reporting:
* Translates technical findings into business risk
* Uses structured, reproducible documentation
* Applies consistent severity scoring
* Prioritises based on real-world impact
* Empowers developers with clear, actionable fixes
* Ensures follow-through until remediation is complete
In professional Python security testing, discovering vulnerabilities demonstrates technical competence.
Communicating them clearly—and driving their resolution—demonstrates maturity.

