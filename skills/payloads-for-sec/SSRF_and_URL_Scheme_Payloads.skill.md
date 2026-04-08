# SKILL: SSRF and URL Scheme Payloads — Protocol Chains and Bypass Picks

> **AI LOAD INSTRUCTION**: Use this skill when a target makes outbound requests and you need a compact SSRF payload routing set: metadata probes, protocol pivots, host validation bypasses, and scheme selection.

## 1. WHEN TO LOAD THIS SKILL

Load when:

- The server fetches URLs, webhooks, avatars, PDFs, callbacks, or import sources
- You need to select SSRF payloads by trust boundary and protocol support

For deeper exploitation, also load:

- `skills/injection-checking/SSRF_Server_Side_Request_Forgery.skill.md`

## 2. FIRST-PASS PAYLOADS

```text
http://127.0.0.1/
http://localhost/
http://169.254.169.254/latest/meta-data/
http://[::1]/
http://127.1/
```

## 3. HOST VALIDATION BYPASS FAMILIES

| Validation Type | Try |
|---|---|
| blocks `localhost` string | `127.0.0.1`, `127.1`, `[::1]` |
| blocks direct IP only | internal DNS name, decimal/octal/hex IP forms |
| allowlist by prefix | username part, subdomain confusion, redirect chain |
| follows redirects | benign external URL redirecting to internal target |
| parses once, fetches twice | mixed encoding or DNS rebinding style targets |

## 4. PROTOCOL ROUTING

| Goal | Protocol / Target |
|---|---|
| cloud credentials | metadata HTTP endpoints |
| internal HTTP admin | `http://127.0.0.1:port/` |
| Redis / raw TCP style abuse | `gopher://` |
| local file read candidate | `file://` |
| dictionary / banner tests | `dict://` |

## 5. SOURCE POOLS TO CONSULT

- Web-Fuzzing-Box: `Vuln/Api_Bypass/`, `Web/URL/`, `Web/Headers/`
- PayloadsAllTheThings: `Server Side Request Forgery/`

## 6. QUICK CHECKLIST

1. Confirm the fetch primitive and whether redirects are followed.
2. Probe loopback, localhost variants, and cloud metadata.
3. Test one bypass family at a time.
4. If confirmed, switch to the full SSRF skill for chaining and internal service abuse.