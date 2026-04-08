# SKILL: Default Credentials by Service — Small, High-Probability Sets

> **AI LOAD INSTRUCTION**: Use this skill for common services where default or weak credential pairs outperform generic brute-force dictionaries.

## 1. SERVICE-FIRST PRIORITY

| Service Type | First Usernames | First Passwords |
|---|---|---|
| phpMyAdmin | `root`, `admin` | empty, `root`, `phpmyadmin`, `admin` |
| FTP | `ftp`, `admin`, `test` | empty, `ftp`, `admin`, `123456` |
| SSH | `root`, `admin`, service account names | `root`, `admin`, seasonal variants |
| MySQL | `root`, `mysql` | empty, `root`, `mysql` |
| Tomcat / Java admin | `tomcat`, `admin`, `manager` | `tomcat`, `admin`, `s3cret` |
| WebLogic | `weblogic`, `admin` | `weblogic`, `welcome1`, `admin` |

## 2. HOW TO USE THIS SKILL

- Start with 3 to 10 high-probability pairs.
- If the panel or banner reveals the product, switch to product-specific pairs immediately.
- If there is no product clue, prefer admin-centric defaults before generic top lists.

## 3. SOURCE GROUPS

- Web-Fuzzing-Box: `Brute/Application/`

Do not inline every file. Reuse the service grouping as the routing structure.

## 4. QUICK CHECKLIST

1. Identify product, port, and login realm.
2. Test tiny default pairs.
3. If one credential field is fixed, shift effort to the other field only.
4. If defaults fail, move to the wordlist selection skill.