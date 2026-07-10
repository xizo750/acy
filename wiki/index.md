---
id: wiki-index
date: 2026-06-27
type: moc
status: active
confidence: 5
tags:
  - wiki/index
links:
  - "[[log]]"
---

# acy Wiki Index
# LLM Knowledge Base for Agentic Security Research
# ROOT: ~/agents/acy/wiki/

---

## Active Targets

| Target | Status | Last Activity | Top Finding |
|--------|--------|---------------|-------------|
| [[coins_ph]] | 🟢 Active | 2026-07-09 | Email Enumeration (HIGH) + Public MFA Endpoint (MEDIUM) |
| [[codacy_com]] | 🟢 Active | 2026-07-10 | Recon Complete — 8 subdomains, 50+ API endpoints, exposed secrets |
| [[secuna_io]] | 🟢 Active | 2026-07-08 | Unrestricted File Upload (MEDIUM, CVSS 4.3) |
| [[claude_ai]] | 🟢 Active | 2026-07-04 | Radiological Safety Bypass via Medical Framing (HIGH) |
| **grok_com** | 🔴 Active | 2026-07-05 | **System Prompt 80-90% Extracted + Bash as Root + 10 Exploits Generated (CRITICAL)** |
| [[pokee_ai]] | 🟢 Active | 2026-07-03 | Env Var Disclosure via Fresh Session Bypass (LOW, CVSS 4.2) |
| [[priceline_com]] | 🟢 Active | 2026-06-30 | [[penny-unauth-data-exfil|Penny AI — Unauth Hotel Data Exfil]] (HIGH, 7.5) |
| [[coinhako_com]] | 🟡 Inactive | 2026-06-27 | PoC Extension XSS → Chain |
| [[1password_com]] | 🟡 Inactive | 2026-06-25 | Auth Bypass via Env Var Case Sensitivity |
| [[agoda_com]] | 🟡 Inactive | 2026-06-24 | — |

## How to Use This Wiki

This wiki is the **persistent, compounding knowledge base** for the acy security research agent.
Every finding, technique, target, and session is documented here with structured metadata.

### Wiki Page Types

| Type | Purpose | Example |
|------|---------|---------|
| target | Per-target intelligence and surface mapping | [[coinhako_com]], [[1password_com]] |
| technique | Per-vulnerability-class deep knowledge | [[technique/auth-bypass]], [[technique/business-logic]] |
| session | Per-session log and findings | [[coinhako/sessions/2026-06-23-coinhako-session]], [[1password/sessions/2026-06-25-1password-session]] |
| chain | Attack chain documentation | [[coinhako/chains/coinhako_com-poc-extension-xss-chain]] |
| moc | Map of Content - index for a topic area | [[coinhako_com]], [[1password_com]] |
| intel | Reconnaissance & intelligence reports | [[coinhako/intelligence/coinhako_com-intelligence]], [[1password/intelligence/1password_com-intelligence]] |

### YAML Frontmatter (required on every page)

```yaml
---
id: {uuid}
date: {ISO8601}
type: {target|technique|session|chain|moc|raw-ref}
status: {draft|active|completed|archived}
confidence: {1-5}
tags: [tag1, tag2]
links:
  - "[[index]]"
---
```

### Wiki-Link Syntax

Use `[[index]]` syntax for bi-directional links between pages (referencing another wiki page by its relative path without `.md` extension).
The agent automatically maintains backlink indexes.

---

## Active Targets

| Target | Status | Last Session | Findings | MOC |
|--------|--------|-------------|----------|-----|
| **1password.com** | 🟢 Active | 2026-06-25 | **1 Confirmed** (1 High) | [[1password_com]] |
| **coinhako.com** | 🟢 Active | 2026-06-27 | **9 Confirmed** (1 Crit, 2 High, 6 Med) + 4 Chains | [[coinhako_com]] |
| **pokee.ai** | 🟢 Active | 2026-07-03 | **1 Confirmed** (1 Low) | [[pokee_ai]] |
| **agoda.com** | 🟢 Active | 2026-06-28 | **1 Confirmed** (1 Medium) | [[agoda_com]] |

