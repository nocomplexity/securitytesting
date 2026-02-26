# Evaluating Open Source Software

Open source components are central to Python ecosystems. However, their adoption introduces supply chain and governance risks.

In this section, you will learn how to:

* Assess the security maturity of open source projects
* Evaluate maintenance activity and community responsiveness
* Identify red flags in dependency selection
* Align technical findings with business risk considerations

The goal is to move beyond blind dependency inclusion and towards informed, risk-based decision-making.


Free and Open Source Software (FOSS) is not automatically more secure than proprietary software. However, the availability of source code makes independent evaluation of its security properties possible. Transparency enables inspection, analysis, and verification—provided that you take the time to assess it properly.

As a Python developer, before adopting any Open Source Software (OSS) dependency or tool, you should identify suitable candidates and evaluate them systematically against your technical, security, and sustainability requirements.

Below is a structured approach to evaluating an OSS dependency from a security validation perspective.


## Can You Avoid Adding It?

Every dependency increases your attack surface.

* Can existing dependencies (direct or indirect) already provide the required functionality?
* Can the functionality reasonably be implemented in-house with less risk?
* What additional transitive dependencies will be introduced?

A compromised dependency—or one of its transitive dependencies—may compromise your entire system.


## Are You Evaluating the Intended Version?

Ensure you are assessing the legitimate and intended project, not a malicious fork or attacker-controlled lookalike. This helps defend against *typosquatting* attacks.

Practical checks:

* Verify the project name and official website.
* Confirm the repository ownership and fork relationships on platforms such as GitHub or GitLab.
* If the project claims affiliation with a foundation, confirm this via the foundation’s official website.
* Review its creation date and popularity metrics (stars, forks, downloads).
* Confirm that you are analysing the exact version you intend to deploy.

---

## Is It Actively Maintained?

Unmaintained software is a significant risk. Most software requires ongoing updates to address vulnerabilities and compatibility issues.

Consider:

* Has there been meaningful activity (e.g. commits) within the last year?
* When was the last release published?
* Is there more than one maintainer, ideally from different organisations?
* Are maintainers responsive to issues and pull requests?
* Does the version string suggest instability (e.g. starting with “0”, or labelled “alpha” or “beta”)?

Dormant projects are more likely to accumulate unpatched vulnerabilities.



## Do the Developers Demonstrate Secure Development Practices?

Look for evidence that security is treated as a first-class concern.

You may:

* Check whether the project has earned, or is progressing towards, an Open Source Security Foundation (OpenSSF) Best Practices badge.
* Review its metadata on deps.dev, including its OpenSSF Scorecard results and known vulnerabilities.
* Determine whether dependencies are regularly updated.
* Look for documented security design rationale (sometimes referred to as an assurance case).
* Examine whether automated tests run within a CI pipeline and review test coverage levels.
* Assess how quickly security issues are fixed.
* Check whether security patches are backported to supported releases.
* Determine whether long-term support (LTS) versions exist.
* Confirm use of hosting platform security controls (e.g. branch protection rules).
* Review any published security audits and whether findings were addressed.

Security maturity is reflected not only in documentation, but in consistent, observable behaviour.



## Is It Easy to Use Securely?

Software that is difficult to configure securely often leads to insecure deployments.

Evaluate:

* Are default configurations secure?
* Do example configurations enable encryption and authentication by default?
* Does the API design encourage secure usage (e.g. support for parameterised queries)?
* Is there clear guidance on secure configuration and usage?

Secure-by-default design is a strong positive indicator.



## Is There a Clear Vulnerability Reporting Process?

A responsible project should:

* Provide documented instructions for reporting vulnerabilities.
* Offer a private disclosure channel.
* Publish security advisories when appropriate.

The absence of a reporting process suggests weak security governance.



## Does It Have Significant Real-World Use?

Widespread usage does not guarantee security. However:

* Popular projects are more likely to be reviewed by many parties.
* More users increase the likelihood that vulnerabilities will be discovered and reported.
* A similarly named but more popular package may indicate a typosquatting attempt.

Popularity should inform—but not replace—your evaluation.


## What Is the Licence?

Licensing is not directly a security issue, but it affects sustainability and compliance.

* Ensure every component has a clearly stated licence.
* Confirm it is an OSI-approved licence (see Open Source Initiative).
* Verify compatibility with your intended use.
* Be cautious of projects that lack clear licensing information.

Projects that neglect licensing clarity may also neglect other governance practices.



## What Do Code-Level Evaluation Results Show?

Even a limited review can provide valuable insight.

When examining the source code:

* Is there evidence of secure development practices (e.g. input validation, parameterised queries)?
* Are there numerous unresolved `TODO` comments suggesting incomplete work?
* What issues are reported by static analysis tools?
* Is there evidence of malicious behaviour?

The academic study Backstabber’s Knife Collection highlights common supply chain attack techniques. In particular:

* Inspect installation scripts for suspicious behaviour.
* Check for attempts to access `~/.ssh`, environment variables, or other sensitive data.
* Look for encoded or obfuscated payloads.
* Review recent commits carefully—malicious changes are often introduced shortly before release.

Where appropriate:

* Run the software in a sandboxed environment.
* Execute all defined test cases.
* Review any publicly documented security assessments.



## Key Principle

Evaluating FOSS Python package for security defects is not a one-time activity. It is a continuous validation process. Security posture can change as maintainers change, dependencies evolve, and new vulnerabilities emerge.

In security testing for Python systems, dependency evaluation is not optional—it is a core supply chain defence mechanism.

