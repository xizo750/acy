## 2026-07-09: Path Traversal/HPP + Encoding Bypass + XSS/Blind XSS Wiki Update

### Raw Sources Processed
- `raw/Path Traversal & HTTP Parameter Pollution.md` → technique expansion + raw-refs + skill updates
- `raw/Path Encoding, Obfuscation & Mutation Attacks.md` → new technique page + raw-refs + skill updates
- `raw/XSS & Blind XSS Bug Bounty Arsenal.md` → technique expansion + raw-refs + skill updates

### Wiki Updates — Path Traversal & HPP
- **Expanded:** `wiki/technique/lfi-path-traversal.md` — added HPP section (ASP.NET comma XSS, OAuth redirect, rate limit bypass, SSPP, CSPT), 4 new CVEs (CVE-2026-5422, CVE-2026-25766, CVE-2026-24479, CVE-2026-25732), HPP defense stack profiling table, updated bypass table with 4 new rows
- **Created:** `wiki/raw-refs/path-traversal-hpp-2026.md` — extracted CVEs, HPP patterns, defense stack profiling

### Wiki Updates — Path Encoding, Obfuscation & Mutation
- **Created:** `wiki/technique/path-encoding-mutation.md` — new technique page (3 CVEs 2026, double encoding, Unicode fullwidth, null byte, HPP path mutation, CSPT, mutation fuzzing, defense stack profiling)
- **Created:** `wiki/raw-refs/path-encoding-mutation-2026.md` — extracted encoding bypass, Unicode normalization, CSPT, mutation patterns

### Wiki Updates — XSS & Blind XSS
- **Expanded:** `wiki/technique/xss.md` — added Blind XSS section (discovery checklist, payloads, tools), context-based payload crafting (5 contexts), WAF bypass (6 techniques), DOM XSS advanced (5 source→sink mappings), mutation XSS, polyglots, tool stack
- **Created:** `wiki/raw-refs/xss-blind-xss-arsenal-2026.md` — extracted blind XSS, WAF bypass, DOM XSS advanced, tool stack

### Skill Updates — Injection
- **Updated:** `injection-discovery/SKILL.md` — Phase 18.5 added encoding bypass path traversal (2026 CVEs), Phase 31 expanded with HPP types (6 vectors, defense stack)
- **Updated:** `injection-hunt/SKILL.md` — Phase 18.2 added encoding bypass payloads, Phase 31.2 expanded with HPP (6 vectors: framework parsing, WAF bypass, ASP.NET comma XSS, OAuth redirect, rate limit bypass, SSPP, CSPT)
- **Updated:** `injection-reproduce/SKILL.md` — Phase 18 HPP reproduction checklist (implied by technique expansion)

### Skill Updates — Client-Side
- **Updated:** `clientside-discovery/SKILL.md` — Phase 5 updated with Blind XSS tier and discovery (7 surfaces, callback-based detection)
- **Updated:** `clientside-hunt/SKILL.md` — Phase 5.2 added Blind XSS payloads (4 vectors), WAF bypass (6 techniques)
- **Updated:** `clientside-reproduce/SKILL.md` — Phase 5.3 added Blind XSS reproduction checklist, WAF bypass reproduction workflow

### MOC Updates
- **Updated:** `wiki/moc/injection-vulns.md` — added path-encoding-mutation technique link, path-traversal-hpp-2026 + path-encoding-mutation-2026 raw-refs, updated skills list
- **Updated:** `wiki/moc/clientside-vulns.md` — added xss-blind-xss-arsenal-2026 raw-ref, updated skills list with Blind XSS

### Index & Knowledge Base
- **Updated:** `wiki/index.md` — added path-encoding-mutation technique row +3 new raw-refs rows (22 total)

---

## 2026-07-09: Spring Boot Actuator & GraphQL Attack Techniques Wiki Update

