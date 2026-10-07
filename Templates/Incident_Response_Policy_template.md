# Incident Response Policy (Template)

Security incidents happen even to well-run, well-intentioned projects. A short,
clear incident response policy turns a stressful, ad-hoc scramble into a
practiced, predictable process — and signals to users, downstream consumers,
and compliance reviewers (e.g. under the EU Cyber Resilience Act) that the
project takes security seriously.

This does not need to live in its own file. For most projects it fits
naturally as a section in `SECURITY.md`, or as a page in existing
documentation (e.g. `docs/incident-response.md`). A few paragraphs is enough
for a small project; larger projects may want more detail and named roles.

## Why adopt this

- Incidents are a matter of "when," not "if." Having a plan in place reduces
  response time and limits damage.
- A documented process helps contributors and users know what to expect and
  where to report concerns.
- It demonstrates security maturity to downstream users, auditors, and
  regulators at minimal cost to maintain.

## Template

```markdown
## Incident Response Policy

### Scope
This policy covers security incidents affecting this project, including its
source code, infrastructure, release pipeline, maintainer accounts, and
contributor trust.

### What constitutes an incident
- Unauthorized code changes (e.g. a malicious commit or compromised
  maintainer account)
- Leaked secrets, credentials, or signing keys
- A vulnerability being actively exploited in the wild
- Compromised build or release infrastructure
- A compromised endpoint belonging to someone with repository or release
  access

### Reporting a security issue
- Report to: <security@example.org>, or via a private security advisory on
  GitHub
- Please do not open a public issue for an active exploit or a leaked secret
- Reports are acknowledged within [X] business days

### Response process
1. **Triage** — Confirm the incident, assess its scope and severity.
2. **Contain** — Revoke credentials, roll back affected commits, pull
   releases, rotate keys as needed.
3. **Eradicate** — Fix the root cause and patch the vulnerability.
4. **Recover** — Restore normal operations; re-issue a release if required.
5. **Disclose** — Notify affected users and publish an advisory, following
   coordinated disclosure practices.
6. **Review** — Conduct a post-incident review and document follow-up
   actions to prevent recurrence.

### Roles and responsibilities
- Incident lead: [name/role]
- Communications: [name/role]
- Technical response: [name/role]

### Contact and escalation
[Maintainer email addresses, chat channel, PGP keys if applicable]
```

## Illustrative examples

**Compromised endpoint (lost or stolen device)**
A maintainer's laptop is lost or stolen, and it was not protected with full
disk encryption. SSH keys, Git credentials, and signing keys stored on the
device are now potentially exposed. A documented incident response policy
ensures someone is responsible for promptly revoking the affected keys,
forcing re-authentication on CI/CD systems, and rotating any credentials the
device had access to — rather than the exposure going unnoticed for weeks.

**The XZ Utils backdoor (2024)**
Over a period of roughly two years, an attacker using the identity "Jia Tan"
built credibility within the xz-utils community, was granted co-maintainer
status, and ultimately inserted a backdoor into the project's build scripts
that targeted OpenSSH. The compromise was discovered largely by chance,
rather than through a defined process. This incident illustrates that
insider threat and social engineering are real risks for open source
projects, and that an incident response policy should account for
compromised maintainers, require review of sensitive changes (such as build
and CI configuration), and provide a clear path for reporting suspicious
contributor behavior.

## Recommendations

- Keep contact and escalation details current; outdated contact information
  delays response.
- Link this section prominently from `SECURITY.md` so it is easy to find.
- A concise policy is far more valuable than no policy — start simple and
  expand it as the project matures.
