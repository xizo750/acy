---
name: report-discovery
description: PoC development, finding reports, triage, verification, pre-submit hardening. Phase start — surface detection, parameter identification, initial probes. Use when testing REPORT vulnerabilities.
---

# SKILL-REPORT-DISCOVERY — PoC Development & Report Writing Discovery — DISCOVERY
# Phase Coverage: 44
# Purpose: Verification checklist and honest triage rules for pre-submit hardening

---

## Phase 44: Verification + Pre-Submit Hardening

```
TRIGGER: After all surfaces tested, before any submission.
RUNS: Once per confirmed finding before it leaves the agent.
```

### Pre-Submit Checklist

```
PRE-SUBMIT CHECKLIST (every finding MUST pass):
  [ ] Reproducible: Can the PoC script run from a fresh terminal and produce the same result?
  [ ] Impact demonstrated: Does the PoC show actual data modification, unauthorized access, or value manipulation?
  [ ] No false positive: Is the result definitely a bug, not a WAF anomaly or normal behavior?
  [ ] Scope verified: Is the target in scope for the current engagement?
  [ ] No PII storage: Is any PII in the PoC output redacted or minimal?
  [ ] Clean PoC: Is the PoC script free of unnecessary noise, comments explain each step?
  [ ] Chain evaluated: Has Phase 42 (Chain Engine) been run on this finding?
  [ ] Wiki linked: Does the finding note link to the target MOC and technique wiki pages?
  [ ] CIA rated: Is Confidentiality/Integrity/Availability impact explicitly rated?
```

### Honest Triage

```
HONEST TRIAGE:
  If a finding does NOT pass all checks -> do NOT report. Log as near-miss in wiki.
  If impact is self-only and no escalation path -> do NOT report. Log in wiki.
  If finding is informational only (missing header, version disclosure) -> do NOT report.
  If finding requires unlikely user action (self-XSS with no delivery mechanism) -> do NOT report.
```

---

*SKILL-REPORT-DISCOVERY — Part of the acy Agentic Security Research System v3.0*
