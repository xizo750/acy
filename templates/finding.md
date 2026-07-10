---
id: {uuid}
date: {ISO8601}
type: finding
status: confirmed
confidence: 5
severity: {critical|high|medium|low}
cia: {C:H/I:H/A:H}
target: {target-slug}
vuln_class: {class}
surface: {endpoint}
links:
  - [[wiki/target/{slug}]]
  - [[wiki/technique/{class}]]
  - [[wiki/session/{session_id}]]
---

# {Impact-First Title}

## Summary
[One paragraph: what the bug is and why it matters]

## Impact
- **Confidentiality**: [C rating] — [explanation with specific data types affected]
- **Integrity**: [I rating] — [explanation with specific state/action affected]
- **Availability**: [A rating] — [explanation; note only for DoS — never trigger in prod]

## Affected Endpoints
- `{METHOD} {URL}` — [what the endpoint does]
- [additional endpoints if chain]

## Steps to Reproduce

### Step 1: [Action]
```bash
curl -sk -X {METHOD} "{TARGET}{ENDPOINT}" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{payload}'
```

**Response:**
```json
{response showing the vulnerability}
```

### Step 2: [Verification]
[How to confirm the impact — actual data accessed, action performed, etc.]

## Evidence

### Request
```
{full HTTP request}
```

### Response
```
{full HTTP response showing the bug}
```

### Screenshot / Console Output
```
{console output or tool output proving impact}
```

## PoC Script
See: `{title}.sh`

## Chain Potential
| Chain Partner | Chain Result | Severity |
|--------------|-------------|----------|
| [other finding or vuln class] | [combined impact] | [critical/high] |

## Remediation
[Specific, actionable fix steps]
1. [Fix 1]
2. [Fix 2]

---

*Finding validated by acy — Agentic Cyber Yield — Confidence: {score}/5*
