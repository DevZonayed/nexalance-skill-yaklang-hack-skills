# SKILL: Brute Wordlist Selection — Scope, Size, and Sequence

> **AI LOAD INSTRUCTION**: Use this skill to choose the right credential wordlist size and shape before brute forcing. Prefer service-aware and scope-aware selection over giant default dictionaries.

## 1. SELECTION ORDER

1. Try service-specific defaults first.
2. Use tiny high-probability sets next.
3. Use medium lists only if the target allows enough attempts.
4. Reserve giant lists for offline cracking or long-running, explicitly approved testing.

## 2. SIZE GUIDANCE

| Scenario | Preferred Size | Why |
|---|---|---|
| Default admin panel | 5 to 50 passwords | Defaults beat giant lists here |
| Internal service with known product | vendor-specific small set | Better signal than generic lists |
| Consumer login with weak controls | Top 20 or Top 100 | Fast verification |
| Rate-limited login | tiny list + header/rotation strategy | Preserve attempts |
| Offline hash cracking | large dictionaries | Online brute rules do not apply |

## 3. SOURCE GROUPS

- Web-Fuzzing-Box: `Brute/Application/`, `Brute/Top_Password/`, `Brute/Password/`
- Small sets to prioritize: top passwords, vendor defaults, environment-specific words
- Sets to keep out of default skill content: million-scale subdomains and huge password corpora

## 4. QUICK CHECKLIST

1. Identify product or framework first.
2. Pick the smallest plausible dictionary.
3. Combine with username variants only after defaults fail.
4. Escalate dictionary size gradually, not immediately.