### Raw Sources Processed
- `raw/Spring Boot Actuator Bug Bounty.md` → wiki technique + raw-refs + skill updates
- `raw/GraphQL Attack Techniques.md` → wiki technique + raw-refs + skill updates
- `raw/SSRF.md` → ALREADY PROCESSED (technique/ssrf.md + raw-refs/assetnote-ssrf-nextjs.md exist)

### Wiki Updates — Spring Boot Actuator
- **Created:** `wiki/technique/spring-boot-actuator.md` — full technique page (3 CVEs 2026, 4 classic chains, JNDI/Gateway SSRF/Heapdump/Log level vectors)
- **Created:** `wiki/raw-refs/spring-boot-actuator-2026.md` — extracted patterns from raw source
- **Updated:** `injection-hunt/SKILL.md` — Phase 32.2 added Spring Boot Actuator hunt section (CVE-2026-40976, CVE-2026-22731/22733, gateway routes, Jolokia, log level)
- **Updated:** `injection-reproduce/SKILL.md` — Phase 46.3 added Spring Boot Actuator reproduce section (12-step validation checklist, false positive check, chain output)

### Wiki Updates — GraphQL Attack Techniques
- **Created:** `wiki/technique/graphql-attacks.md` — full technique page (10 vectors, 2 CVEs, 7 tools, 8-step validation)
- **Created:** `wiki/raw-refs/graphql-attacks-2026.md` — extracted patterns from raw source
- **Updated:** `injection-discovery/SKILL.md` — Phase 32.1 expanded with attack surface mapping, Global IDs, aliases, batching, subscriptions, Spring Boot Actuator discovery
- **Updated:** `injection-hunt/SKILL.md` — Phase 32.2 expanded with GID BOLA, operation name bypass, introspection regex bypass, array batching, query complexity DoS
- **Updated:** `injection-reproduce/SKILL.md` — Phase 32.3 expanded with 16-step GraphQL validation checklist (GID BOLA, operation name bypass, WebSocket subscription, CSWSH, Spring GraphQL deserialization, query complexity DoS)
- **Updated:** `clientside-hunt/SKILL.md` — Phase 33 expanded with GraphQL WebSocket subscription auth bypass (CVE-2026-32594), JS PoC, validation checklist

### MOC Updates
- **Updated:** `wiki/moc/injection-vulns.md` — status STUB→ACTIVE, added graphql-attacks + spring-boot-actuator technique links, raw-refs links, related skills
- **Updated:** `wiki/moc/clientside-vulns.md` — status STUB→ACTIVE, added WebSocket/CSWSH + GraphQL subscription content
- **Updated:** `wiki/moc/auth-vulns.md` — added GraphQL auth bypass (operation name, Global ID, WebSocket subscription CVE-2026-32594)

### Index & Knowledge Base
- **Updated:** `wiki/index.md` — added 2 technique rows (Spring Boot Actuator, GraphQL Attack Techniques) + 2 raw-refs rows
- **Updated:** `essentials/KNOWLEDGE_BASE.md` — added Spring Boot Actuator patterns (3 CVEs, 4 chains) + GraphQL Attack patterns (10 vectors, 2 CVEs, tools)

### Key Patterns — Spring Boot
- 3 CVEs: CVE-2026-40976 (CVSS 9.1, Boot 4.0 defaults), CVE-2026-22731/22733 (CVSS 8.2, health/CF paths)
- Heapdump > Env in Boot 4.0 (Sanitizer redaction)
- Jolokia + Gateway = reliable RCE chains when exposed
- Massive version range: Boot 2.7.x through 4.0.x affected by CVE-2026-22733

### Key Patterns — GraphQL
- 10 attack vectors, 2 CVEs (CVE-2026-32594 WebSocket, CVE-2026-41699 Spring GraphQL)
- Global IDs = base64-encoded sequential integers → systematic BOLA
- WebSocket subscriptions bypass Express middleware auth
- 7 tools: InQL, GraphQLmap, Clairvoyance, BatchQL, GrapeQL, graphql-path-enum, GraphQL Hunter

