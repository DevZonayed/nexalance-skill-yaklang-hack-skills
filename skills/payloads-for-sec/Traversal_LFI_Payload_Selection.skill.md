# SKILL: Traversal and LFI Payload Selection — Path Mutation and File Targets

> **AI LOAD INSTRUCTION**: Use this skill when file paths, download paths, templates, or include sinks are controllable and you need a compact traversal and LFI payload map instead of a giant wordlist.

## 1. WHEN TO LOAD THIS SKILL

Load when:

- URL, JSON, or form fields influence file names or include paths
- You need to choose traversal encodings and target files quickly

For deeper exploitation, also load:

- `skills/file-access-vuln/PathTraversal_LFI.skill.md`

## 2. FIRST-PASS TRAVERSAL CHAINS

```text
../etc/passwd
../../../../etc/passwd
..%2f..%2f..%2fetc%2fpasswd
..%252f..%252f..%252fetc%252fpasswd
..\\..\\..\\windows\\win.ini
```

## 3. FILE TARGETS BY PLATFORM

| Platform | First Targets |
|---|---|
| Linux | `/etc/passwd`, `/etc/hosts`, app config, logs |
| PHP app | config files, session files, access logs, wrapper targets |
| Windows | `C:\\Windows\\win.ini`, `C:\\inetpub\\wwwroot`, IIS logs |
| Containers | `/proc/self/environ`, mounted secrets, app env files |

## 4. BYPASS FAMILIES

| Filter Behavior | Try |
|---|---|
| strips `../` | double URL encoding, nested traversal, mixed slash |
| normalizes once | double-decoded variants |
| suffix appended | null-byte style legacy tests, wrapper abuse, valid extension chaining |
| PHP include sink | `php://filter`, `php://input`, `data://` |

## 5. SOURCE POOLS TO CONSULT

- Web-Fuzzing-Box: `Vuln/Traversal_Directory/`, `Vuln/File_Include/`, `Web/File_Path/`
- PayloadsAllTheThings: `Directory Traversal/`, `File Inclusion/`

## 6. QUICK CHECKLIST

1. Confirm read, include, or download behavior.
2. Test a clean traversal chain on Linux and Windows targets.
3. Observe normalization and encoding behavior.
4. If PHP is involved, move quickly to wrapper testing in the full LFI skill.