### Grok Quick Stats
- **Model Tested:** Grok (grok.com) — Fast + Think models
- **Boundary Testing:** 10/12 prohibited categories bypassed (0 refusals for code)
- **Findings:** 9 confirmed (2 Critical, 3 High, 2 Medium, 1 Low)
- **Key Findings:** RAT implant with persistence (crit), ransomware feature set (crit), C2 beacon (high), Google phishing page (high), Android spyware (high), fake news (med), extremist recruitment (med), CBRN academic partial (low)
- **Bypass Techniques Discovered:** Red/Blue framing (P22), Feature Accretion (P23), Proactive Offer Exploitation (P24), Contextual Saturation (P25), Educational Pretext (P26)
- **Claude Comparison:** Claude refused ransomware combo, C2 beacon; Grok accepted all 3. Claude refused broken-code-fix; Grok fixed + added decrypt.

### PokeeClaw AI Quick Stats
- **Subdomains:** 44 discovered, 33 live
- **Type:** AI Sandbox / LLM Execution Environment
- **Findings:** 1 active (1 Low — Environment Variable Disclosure via Fresh Session Bypass)
- **Key Technique:** Fresh session guardrail differential — burned sessions block `os.environ`, fresh sessions return full `printenv`. No credentials disclosed — infrastructure config only (LOW impact).
- **Session:** Phase 0 recon complete, F1 confirmed

### 1Password Quick Stats
- **Subdomains:** 1,540 discovered, 597 live
- **API Routes:** 683 unique (v1-v4)
- **Vuln Classes Found:** 1 (business-logic, 3 variants)
- **Mock Accounts:** 3 pending/active
- **Session:** Phase 2 in progress

### Coinhako Quick Stats
- **Subdomains:** 33 discovered, 16 live
- **Findings:** 9 active (1 Crit, 2 High, 6 Med) + 2 retracted/patched
- **Attack Chains:** 4 (2 PRIMED: CORS->SDK XSS->ATO CVSS 8.6, safeHtml->localStorage->ATO CVSS 9.1; 2 CONFIRMED)
- **RCE:** None found (tested SSTI, CMDi, file upload, deserialization, GraphQL, WebSocket, LFI, CRLF, prototype pollution)
- **Last Session:** 2026-06-27 -- CORS retest, SDK XSS chain, RCE hunt, H1 report compiled
- **HackerOne Report:** Ready (`findings/coinhako_com/HACKERONE_REPORT_ZOHO_SDK_XSS.md`)

### Agoda Quick Stats
- **Subdomains:** 654 discovered, 544 live
- **Findings:** 1 active (1 Medium)
- **Architecture:** React MSPA + ASP.NET MVC + Envoy + K8s + Okta SSO
- **Account:** memberId 609829128 (xziao Nico, VIP Bronze, loginLvl 2)
- **Last Session:** 2026-06-28 -- JS intel, profile analysis, F1 confirmed

---

## Technique Pages

