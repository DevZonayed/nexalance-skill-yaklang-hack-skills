# SKILL: Username Generation and Variants — Admin Patterns and Identity Guesses

> **AI LOAD INSTRUCTION**: Use this skill when a login surface exists but no username list is available. Build small, defensible username sets from role, naming convention, and organization context.

## 1. FIRST-PASS USERNAME CLASSES

| Class | Examples |
|---|---|
| Generic admins | `admin`, `administrator`, `root`, `test`, `guest` |
| Support / ops | `dev`, `ops`, `sysadmin`, `service`, `backup` |
| Name-based | `firstname`, `lastname`, `f.lastname`, `first.last` |
| Mail-derived | left side of corporate email formats |
| Product-based | `tomcat`, `weblogic`, `jenkins`, `gitlab` |

## 2. VARIANT RULES

- lowercase and original casing
- numeric suffixes like `admin1`, `test01`
- year or season suffixes only if the target pattern suggests it
- tenant or organization prefix when multi-tenant naming is visible

## 3. SOURCE GROUPS

- Web-Fuzzing-Box: `Brute/Username/`, `Brute/Full_Name/`, `Brute/Test_Chinese_Mobilephonenumber.txt`

Use locale-aware sources only when the target context justifies them.

## 4. QUICK CHECKLIST

1. Infer whether the system uses email, short usernames, or employee IDs.
2. Start with 5 to 20 usernames.
3. Add organization-specific variants only after format evidence appears.
4. Avoid giant name corpora unless the target scope explicitly warrants it.