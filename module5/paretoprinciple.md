---
title: 80/20 rule and Python Security Testing
short_title: 80/20 rule 
---


The [Pareto principle](https://en.wikipedia.org/wiki/Pareto_principle),  also known as the 80/20 rule, states that, for many outcomes, roughly 80% of consequences come from 20% of causes. This will mean for Cyber Security defects that 80% of the security breaches come from only 20% of all possible causes.

From a business perspective translating the 80/20 rule for cyber security **testing** would mean that 80% of security benefits can be achieved by focusing on 20% of the causes or efforts. 

OWASP Top 10 is an excellent example that shows that of all possible security weaknesses only a small percentage still leads to the majority of security breaches. The OWASP Top 10 project analyses CVE and calculates an impact score.

![pareto principle](/images/pareto.png)

Security Testing is complex and resources available are never endless. So security testing for Python should focus on:

- Always perform a SAST test (Static Application Security Testing) on Python code before running. Despite complex dependency chains that are also possible for Python packages, a SAST test will give a quick view for security code aspects that deserve attention.

+++

- Validate if and how security by design is applied. 

+++

- Ensure a threat model is created and that a risk-based approach is followed for all security test performed.

The threat model identifies the impact, while the risk-based approach determines the priority.

![risk-based](/images/riskbased.jpeg)