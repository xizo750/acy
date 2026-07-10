---
id: {uuid}
date: {ISO8601}
type: session
target: {target-slug}
phase: {current_phase}
status: {active|completed|paused}
---

# Session: {ISO8601} — {Target} — Phase {N}

## Session Summary
- **Target**: {TARGET}
- **Slug**: {SLUG}
- **Phase Started**: {phase_number}
- **Phase Ended**: {phase_number}
- **Surfaces Tested**: {count}
- **Findings Confirmed**: {count}
- **Chains Attempted**: {count}
- **Time Active**: {duration}

## State at Start
- **Last Phase**: {phase_number}
- **Last Surface**: {endpoint}
- **Queue Size**: {count}
- **Pending Chains**: {count}

## Actions Taken
| Time | Action | Result |
|------|--------|--------|
| {timestamp} | [Action description] | [Result/HTTP code/finding] |

## Findings Confirmed This Session
| # | Title | Severity | Vuln Class | CIA |
|---|-------|----------|-----------|-----|
| 1 | [Title] | [Critical] | [sqli] | C:H I:H |

## Dead Ends / Near Misses
| Endpoint | Vuln Class | Reason |
|----------|-----------|--------|
| [endpoint] | [class] | [why it wasn't exploitable] |

## State at End
- **Next Phase**: {phase_number}
- **Next Surface**: {endpoint}
- **Queue Remaining**: {count}
- **Pending Chains**: {count}

## Knowledge Base Updates
- [New patterns discovered]
- [Wiki pages created/updated]

## Operator Notes
[Any observations, WAF behavior, unusual responses, research leads]

---

*Session recorded by acy — Agentic Cyber Yield*
