# SKILL: Port Targeting for Brute — Service Narrowing Before Credential Spray

> **AI LOAD INSTRUCTION**: Use this skill to focus brute-force effort on the right services and ports before selecting credentials. Service narrowing reduces noise and preserves rate limits.

## 1. SERVICE PRIORITY

| Category | Ports / Examples | Why |
|---|---|---|
| Web admin surfaces | 80, 443, 8080, 8443 | Highest chance of admin portals and API auth |
| SSH / remote admin | 22 | High-value but often tightly rate-limited |
| FTP / file services | 21 | Common weak defaults in internal targets |
| Databases | 3306, 5432, 6379, 27017 | Useful when externally exposed or SSRF-reachable |
| Mail / legacy auth | 110, 143, 993, 995 | Often paired with weak shared credentials |

## 2. HOW TO USE

- Determine whether the target is web-first, infra-first, or product-specific.
- Use banner clues and product strings to choose service-specific credentials.
- If multiple login surfaces exist, start with the one that gives the clearest product identity.

## 3. SOURCE GROUPS

- Web-Fuzzing-Box: `Brute/Ports/`

## 4. QUICK CHECKLIST

1. Narrow to the smallest port set that matches the target type.
2. Map each port to a service credential strategy.
3. Only after service identification should dictionary size expand.