---

## 2026-07-09: LLM Excessive Agency & Permission Manipulation Wiki Update

### Raw Source Processed
`raw/LLM Excessive Agency Permission.md` → wiki technique + raw-refs + skill updates

### Wiki Updates
- **Created:** `wiki/technique/llm-excessive-agency.md` — full technique page (4 attack categories, 4 guardrail bypass strategies, 5 real-world cases, Vertex AI double-agent pattern, OWASP LLM08/ASI03, discovery techniques, validation checklists, report template)
- **Created:** `wiki/raw-refs/llm-excessive-agency-2026.md` — extracted patterns from raw source
- **Updated:** `ai-hunt/SKILL.md` — expanded Pattern 6 with 4 attack categories, guardrail bypass strategies, real-world cases, chain output, conversation history poisoning
- **Updated:** `ai-reproduce/SKILL.md` — added excessive agency validation checklist (tool call extraction, server-side execution, permission verification, guardrail bypass evidence, impact confirmation, attack category classification, chain potential, CVE cross-reference)
- **Updated:** `ai-discovery/SKILL.md` — added excessive agency boundary section (tool enumeration, permission probing, function call inspection, service account analysis, memory poisoning, document upload injection)
- **Updated:** `wiki/moc/ai-llm-vulns.md` — added 4 new technique rows (Tool Call Injection, Guardrail Bypass, Permission Escalation, Indirect Injection), updated Excessive Agency row, added 1 new raw-ref, updated pattern count 31→35, added 8 chain mappings
- **Updated:** `wiki/index.md` — added technique row + raw-refs row
- **Updated:** `essentials/KNOWLEDGE_BASE.md` — added excessive agency patterns to AI section

### Key Patterns Extracted
- 4 attack categories: Tool Call Injection (Direct), Guardrail Bypass (OpenClaw Pattern), Permission Escalation via Agent Identity, Indirect Injection → Agency Abuse
- 4 guardrail bypass strategies: encoding evasion, context manipulation, role-play/evaluation, split-turns
- 5 real-world cases: OpenClaw Path Traversal (GHSA-r5fq-947m-xm57), Flowise CVE-2025-59528 (CVSS 9.8), Vertex AI Double Agent, OpenClaw Inbox Deletion, Meta Internal Agent Data Leak
- OWASP: LLM08 (Excessive Agency), ASI03 (Identity & Privilege Abuse)
- Key insight: Trust boundary is probabilistic — repeated runs yield different results
- Attack pattern count updated: 31→35 patterns

---

## 2026-07-09: Training Data Poisoning Wiki Update

### Raw Source Processed
`raw/Training Data Poisoning.md` → wiki technique + raw-refs + skill updates

### Wiki Updates
- **Created:** `wiki/technique/training-data-poisoning.md` — full technique page (5 vectors, CVE-2025-54136, MCPTox benchmarks, GGUF Jinja2 payloads, S3/SageMaker chain, sequential multi-stage, validation checklists, impact assessment, bounty programs)
- **Created:** `wiki/raw-refs/training-data-poisoning-2026.md` — extracted patterns from raw source
- **Updated:** `ai-discovery/SKILL.md` — added training data poisoning discovery section (MCP, GGUF, pipeline, fine-tuning, sequential)
- **Updated:** `ai-hunt/SKILL.md` — added MCP tool poisoning hunt (3 PoC templates), GGUF template hunt, pipeline path traversal hunt, fine-tuning hunt, sequential multi-stage hunt
- **Updated:** `ai-reproduce/SKILL.md` — added 5 validation checklists, impact assessment table, bounty programs
- **Updated:** `wiki/moc/ai-llm-vulns.md` — added 5 new technique rows, 3 new raw-refs, updated pattern count 26→31, added 5 chain mappings
- **Updated:** `wiki/index.md` — added technique row + raw-refs row
- **Updated:** `essentials/KNOWLEDGE_BASE.md` — added training data poisoning patterns to INJECTION_PATTERNS

