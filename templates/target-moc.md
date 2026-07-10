---
id: moc-{target-slug}
date: {ISO8601}
type: moc
target: {target-slug}
status: active
tags: [target, {target-slug}, moc]
---

# {Target Name} — Map of Content

## Target Info
- **URL**: {TARGET}
- **Slug**: {SLUG}
- **Program**: {bug_bounty|pentest|vdp|ctf}
- **Scope**: {scope_description}
- **Onboarded**: {ISO8601}

## Tech Stack
- **Frontend**: {React|Vue|Angular|etc.}
- **Backend**: {Node|Django|Rails|Spring|etc.}
- **Database**: {MySQL|Postgres|MongoDB|etc.}
- **Auth**: {JWT|Session|OAuth|API Key|etc.}
- **CDN/WAF**: {Cloudflare|Fastly|Akamai|etc.}
- **Cloud**: {AWS|GCP|Azure|None detected}

## Recon Intelligence
- [[wiki/recon/{slug}/subdomains]] — Discovered subdomains
- [[wiki/recon/{slug}/endpoints]] — All endpoints
- [[wiki/recon/{slug}/js]] — JS intelligence report

## Surface Map
| Surface | Type | Priority Vulns | Status |
|---------|------|---------------|--------|
| {endpoint} | {surface_type} | {vuln_classes} | {pending|testing|completed} |

## Findings Index
| # | Title | Severity | Vuln Class | CIA | Status |
|---|-------|----------|-----------|-----|--------|
| 1 | [[findings/{slug}/{severity}/{class}/{title}/{title}.md]] | {severity} | {class} | C:H I:H | Confirmed |

## Chain Queue
| Chain | Finding A | Finding B | Target Impact | Status |
|-------|----------|----------|--------------|--------|
| {chain_name} | [[F1]] | [[F2]] | {critical|high} | {pending|attempted|confirmed} |

## Session History
| Session | Date | Phases | Findings | Link |
|---------|------|--------|----------|------|
| {session_id} | {ISO8601} | {0-45} | {count} | [[wiki/session/{session_id}]] |

## Knowledge Graph
```mermaid
graph TD
  T[{Target}] --> R[Recon]
  T --> JS[JS Intel]
  R --> S1[Surface 1]
  JS --> S1
  S1 --> F1[Finding 1]
  F1 --> CH[Chain Engine]
```

---

*Target MOC maintained by acy — Agentic Cyber Yield*