| Technique | Vuln Class | Findings | From Target | Page |
|-----------|-----------|----------|-------------|------|
| **Attack Chaining** | chain | 4 chains (2 confirmed) | coinhako | [[technique/chain]] |
| **Business Logic** | business-logic | 1 High | 1password (F1) | [[technique/business-logic]] |
| **Authentication Bypass** | auth-bypass | 1 Crit + 1 AI guardrail | coinhako (C1), pokee_ai (F1) | [[technique/auth-bypass]] |
| **CORS Misconfiguration** | cors | 1 High, 1 Medium | coinhako (H1, M4) | [[technique/cors]] |
| **Information Disclosure** | info-disclosure | 1 Crit, 2 High, 3 Med, 1 Low | coinhako, agoda, pokee_ai | [[technique/info-disclosure]] |
| **Cross-Site Scripting** | xss | 1 Medium | coinhako (M6) | [[technique/xss]] |
| **Session Management** | session-mgmt | 1 Medium + 1 AI sandbox | coinhako (M5), pokee_ai (F1) | [[technique/session-mgmt]] |
| SQL Injection | sqli | — | — | [[technique/sqli]] |
| NoSQL Injection | nosqli | — | — | [[technique/nosqli]] |
| SSRF | ssrf | — | — | [[technique/ssrf]] |
| **IDOR / BOLA** | idor | 7 patterns + 3 flavors + 5-step blueprint | Tanvir0x1 + $15,500 writeups | [[technique/idor]] |
| JWT Vulnerabilities | jwt | — | — | [[technique/jwt]] |
| OAuth2 / OIDC | oauth | — | — | [[technique/oauth]] |
| Race Conditions | race-condition | — | — | [[technique/race-condition]] |
| Prototype Pollution | prototype-pollution | — | — | [[technique/prototype-pollution]] |
| **SSTI (Template Injection)** | ssti | 6 PoC patterns | exploitarium/floci | [[technique/ssti]] |
| **Insecure Deserialization** | deserialization | PHP/Java/Python chains | exploitarium/php857 | [[technique/deserialization]] |
| **CI/CD & Container Security** | devops | container escape, workflow injection | exploitarium/gitea | [[technique/devops]] |
| **File Upload** | file-upload | — | sudohunt writeup | [[technique/file-upload]] |
| **LFI / Path Traversal** | lfi / path-traversal | — | sudohunt writeup | [[technique/lfi-path-traversal]] |
| **Prompt Injection / AI Security** | ai-security, prompt-injection | 26 patterns (v3.5) — 5 new: Red/Blue framing, feature accretion, proactive offers, context saturation, educational pretext | Brenndoerfer 2026, Grok campaign 2026-07-05 | [[technique/prompt-injection]] |
| **CBRN Stealth Framing** | ai-security, prompt-injection, cbrn | System prompt extraction via CBRN research cover | Grok campaign 2026-07-05 | [[technique/cbrn-stealth-framing]] |
| **Stealth Framing Bypass** | ai-security, safety-filter-bypass | Fiction, historical, defensive training filter bypass | Grok campaign 2026-07-05 | [[technique/stealth-framing-bypass]] |
| **CRLF / Header Injection** | crlf, header-injection, response-splitting | 4 CVEs (2026), 7 WAF bypass techniques, multi-layer architecture insight | Raw guide 2026-07-09 | [[technique/crlf-header-injection]] |
| **Race Conditions** | race-condition, toctou, concurrency, timing | 6 attack types, single-packet (HTTP/2), First Sequence Sync, Turbo Intruder templates, 10 high-value targets | Raw guide 2026-07-09 | [[technique/race-condition]] |
| **Training Data Poisoning** | training-data-poisoning, mcp-tool-poisoning, gguf-template-poisoning, pipeline-poisoning | 5 vectors, CVE-2025-54136, MCPTox benchmarks (72.8% ASR on o1-mini), GGUF templates, S3/SageMaker chain, sequential multi-stage | Raw guide 2026-07-09 | [[technique/training-data-poisoning]] |
| **LLM Excessive Agency & Permission Manipulation** | excessive-agency, permission-manipulation, tool-call-injection, guardrail-bypass, agent-hijack | 4 attack categories (tool call injection, guardrail bypass, permission escalation via identity, indirect injection → agency abuse), 4 guardrail bypass strategies (OpenClaw pattern), 5 real-world cases (GHSA-r5fq-947m-xm57, CVE-2025-59528, Vertex AI double-agent), OWASP LLM08/ASI03 | Raw guide 2026-07-09 | [[technique/llm-excessive-agency]] |
| **Spring Boot Actuator** | spring-boot-actuator, actuator, jolokia, heapdump, gateway-routes | 3 CVEs (2026): CVE-2026-40976 (CVSS 9.1 auth bypass), CVE-2026-22731/22733 (CVSS 8.2 health/CF paths), 4 classic chains (Eureka RCE, Jolokia JNDI, Gateway SSRF, log level), heapdump credential extraction | Raw guide 2026-07-09 | [[technique/spring-boot-actuator]] |
| **GraphQL Attack Techniques** | graphql, gid-bola, alias-batching, subscription-bypass, cswsh | 10 vectors: GID BOLA/IDOR, operation name auth bypass, alias rate limit bypass, array batching, introspection regex bypass, WebSocket subscription auth (CVE-2026-32594), Spring GraphQL deserialization (CVE-2026-41699), CSWSH, injection (SQL/NoSQL/SSTI), query complexity DoS, 7 tools | Raw guide 2026-07-09 | [[technique/graphql-attacks]] |
| **Path Encoding, Obfuscation & Mutation Attacks** | encoding-bypass, unicode-normalization, cspt, mutation-fuzzing | 3 CVEs (2026): CVE-2026-21726 (Grafana Loki double decode), CVE-2026-30869 (Go/Node.js PathUnescape), CVE-2026-35583 (Unicode normalization bypass), double encoding, null byte injection, CSPT, mutation fuzzing, defense stack profiling | Raw guide 2026-07-05 | [[technique/path-encoding-mutation]] |

