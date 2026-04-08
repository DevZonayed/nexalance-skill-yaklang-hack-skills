# SKILL: SSTI Payload Selection — Polyglots, Engine Fingerprints, and Low-Noise Escalation

> **AI LOAD INSTRUCTION**: Use this skill when server-side template injection is plausible and you need compact probes to distinguish engines before loading the full exploitation playbook.

## 1. WHEN TO LOAD THIS SKILL

Load when reflected input appears inside templates, rendered emails, previews, exports, or server-side theming logic.

## 2. FIRST-PASS PROBE SEQUENCE

```text
{{7*7}}
${7*7}
#{7*7}
<#assign x=7*7>${x}
@{7*7}
```

## 3. FINGERPRINT HINTS

| Result | Likely Engine Family |
|---|---|
| `49` from `{{7*7}}` | Jinja2 or Twig |
| `7777777` from `{{7*'7'}}` | Jinja2 |
| `49` from `${7*7}` | Java EL / FreeMarker / Velocity |
| `class 'str'` style object output | Python templating |
| fragment or expression syntax accepted | Thymeleaf / Spring EL |

## 4. LOW-NOISE NEXT PICKS

- object introspection without code execution
- math evaluation confirmation
- engine-specific safe probes before RCE chains

## 5. SOURCE POOLS TO CONSULT

- PayloadsAllTheThings: `Server Side Template Injection/`

## 6. QUICK CHECKLIST

1. Confirm server-side evaluation, not client-side template rendering.
2. Fingerprint the engine with two or three low-noise probes.
3. Only after the engine is known should you switch to the full SSTI skill.