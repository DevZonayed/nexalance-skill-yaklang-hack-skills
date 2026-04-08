# SKILL: API Auth and JWT Abuse — Token Trust, Header Tricks, and Rate Limits

> **AI LOAD INSTRUCTION**: Use this skill when APIs rely on JWT, bearer tokens, API keys, or weak request identity signals. Focus on token trust boundaries, claim misuse, header spoofing, and rate-limit bypass.

## 1. TOKEN TRIAGE

Inspect:

- `alg`, `kid`, `jku`, `x5u`
- role, org, tenant, scope, or privilege claims
- issuer and audience mismatches
- reuse of mobile and web tokens across products

## 2. QUICK ATTACK PICKS

| Pattern | First Test |
|---|---|
| `alg:none` acceptance | unsigned token with trailing dot |
| RS256 confusion | switch to HS256 using public key as secret |
| `kid` lookup trust | path traversal or injection in `kid` |
| remote key fetch trust | attacker-controlled `jku` or `x5u` |
| weak secret | offline crack with targeted wordlists |

## 3. RATE LIMIT BYPASS FAMILIES

```text
X-Forwarded-For
X-Real-IP
Forwarded
User-Agent rotation
Path case / slash variants
```

## 4. NEXT ROUTING

- For GraphQL batching and hidden parameters: `GraphQL_and_Hidden_Parameters.skill.md`
- For default credential and brute-force planning: `skills/payloads-for-brute/Brute_Wordlist_Selection.skill.md`
- For full JWT and OAuth depth: `skills/auth-sec/JWT_OAuth_Token_Attacks.skill.md`
- For OAuth or OIDC configuration flaws in browser and SSO flows: `skills/auth-sec/OAuth_OIDC_Misconfiguration.skill.md`
- For credentialed browser reads and origin trust bugs: `skills/auth-sec/CORS_Cross_Origin_Misconfiguration.skill.md`