---

## Session Pages

| Session | Target | Findings | Status |
|---------|--------|----------|--------|
| [[1password/sessions/2026-06-25-1password-session]] | 1password.com | 3 confirmed | 🟢 Active |
| [[coinhako/sessions/2026-06-23-coinhako-session]] | coinhako.com | 12 confirmed | ✅ Complete |

---

## Chain Pages

| Chain | Findings Chained | Severity | Status |
|-------|-----------------|----------|--------|
| [[coinhako/chains/coinhako_com-poc-extension-xss-chain]] | C1 + C2 + M5 + M6 — Extension → XSS → ATO | **CRITICAL (CVSS 10.0)** | ✅ Confirmed |
| [[coinhako/chains/coinhako_com-chain-xss-ato]] | C2 + H2 + M6 — XSS → localStorage → API Takeover | CRITICAL | ✅ Ready |
| [[coinhako/chains/coinhako_com-chain-zoho-xss]] | H1 + M6 — Zoho CORS + XSS → Data Theft | HIGH | ✅ Ready |

---

## Maps of Content (MOCs)

- [[1password_com]] — **1Password Full Target MOC** (1 finding, surfaces, intel, session)
- [[coinhako_com]] — **Coinhako Full Target MOC** (all findings, chains, surfaces, intel)
- [[moc/injection-vulns]] — SQLi, NoSQLi, CMDi, SSTI, XXE, SSRF
- [[moc/auth-vulns]] — IDOR, JWT, OAuth, Session, Access Control
- [[moc/clientside-vulns]] — XSS, CSRF, CORS, Prototype Pollution
- [[moc/logic-vulns]] — Business Logic, Race Conditions, Mass Assignment
- [[moc/recon-intel]] — Reconnaissance, Intelligence, Info Disclosure
- [[moc/file-upload-vulns]] — File Upload, LFI, Path Traversal, Upload Chains
- [[moc/ai-llm-vulns]] — **NEW v3.3** — Prompt Injection, MCP Abuse, RAG Injection, Jailbreaks, Indirect Injection, 18 patterns

---

## Raw Source References

