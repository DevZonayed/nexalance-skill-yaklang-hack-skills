---
name: payloads-for-brute
description: >-
  Brute-force payload routing for default credentials, username variants,
  wordlist selection, and service-specific targeting. Use this as a compact
  index instead of embedding giant dictionaries into the installer entrypoint.
metadata:
  author: yaklang
  version: "1.0.0"
  category: security
  tags:
    - brute-force
    - wordlists
    - credentials
    - fuzzing
---

# payloads-for-brute

这是爆破场景的轻量索引入口。

核心目标：

1. 指导 Agent 选择对的字典规模和服务类型
2. 提供默认凭证、用户名变体和端口聚焦策略
3. 避免把超大字典直接塞进 skill

## Skill Map

- `Brute_Wordlist_Selection.skill.md`: 按场景选字典规模和组合方式
- `Default_Credentials_By_Service.skill.md`: 按服务列出默认凭证测试顺序
- `Username_Generation_and_Variants.skill.md`: 用户名变体构造规则
- `Port_Targeting_for_Brute.skill.md`: 面向爆破的端口聚焦和协议优先级

## Operating Rules

- 先缩小服务面和账号模型，再决定字典大小。
- 优先用 Top 20、Top 100、服务专用小字典做验证。
- 巨型字典只作为后续参考，不进入默认加载路径。