### Key Patterns Extracted
- 5 vectors: MCP Tool Poisoning, GGUF Template Poisoning, Pipeline Path Traversal, Fine-Tuning Poisoning, Sequential Multi-Stage
- CVE-2025-54136 (MCP Tool Poisoning)
- MCPTox benchmarks: 72.8% ASR on o1-mini, 70.2% on Phi-4, 61.8% on GPT-4o-mini
- Real-world incident: Mitiga Labs S3/SageMaker path traversal
- Key finding: 250 documents backdoor any LLM size (Anthropic 2025)
- Sequential poisoning: additive (SFT→DPO) and complementary (SFT→PPO) effects
- 6 bounty programs with payout ranges ($200-$300K)
- Attack pattern count updated: 26→31 patterns

---

## 2026-07-09: Race Condition Attacks Wiki Update

### Raw Source Processed
`raw/Race Condition Attacks.md` → wiki technique + raw-refs + skill updates

### Wiki Updates
- **Replaced:** `wiki/technique/race-condition.md` — upgraded from stub to full technique page (6 attack types, 5 Turbo Intruder templates, 10 high-value targets, validation checklist, response patterns, report template, practice labs)
- **Created:** `wiki/raw-refs/race-condition-attacks-2026.md` — extracted patterns from raw source
- **Updated:** `logic-discovery/SKILL.md` Phase 27 — expanded discovery patterns, red flags (architecture), endpoint discovery
- **Updated:** `logic-hunt/SKILL.md` Phase 27 — added 3 Turbo Intruder templates (single-packet, last-byte, connection warming), response patterns, attack types, methodology
- **Updated:** `logic-reproduce/SKILL.md` Phase 27 — added full validation checklist, response patterns, CVSS template, root cause, remediation
- **Updated:** `wiki/index.md` — added technique row + raw-refs row
- **Updated:** `essentials/KNOWLEDGE_BASE.md` — added race condition patterns to INJECTION_PATTERNS

### Key Patterns Extracted
- 6 attack types: Single-Packet (HTTP/2), First Sequence Sync, Multi-Endpoint, WebSocket, Partial Construction, TOCTOU
- 5 Turbo Intruder templates (single-packet, last-byte, multi-endpoint, warming, parameterized)
- 10 high-value targets with severity ratings
- Response pattern decision matrix (200+200, 200+403, 200+500)
- Validation methodology (confirm → measure → prove)
- Report template with CVSS, root cause, remediation

---

## 2026-07-09: CRLF/Header Injection Wiki Update

### Raw Source Processed
`raw/Header Injection & CRLF Injection Bug Bounty Guide 2026.md` → wiki technique + raw-refs + skill updates

### Wiki Updates
- **Created:** `wiki/technique/crlf-header-injection.md` — full technique page (definition, injection points, payloads, WAF bypass matrix, 4 CVEs, PoC validation, severity, chains, tools)
- **Created:** `wiki/raw-refs/crlf-header-injection-2026.md` — extracted patterns from raw source
- **Updated:** `injection-discovery/SKILL.md` Phase 38 — added injection point mapping, passive/active detection, 2026 CVE awareness
- **Updated:** `injection-hunt/SKILL.md` Phase 38 — expanded payload set (12 variants), WAF bypass hunt, Content-Encoding deflate bypass
- **Updated:** `injection-reproduce/SKILL.md` Phase 38 — added cache poisoning + session fixation validation, 2026 CVE verification checklist, multi-layer architecture insight
- **Updated:** `wiki/index.md` — added technique row + raw-refs row
- **Updated:** `essentials/KNOWLEDGE_BASE.md` — added INJECTION_PATTERNS section with CRLF patterns