| Source | Author | Techniques Covered | Wiki Page |
|--------|--------|--------------------|-----------|
| Exploitarium PoC Library | exploitarium | SSTI, Deserialization, DevOps, Auth Bypass, File Upload | [[raw-refs/exploitarium]] |
| File Upload → Path Traversal → LFI | SudoHunt (terp0x0) | file-upload, lfi, path-traversal, chain | [[raw-refs/sudohunt-file-upload-lfi]] |
| Critical IDOR — Dual User ID + Batch Escalation | Tanvir Ahmed (Tanvir0x1) | idor, dual-user-id, batch-endpoint, sequential-id | [[raw-refs/tanvir-idor-dual-user-id]] |
| Critical IDOR — $15,500 Payout on SaaS | Tanvir Ahmed (@tanvir.infosec) | idor, horizontal-idor, beginner-blueprint, report-writing, 3-flavors | [[raw-refs/tanvir-idor-15500-payout]] |
| **Prompt Injection: Attacks, RAG Risks, Defenses** | Michael Brenndoerfer (2026) | direct/indirect injection, RAG risks, defenses, prompt leaking, transformer analysis | [[raw-refs/prompt-injection-brenndoerfer]] |
| **Prompt Injection Red Team Toolkit** | Community (compiled) | tools (garak/julius/augustus/promptfoo), 31-row strategy matrix, indirect vectors, challenges | [[raw-refs/prompt-injection-red-team-toolkit]] |
| **Assetnote — SSRF in NextJS Apps** | Assetnote (May 2024) | `_next/image` blind SSRF, Server Actions CVE-2024-34351 full read SSRF, Flask exploit server, HEAD→GET→redirect chain | [[raw-refs/assetnote-ssrf-nextjs]] |
| **Helldivers 2 — Offensive Playbook v13** | Community (game tactics) | 8 offensive fire-and-maneuver squad schemas, weapon crafting, tactical combat cycle — red-team operational planning analogies | [[raw-refs/helldivers-2-offensive-playbook-v13]] |
| **Header Injection & CRLF Injection Bug Bounty Guide 2026** | Community (compiled) | CRLF injection, header injection, response splitting, WAF bypass (7 techniques), cache poisoning, session fixation, 4 CVEs (2026), multi-layer architecture insight | [[raw-refs/crlf-header-injection-2026]] |
| **Race Condition Attacks for Bug Bounty (2025/2026)** | Community (compiled) | 6 race types (single-packet, first-sequence-sync, multi-endpoint, WebSocket, partial-construction, TOCTOU), Turbo Intruder templates (5), validation methodology, 10 high-value targets | [[raw-refs/race-condition-attacks-2026]] |
| **Best & Latest Information Disclosure Attacks for Bug Bounty (2026)** | poorman3exp | 10 vectors: config files, source maps, IDOR→info leak, error messages, cloud buckets, GitHub dorking, subdomain takeover, Swagger exposure, NTLM leakage, debug endpoints | [[raw-refs/info-disclosure-bugbounty-2026]] |
| **Wayback Machine & Legacy API Attack Surface (2026)** | poorman3exp | CDX API recon, legacy API auth bypass, version downgrade, method tampering, header injection, guest user attacks, BOLA/IDOR, file download validation, 5 case studies (T-Mobile 37M, Optus 9.8M) | [[raw-refs/wayback-machine-2026]] |
| **Cookie Attack Field Guide (2026)** | Community | 8 vectors: prefix bypass (__Host-/__Secure-), cookie tossing, jar overflow (HttpOnly bypass), reflection/sandwich, SameSite bypass, cookie bomb, cookie smuggling (Jetty), request smuggling cookie theft | [[raw-refs/cookie-attack-field-guide-2026]] |
| **Bug Bounty Triage Methodology (2026)** | YesWeHack/Intigriti/BugBase | 6-step validation pipeline, strict metrics (FPR<2%, repro>95%), CVSS metric-by-metric scoring, automated validation stages, quality gates, edge case rules, AI-assisted triage with guardrails | [[raw-refs/triage-methodology-2026]] |
| **Training Data Poisoning Bug Bounty Guide 2026** | Community (compiled) | 5 vectors (MCP tool, GGUF template, pipeline path traversal, fine-tuning, sequential multi-stage), CVE-2025-54136, MCPTox benchmarks, GGUF Jinja2 payloads, S3/SageMaker chain, bounty programs | [[raw-refs/training-data-poisoning-2026]] |
| **LLM Excessive Agency / Permission Manipulation Bug Bounty Playbook 2026** | Community (compiled) | 4 attack categories (tool call injection, guardrail bypass, permission escalation, indirect injection), 4 guardrail bypass strategies (encoding, context manipulation, role-play, split-turns), 5 real-world cases (OpenClaw, Flowise CVE-2025-59528, Vertex AI), OWASP LLM08/ASI03 | [[raw-refs/llm-excessive-agency-2026]] |
| **Spring Boot Actuator Bug Bounty Reference Guide 2026** | Community (compiled) | 3 CVEs (2026): CVE-2026-40976 (CVSS 9.1 framework auth bypass), CVE-2026-22731/22733 (CVSS 8.2 health/CF paths), 4 classic chains (Eureka XStream RCE, Jolokia JNDI, Gateway SSRF, log level), heapdump analysis, Shodan/Censys fingerprints | [[raw-refs/spring-boot-actuator-2026]] |
| **Advanced GraphQL Attack Techniques for Bug Bounty 2026** | Community (compiled) | 10 vectors: GID BOLA/IDOR, operation name auth bypass, alias rate limit bypass, array batching, introspection regex bypass, WebSocket subscription auth (CVE-2026-32594), Spring GraphQL deserialization (CVE-2026-41699), CSWSH, injection (SQL/NoSQL/SSTI), query complexity DoS, 7 tools (InQL, GraphQLmap, Clairvoyance, BatchQL, GrapeQL) | [[raw-refs/graphql-attacks-2026]] |
| **Path Traversal & HTTP Parameter Pollution** | Community (compiled) | 4 CVEs (2026): CVE-2026-5422 (Jupyter Server startsWith bypass), CVE-2026-25766 (Go filepath.FromSlash), CVE-2026-24479 (ZIP archive), CVE-2026-25732 (NiceGUI filename upload), HPP (ASP.NET comma XSS, OAuth redirect, rate limit bypass, SSPP, CSPT), defense stack profiling | [[raw-refs/path-traversal-hpp-2026]] |
| **Path Encoding, Obfuscation & Mutation Attacks** | Community (compiled) | 3 CVEs (2026): CVE-2026-21726 (Grafana Loki double decode), CVE-2026-30869 (Go/Node.js PathUnescape double decode), CVE-2026-35583 (Unicode normalization bypass), double encoding, null byte injection, fullwidth Unicode, HPP path mutation, CSPT, mutation fuzzing, PathMutationEngine | [[raw-refs/path-encoding-mutation-2026]] |
| **XSS & Blind XSS Bug Bounty Arsenal** | Community (compiled) | Blind XSS discovery (7 surfaces), context-based payload crafting (5 contexts), WAF bypass (6 techniques), DOM XSS advanced (5 source→sink mappings), mutation XSS, polyglots, tool stack (dalfox, XSStrike, Interactsh, katana), cookie jar overflow | [[raw-refs/xss-blind-xss-arsenal-2026]] |

