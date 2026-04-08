# SKILL: API Security Testing — Router for Recon, Authorization, Token Abuse, and GraphQL

> **AI LOAD INSTRUCTION**: This file is the API security router. Load it first to decide which specialized API skill to use next. Keep this file lightweight; do not treat it as the full attack reference.

## 1. WHEN TO LOAD THIS FILE

Load this file when the target exposes REST, mobile, or GraphQL APIs and you need to choose the correct deeper skill quickly.

## 2. API SKILL MAP

| Situation | Load Next |
|---|---|
| Need endpoint discovery, docs, versions, schemas | `API_Recon_and_Docs.skill.md` |
| Object IDs, nested resources, admin functions, hidden writable fields | `API_Authorization_and_BOLA.skill.md` |
| JWT, bearer tokens, API keys, header spoofing, rate-limit issues | `API_Auth_and_JWT_Abuse.skill.md` |
| GraphQL, batching, introspection, undocumented or optional parameters | `GraphQL_and_Hidden_Parameters.skill.md` |

## 3. DEFAULT API TEST ORDER

1. Recon and docs
2. Authorization: BOLA, BFLA, method abuse, mass assignment
3. Token trust and rate limiting
4. GraphQL and hidden parameter discovery
5. Business logic and chained exploitation if the authz boundary is sound

## 4. QUICK TRIAGE

| Observation | Route |
|---|---|
| Swagger or OpenAPI exists | `API_Recon_and_Docs.skill.md` |
| IDs appear in URL, JSON, headers, or GraphQL args | `API_Authorization_and_BOLA.skill.md` |
| JWT token visible in traffic | `API_Auth_and_JWT_Abuse.skill.md` |
| `/graphql` or batched JSON arrays exist | `GraphQL_and_Hidden_Parameters.skill.md` |
| Login, registration, or profile update accepts extra fields | `API_Authorization_and_BOLA.skill.md` plus `API_Auth_and_JWT_Abuse.skill.md` |

## 5. RELATED NON-API SKILLS

- `skills/auth-sec/IDOR_Broken_Object_Authorization.skill.md`
- `skills/auth-sec/JWT_OAuth_Token_Attacks.skill.md`
- `skills/business-logic-vuln/BusinessLogic_Vulnerabilities.skill.md`
- `skills/recon-for-sec/Recon_and_Methodology.skill.md`

## 6. RULES

- Do not start with giant endpoint or payload lists.
- Confirm target type and trust boundary first.
- Route into the smallest specialized skill that matches the current evidence.