# Skill Template

## Metadata

```yaml
---
id: SKILL-{NAME}
version: 1.0
date: {ISO8601}
status: active
phase: {phase_number}
vuln_classes: [{comma-separated}]
dependencies: [{skill_files}]
---
```

## Phase {N}: {Vuln Class Name} — CIA: {C:H/I:H/A:H}

```
TRIGGER: [What surface or condition activates this skill]
SURFACE TYPES: [What kinds of endpoints/features to test]
```

### SUB-PHASE {N}.1: DISCOVERY

**Passive:**
  - [What to look for in JS, config, headers without sending payloads]
  - [Patterns to grep, signs of the technology]

**Active:**
  - [Probes to confirm the technology/endpoint exists]
  - [What responses confirm presence]

### SUB-PHASE {N}.2: HUNT

**Standard Payloads:**
```bash
# [Description of the test]
for payload in \
  "payload1" \
  "payload2"; do
  RESP=$(curl -sk "$TARGET/endpoint?param=$payload")
  echo "$RESP" | grep -q "success_pattern" && echo "[VULN HIT]"
done
```

**Complex/Advanced Payloads:**
```bash
# [WAF bypass, filter evasion, chained exploitation]
```

### SUB-PHASE {N}.3: REPRODUCE

**Confirm:** [What proves the vulnerability is real, not a false positive]
**PoC Script:** save to scripts/{SLUG}/{vuln_class}_{surface}.sh
**Save finding:** findings/{SLUG}/{severity}/{vuln-class}/{title}/

**CHAIN OUTPUT:**
  → [Vuln A] + [Vuln B] = [Escalated Impact] (severity)

---

## Tool Reference

| Tool | Purpose | When to Use |
|------|---------|-------------|
| tool_name | what it does | when to use it |

---

## Validation Checklist

```
□ Can the vulnerability be reproduced consistently?
□ Is the impact demonstrable (not just an anomaly)?
□ Is there a chain candidate?
□ Is the finding documented with CIA ratings?
□ Is the PoC script clean and executable?
```

---

*SKILL-{NAME} — {Vuln Class} Module*
*Part of the acy — Agentic Cyber Yield skill system*