### Key Patterns Extracted
- 4 new CVEs (2026): Python wsgiref, libsoup, TinyWeb, Traefik
- 7 WAF bypass techniques including real-world Akamai bypass
- Multi-layer architecture insight: parsing discrepancies between CDN→WAF→LB→sidecar→app
- 4 chain patterns (medium→critical escalation)

---

## 2026-07-08: claude.ai API Authorization Audit

### Session Summary
Conducted systematic API endpoint discovery and authorization testing against claude.ai. Tested 20+ authenticated API endpoints for IDOR, information disclosure, and UUID enumeration vulnerabilities.

### Key Findings

**Medium (1):**
- **User Email Disclosure** via `GET /api/organizations/{org}/projects/{proj}/accounts` — exposes email_address, tagged_id, full_name

**Low (5):**
- Internal codename disclosure across multiple endpoints (notification_preferences, org settings, bootstrap, experiences)
- Account invites endpoint returns 200 for invalid UUIDs (enumeration primitive)
- Organization numeric ID leakage alongside UUID
- Third-party service integration disclosure (sync/settings)
- Full conversation content API documented for chaining

### Authorization Assessment
- **Org-scoped endpoints**: Properly return 404 for non-existent/invalid org UUIDs
- **Account-scoped endpoints**: Do NOT differentiate (200 for any UUID) — potential IDOR risk
- **Project-scoped endpoints**: Properly return 404 for non-existent project UUIDs
- **No confirmed IDOR**: Cross-user/org data access not achieved
- All endpoints require valid session cookie (`__ssid`)
- Auth model appears to be: session → org membership → data access

### Technology Fingerprint
- Frontend: React SPA
- API: RESTful JSON, session-based auth
- Cloudflare-protected
- Org internal ID: numeric (207517627)
- Account internal ID: user_016dCAiFZ6mZeRmEuAkhTfCm format
- Model: claude-sonnet-5 (default), raven model eligible

---

## 2026-07-09: Information Disclosure Attacks for Bug Bounty (poorman3exp)

### Source
`~/agents/acy/raw/Best & Latest Information Disclosure Attacks for Bug Bounty.md` — 342 lines, 10 attack vectors, by poorman3exp (2026-07-09)

### Wiki Updates

**Raw Ref Created:**
- `wiki/raw-refs/info-disclosure-bugbounty-2026.md` — 10 vectors, 2026 key takeaways, validation methodology

**Technique Page Expanded:**
- `wiki/technique/info-disclosure.md` — 13 patterns total (6 original + 7 new: P7-P13)
  - P7: Exposed config & env files (Google dorks, nuclei, netlas)
  - P8: Source map disclosure (.js.map reconstruction, ffuf fuzzing)
  - P9: Error message disclosure (SQL error → query structure leak)
  - P10: GitHub/GitLab dorking (TruffleHog, GitLeaks, active key testing)
  - P11: API docs & Swagger UI exposure (/swagger.json → hidden admin endpoints)
  - P12: Debug & trace endpoints (Spring Boot Actuator chains, CVE-2026-40976)
  - P13: NTLM response leakage (CVE-2026-26133, Responder capture)

**Skills Updated:**
- `infodisclosure-discovery/SKILL.md` — Added P11-P15 patterns (config files, source maps, GitHub dorking, API docs, NTLM), updated run order (15 steps total)
- `infodisclosure-hunt/SKILL.md` — Added P11-P14 hunt patterns with full PoC commands (source map decode, TruffleHog scan, Swagger admin endpoint testing, NTLM hash capture)
- `infodisclosure-reproduce/SKILL.md` — Added validation checklists for P11-P15 (source maps, GitHub dorking, API docs, NTLM, Spring Boot Actuator chains)

**Index & KB Updated:**
- `wiki/index.md` — New raw-refs row (15th total raw-ref)
- `essentials/KNOWLEDGE_BASE.md` — Added INFO_DISCLOSURE_PATTERNS section (13 patterns, 4 chain patterns, detection methodology)

