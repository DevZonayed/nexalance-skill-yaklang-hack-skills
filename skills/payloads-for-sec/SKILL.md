---
name: payloads-for-sec
description: >-
  Security payload routing for web and API testing. Use when the agent needs a
  compact index of payload families, bypass patterns, and scenario-based quick
  picks instead of raw giant wordlists.
metadata:
  author: yaklang
  version: "1.0.0"
  category: security
  tags:
    - payloads
    - web-security
    - api-security
    - fuzzing
---

# payloads-for-sec

这是面向安全测试场景的 payload 索引入口。

它不负责承载超大字典，也不复制外部仓库全文。它只做三件事：

1. 按漏洞类型路由到更合适的 payload skill
2. 提供小而稳定的样本、分类法和使用边界
3. 把 payload 选择和现有专题技能串起来

## When to Use

优先在这些场景使用：

- 你已经确认目标漏洞方向，但需要快速选 payload 家族
- 你不想把大字典直接塞给 Agent，只想让它先选测试路径
- 你需要把 payload 和专题 skill 连接起来，而不是孤立地枚举字符串

## Skill Map

- `SQLi_Payload_Selection.skill.md`: SQL 注入 payload 家族、按 DBMS/技术分类
- `XSS_Payload_Selection.skill.md`: XSS 上下文矩阵和小样本 payload 选型
- `SSRF_and_URL_Scheme_Payloads.skill.md`: SSRF 协议链、编码绕过和命中顺序
- `Traversal_LFI_Payload_Selection.skill.md`: 路径穿越、LFI、常见文件目标和变形链
- `JWT_and_API_Abuse_Payloads.skill.md`: JWT、Header 绕过、API 参数/批处理滥用
- `File_Upload_Payload_Selection.skill.md`: 上传扩展绕过、SVG/XML、处理链与回显路径
- `SSTI_Payload_Selection.skill.md`: SSTI 指纹探针、低噪声探测和引擎分流
- `CMDi_Payload_Selection.skill.md`: 命令注入分隔符、盲测和过滤绕过家族

## Operating Rules

- 先识别上下文，再选 payload，不要先堆大字典。
- 优先使用小样本确认漏洞类型，再扩大 payload 族。
- 命中后回到对应专题 skill 做深挖，而不是继续盲打。
- 对大规模字典，只记录适用场景和选择策略，不内嵌全集。