---
name: intel-discovery
description: JS intelligence, technology fingerprinting, version extraction, asset attribution. Phase start — surface detection, parameter identification, initial probes. Use when testing INTEL vulnerabilities.
---

# SKILL-INTEL-DISCOVERY — JS Intelligence & App Understanding — DISCOVERY
# Phase Coverage: JS-1, JS-2
# Purpose: Discover and collect JavaScript files, extract hidden endpoints, parameters, and
#          build an application understanding checklist before testing begins.

---

## Philosophy

JavaScript files are the blueprint of the application.
Read them BEFORE testing. They reveal: hidden endpoints, auth logic, business rules,
client-side validation (bypass targets), token handling, and developer mistakes.
JS analysis OVERRIDES and ENRICHES the Surface-to-Vuln Mapping for every surface.

---

## Phase JS-1: Discover and Download All JS Files

```bash
SLUG=$(echo "$TARGET" | sed 's|https\?://||;s|[/:.]|_|g' | tr '[:upper:]' '[:lower:]')
JSDIR=~/agents/acy/fullrecon/${SLUG}/js
mkdir -p "$JSDIR"

# From Burp proxy history
mcp_burp_get_proxy_http_history_regex(regex="\.js(\?|$)")
# → extract all JS URLs from results → download each

# From crawler
cat ~/agents/acy/fullrecon/${SLUG}/katana_endpoints.txt 2>/dev/null \
  | grep -E "\.js(\?.*)?$" | sort -u > "$JSDIR/js_urls.txt"

# Download and beautify each JS file
while read -r url; do
  fname=$(echo "$url" | md5sum | cut -c1-8).js
  curl -sk "$url" -o "$JSDIR/${fname}_raw.js"
  python3 -m jsbeautifier "$JSDIR/${fname}_raw.js" > "$JSDIR/${fname}.js" 2>/dev/null \
    || cp "$JSDIR/${fname}_raw.js" "$JSDIR/${fname}.js"
  echo "$url → $JSDIR/${fname}.js"
done < "$JSDIR/js_urls.txt"

# Source maps (.js.map) — often contain original unminified source
while read -r url; do
  curl -sk "${url}.map" -o "$JSDIR/$(basename $url).map" 2>/dev/null
done < "$JSDIR/js_urls.txt"
```

## Phase JS-2: Extract Hidden Endpoints and Parameters

```bash
cd "$JSDIR"

# jsluice — endpoint and secret extraction
for f in *.js; do
  jsluice urls -u "$TARGET" < "$f" 2>/dev/null >> ../jsluice_endpoints.txt
  jsluice secrets < "$f" 2>/dev/null >> ../jsluice_secrets.txt
done

# linkfinder
python3 /opt/LinkFinder/linkfinder.py -i "$TARGET" -d -o cli 2>/dev/null \
  | tee ../linkfinder_endpoints.txt

# Manual grep patterns
grep -rhoP '"(/[a-zA-Z0-9_/\-\.]+)"' *.js 2>/dev/null | sort -u | tee ../js_paths.txt
grep -rhoP "'(/[a-zA-Z0-9_/\-\.]+)'" *.js 2>/dev/null | sort -u >> ../js_paths.txt
grep -rhioP "(api|endpoint|url|path|route|baseurl)['\"\s:=]+['\"]?https?://[^\s'\"\\]+" *.js \
  | sort -u | tee ../js_api_urls.txt

# Parameter names from JS
grep -rhoP '"([a-zA-Z_][a-zA-Z0-9_]+)"\s*:' *.js 2>/dev/null \
  | sed 's|[":{ ]||g' | sort | uniq -c | sort -rn | head -100 \
  | tee ../js_param_names.txt

# Hidden debug / admin routes
grep -rhi "admin\|debug\|internal\|dev\|staging\|test\|backup\|secret\|private\|config" *.js \
  | grep -iP "route|path|url|endpoint" | tee ../js_hidden_routes.txt
```

---

## App Understanding Checklist

```
□ What type of application is this? (e-commerce, banking, social, API-only, CMS...)
□ What tech stack? (Node/Express, Django, Rails, Laravel, Spring, ASP.NET...)
□ What auth system? (JWT, session cookie, OAuth, API key, basic auth, 2FA...)
□ What database? (MySQL, Postgres, MongoDB, SQLite, Redis as primary...)
□ What does each feature DO? Map inputs → backend logic → outputs
□ Where does money/value flow? (checkout, discount, credit, transfer, reward)
□ Where are privileges enforced? (middleware, per-route, per-object, none?)
□ Where is user-controlled data reflected? (stored vs reflected vs DOM)
□ What business rules exist? (one per user, time-limited, role-gated, quantity limits)
□ What integrations exist? (payment processors, email services, SSO providers, S3...)
□ What APIs are exposed? (REST, GraphQL, WebSocket, gRPC, SOAP...)
□ What AI/LLM features exist? (chat, agent, RAG, embeddings, completions, MCP tools...)
□ What CI/CD pipelines are visible? (GitHub Actions, GitLab CI, Jenkins, exposed .github/...)
□ What cloud infrastructure is detectable? (AWS, GCP, Azure — IMDS reachable, bucket names...)
□ What does the JS tell us? (see JS Intelligence System — always run first)
```

---

## Workflow Map Format

For each feature, write in ~/agents/acy/notes/{SLUG}/{feature}.workflow.md:

```markdown
# {Feature} Workflow

## INPUT
[what the user provides]

## PROCESS
[what the backend likely does]

## OUTPUT
[what comes back]

## STATE
[what changes in the system]

## TRUST
[what assumptions the backend makes about input validity]

## LOGIC
[what business rules apply]

## FLAW
[what could go wrong given the above]

## VULNS
[applicable classes from SURFACE-TO-VULN MAPPING TABLE]
```

---

*SKILL-INTEL-DISCOVERY — Part of the acy Agentic Security Research System v3.0*