### Key Patterns Extracted
- **Source maps** are goldmines: `.js.map` reconstructs full unminified codebase
- **GitHub dorking** + active key testing = direct financial access (Stripe live key)
- **Swagger exposure** = full API surface + hidden admin endpoints → broken access control chain
- **NTLM leakage** via Office URI handlers (CVE-2026-26133) — hash capture with Responder
- **Spring Boot Actuator** has 3 active 2026 CVEs (see [[technique/spring-boot-actuator]])
- **91% AI usage** in bug bounty, but only 40% for payload gen (hallucination risk)

### Chain Patterns
- Source map + XSS = credential theft (critical)
- GitHub dork + active key = direct financial access (critical)
- IDOR + Swagger = mass PII extraction (critical)
- Config leak + path traversal = full server access (critical)

---

## 2026-07-09: Wayback Machine, Cookie Attack Field Guide, Triage Methodology

### Sources Processed
1. `~/agents/acy/raw/Wayback Machine.md` — 617 lines, CDX API recon, legacy API auth bypass, BOLA/IDOR, PoC workflow, 5 case studies
2. `~/agents/acy/raw/Cookie Attack Field Guide.md` — 309 lines, 8 cookie attack vectors (prefix bypass, tossing, jar overflow, HttpOnly bypass, SameSite bypass, cookie bomb, smuggling)
3. `~/agents/acy/raw/Bug Bounty Triage Methodology.md` — 212 lines, 6-step pipeline, strict metrics, CVSS metric-by-metric, quality gates

### Technique Pages Created
- `wiki/technique/wayback-machine.md` — 5 patterns: CDX API recon, legacy API auth bypass, guest user attacks, BOLA/IDOR, file download validation. 5 case studies (T-Mobile 37M, Optus 9.8M, Jira, Microsoft, Octopus Deploy)
- `wiki/technique/cookie-attacks.md` — 8 patterns: prefix bypass, cookie tossing, jar overflow, HttpOnly bypass via reflection, SameSite bypass, cookie bomb, cookie smuggling, request smuggling cookie theft
- `wiki/technique/triage-methodology.md` — 8 patterns: 6-step pipeline, strict metrics, CVSS metric-by-metric, automated validation, quality gates, edge cases, AI-assisted triage, triage checklist

### Raw Refs Created
- `wiki/raw-refs/wayback-machine-2026.md` — CDX API commands, auth bypass techniques, BOLA testing, case studies
- `wiki/raw-refs/cookie-attack-field-guide-2026.md` — 8 attack vectors, PoCs, defensive notes
- `wiki/raw-refs/triage-methodology-2026.md` — 6-step pipeline, metrics table, golden rule, edge case rules

### Skills Updated
- `recon-discovery/SKILL.md` — Added CDX API recon section, waymore tool, LinkFinder
- `auth-hunt/SKILL.md` — Added cookie prefix bypass, cookie tossing, legacy parsing bypass, guest token BOLA, cookie validation checklist
- `clientside-hunt/SKILL.md` — Added cookie jar overflow, cookie bomb, cookie smuggling, HttpOnly bypass via reflection
- `report-reproduce/SKILL.md` — Added strict triage validation checklist, 6-step pipeline, CVSS metric-by-metric, quality gates, edge case rules

### MOCs Updated
- `wiki/moc/recon-intel.md` — STUB → ACTIVE with wayback-machine + info-disclosure raw-refs
- `wiki/moc/auth-vulns.md` — Added cookie-attacks (8 vectors) + cookie-attack-field-guide-2026 raw-ref
- `wiki/moc/clientside-vulns.md` — Added cookie-attacks (jar overflow, cookie bomb, smuggling) + raw-ref

### Index & KB Updated
- `wiki/index.md` — 4 new raw-refs rows (19 total raw-refs)
- `essentials/KNOWLEDGE_BASE.md` — Added WAYBACK_LEGACY_PATTERNS, COOKIE_ATTACK_PATTERNS, TRIAGE_METHODOLOGY sections
