---
title: Using AI for Python security testing
short_title: Security testing and AI
---


Many people advocate for the use of AI technology , like AI agents, for Python security testing. 

:::{warning}
Most are just far from good enough. In the best case scenario, you’ll only be disappointed. But the risk of a false sense of security is enormous.
:::

So why should you not use AI powered security test tools for Python?
- **No single tool can judge the context** where a program is used, how it is used and by whom. There is a large difference between using a e.g. a SAST scanner on code from a developer perspective, or to use a SAST scanner as a potential user of some Python software. Based on findings you will and must judge risks differently. Judging risks is always context dependent and can still not be automated. 

+++

- **Limited transparency and trust issues**:  Using non FOSS solutions for cybersecurity is a large risk. Too many closed commercial cyber security solutions have proven to create security disasters instead of mitigating security risks.

+++

- **Security and Privacy Concerns:** Using AI security test tools, especially those that rely on cloud-based Large Language Models (LLMs), can introduce new security and privacy risks. E.g. most AI powered SAST scanners require you to use some insecure AI agent on your code with a connection to a ‘black-box’. Using untrusted AI agents that have a connection to a remote service is a receipt for security and privacy disasters. 

+++


- **AI/ML solutions do not fit every problem.** Or to put it even more clearly: In most cases applying AI is overkill, too expensive, does not work, and other traditional software solutions make far more sense. If it’s possible to structure a set of rules of “if-then scenarios” to handle a problem, then there is usually no need to use AI. And finding static security validation is in essence validation against clear rules. You do not want to worry about enough training data, validity of the result and the fear of looking at results that are created by a hallucinating AI application.
AI and ML technologies can support cyber security, particularly in areas such as DAST (Dynamic Application Security Testing) and the development of more effective fuzzers. However, using AI to assist with software development is fundamentally different from applying fully autonomous AI systems to security testing.

:::{attention}
**Security testing should always be reproducible.** AI technology is based on probabilistic models and advanced statistical methods, whereas security testing is expected to be deterministic. You should be able to repeat the same security test over time and obtain consistent results.

When AI technology is used, strict reproducibility cannot always be guaranteed due to its probabilistic nature.
:::

Cyber security professionals should be conservative with adopting new IT hypes for security testing tools. IT hypes like AI-agents and LLMs are not the holy grail for solving our cybersecurity problems. This is because in the end you always pay more for cyber security solutions, but the risks still remain. Cyber security is not a product, but a process.
