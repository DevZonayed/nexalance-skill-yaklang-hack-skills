# SKILL: File Upload Payload Selection — Extension Tricks, Polyglots, and Processing Targets

> **AI LOAD INSTRUCTION**: Use this skill when a target accepts file uploads and you need compact payload families for extension bypass, stored XSS, parser abuse, and post-upload execution paths.

## 1. WHEN TO LOAD THIS SKILL

Load when:

- The target accepts avatars, documents, media, imports, or admin uploads
- You need to choose between extension bypass, content spoofing, SVG/XML abuse, or server-side processing attacks

For the full upload workflow after first signal, also load:

- `../file-access-vuln/Upload_Insecure_Files.skill.md`

## 2. PAYLOAD FAMILY MAP

| Situation | Start With | Why |
|---|---|---|
| extension filtering only | double extension, case change, trailing dot | cheap validation bypass checks |
| image upload with rendering | SVG XSS or metadata injection | strong signal with small payloads |
| office or XML import | XML or OOXML payload family | parser and XXE exposure |
| image processing backend | polyglot image, ImageMagick/FFmpeg target | server-side processor abuse |
| upload path exposure | predictable filename and content-type mismatch | post-upload retrieval and execution checks |

## 3. SMALL, STABLE PAYLOAD SET

```text
shell.php.jpg
shell.php%00.jpg
file.svg
avatar.jpg.php
report.html
```

Representative content families:

- SVG with onload handler
- EXIF metadata injection
- document imports with active formulas or embedded XML
- benign marker file for content-type and retrieval checks

## 4. SOURCE POOLS TO CONSULT

- Web-Fuzzing-Box: `Vuln/File_Upload/`
- PayloadsAllTheThings: `Upload Insecure Files/`

## 5. QUICK CHECKLIST

1. Separate validation at upload time from behavior at retrieval or processing time.
2. Test one extension bypass and one content-based payload first.
3. Identify whether files are transformed, scanned, or re-served from a different host.
4. If processing exists, pivot to XSS, XXE, CMDi, or file execution routes.
5. Once the likely family is known, switch to the deep upload workflow skill.