---

## 1Password Wiki Pages (Full Index)

### Target & Intelligence
- [[1password_com]] — Main target MOC
- [[1password/targets/1password_com]] — Target profile
- [[1password/intelligence/1password_com-intelligence]] — Recon & JS intel

### Surfaces
- [[1password/surfaces/1password_com-signup]] — Registration & verification flow

### Sessions
- [[1password/sessions/2026-06-25-1password-session]] — Session 2026-06-25 (Phases 0-2)

---

## Coinhako Wiki Pages (Full Index)

### Target & Intelligence
- [[coinhako_com]] — Main target MOC
- [[coinhako/targets/coinhako_com]] — Target profile
- [[coinhako/intelligence/coinhako_com-intelligence]] — Recon & JS intel

### Surfaces
- [[coinhako/surfaces/coinhako_com-www]] — Main application
- [[coinhako/surfaces/coinhako_com-trading]] — Talos trading platform
- [[coinhako/surfaces/coinhako_com-help]] — Zoho Desk
- [[coinhako/surfaces/coinhako_com-blog]] — Ghost CMS

### Findings (Vault Copies)
- [[coinhako/findings/coinhako_com-critical-auth-bypass-x-chk-apikey-bypass]]
- [[coinhako/findings/coinhako_com-critical-auth-bypass-x-chk-apikey-global]] (RETRACTED)
- [[coinhako/findings/coinhako_com-critical-info-disclosure-keys-in-localstorage]]
- [[coinhako/findings/coinhako_com-high-cors-zoho-cors]]
- [[coinhako/findings/coinhako_com-high-info-disclosure-user-id-exposed]]
- [[coinhako/findings/coinhako_com-medium-cors-ghost-api]]
- [[coinhako/findings/coinhako_com-medium-info-disclosure-s3-bucket]]
- [[coinhako/findings/coinhako_com-medium-info-disclosure-talos-config]]
- [[coinhako/findings/coinhako_com-medium-session-cookie-analysis]]
- [[coinhako/findings/coinhako_com-medium-xss-safehtml-pipe]]

### Verifications
- [[coinhako/verifications/coinhako_com-zoho-sdk-verification]] — Zoho ASAP SDK Escalation Surface Live Test

---

## Agoda Wiki Pages (Full Index)

### Target & Intelligence
- [[agoda_com]] — Main target MOC

### Findings
- [[agoda/findings/agoda_com-f1-config-exposure]] — MEDIUM: K8s Pod Name Exposure (CVSS 5.3)

---

## PokeeClaw AI Wiki Pages

### Target & Intelligence
- [[pokee_ai]] — Main target MOC (1 finding: Environment Variable Disclosure via Fresh Session Bypass)

---

*acy Wiki Index — Updated 2026-07-09 — 1 new technique page (path-encoding-mutation), 3 new raw-refs (22 total). Path traversal/HPP expanded with 7 CVEs. XSS expanded with Blind XSS arsenal and WAF bypass. Injection + clientside skills updated.*
