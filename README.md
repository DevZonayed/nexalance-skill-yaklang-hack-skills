# HACKING SKILLS / HackSkills

这是一个面向漏洞赏金、Web 安全、API 安全和授权测试的 Agent Skills 知识库。

仓库现在采用标准的目录式 skill 结构：每一个可复用 skill 都是一个独立文件夹，文件夹内包含一个标准入口 [SKILL.md](./skills/hack/SKILL.md)。设计目标不是把所有零碎技巧都暴露成入口，而是让 loader 优先发现高价值入口，再按分类和现象逐层进入更深的专题技能。

目标很直接：把真正能在实战里派上用场、又方便审查和持续维护的安全知识，整理成一套可安装、可检索、可组合的 HackSkills。

## 知识来源与蒸馏边界

这个仓库不是外部资料的镜像仓库，而是一个面向 Agent 的蒸馏层。

目前主要参考这些公开知识来源：

- `gh0stkey/Web-Fuzzing-Box`: 提供按场景组织的字典、payload 和 fuzzing 组件，适合蒸馏为分类法和小样本选择策略。
- `BugBountyBooks`: 提供适合技能化整理的漏洞赏金方法论、测试套路与专题草稿。
- `swisskyrepo/PayloadsAllTheThings`: 提供高价值 payload 家族、绕过方式和利用链方向，适合蒸馏为场景化索引与方法矩阵。

本仓库对这些内容的处理原则是：

- 不直接搬运超大字典和长 payload 全集。
- 优先提炼为可路由、可组合、可审查的安全 skill。
- 用小而稳定的样本、分类法和交叉引用来提升 Agent 在真实安全场景中的稳定性。

## 快速开始

首选入口是 `hack`：

```bash
npx skills add yaklang/hack-skills
```

如果你的工具支持直接拉单个 SKILL.md，也可以使用：

- frontmatter name: `entry-00-hack`
- raw URL: `https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md`

装完以后，建议先从总入口开始，再按现象进入分类入口和深度专题 skill。

## Loader 优先级

为了更符合实际 loader 的使用方式，这个仓库把 skill 分成三层：

另外，入口层 frontmatter name 现在使用稳定前缀：`entry-00-*` 表示总入口，`entry-10-*` 到 `entry-60-*` 表示分类入口。这样做不改变文件路径，只是让 loader 在按名称展示时更稳定地把入口层排在一起。

| 层级 | 作用 | 推荐暴露方式 | 代表 skill |
|---|---|---|---|
| 总入口 | 负责全局路由、测试顺序和跨类别切换 | 优先暴露 | [hack](./skills/hack/SKILL.md) |
| 分类入口 | 负责按攻击面分流到稳定的专题族 | 优先暴露 | [api-sec](./skills/api-sec/SKILL.md), [auth-sec](./skills/auth-sec/SKILL.md), [injection-checking](./skills/injection-checking/SKILL.md) |
| 深度专题 | 提供完整攻击手册和执行细节 | 按需加载 | [xss-cross-site-scripting](./skills/xss-cross-site-scripting/SKILL.md), [jwt-oauth-token-attacks](./skills/jwt-oauth-token-attacks/SKILL.md) |

像 payload-selection、默认凭证、用户名生成、端口聚焦这类短 skill 现在进一步并回了主专题 skill，不再保留为独立入口。loader 优先面对总入口、分类入口和深度专题，不再需要处理中间层碎片 skill。

## 怎么使用

推荐顺序：

1. 先加载 `hack`，让 Agent 判断当前更像是 recon、API、认证授权、注入检查、文件访问还是业务逻辑问题。
2. 再进入对应分类 skill，而不是一开始就直接挑一个很细的专题。
3. 只有在现象已经明确时，再进入深度专题 skill。
4. payload 选型、小字典和快速样本选择，直接在对应主专题里处理，不再单独跳辅助入口。

比较适合这些场景：

- 刚接一个新目标，需要先定测试路线。
- Web/API 安全测试里，想把专题方法补全。
- 需要系统化过一遍认证、授权、输入边界和业务边界。
- 手上只有零散现象，想快速路由到正确漏洞类别。

## 主要入口

| 类型 | Skill | 用途 | 何时优先使用 |
|---|---|---|---|
| 总入口 | [hack](./skills/hack/SKILL.md) | 全局路由、阶段判断、跨类别切换 | 新目标、未知攻击面、想先定方法论 |
| 分类入口 | [recon-for-sec](./skills/recon-for-sec/SKILL.md) | 资产发现、技术识别、测试起点 | 刚接目标、信息不足 |
| 分类入口 | [api-sec](./skills/api-sec/SKILL.md) | REST、GraphQL、移动端后端路由 | 看到 API 接口或 OpenAPI |
| 分类入口 | [auth-sec](./skills/auth-sec/SKILL.md) | 认证、会话、OAuth、JWT、对象授权 | 看到登录、令牌、对象 ID、跨租户 |
| 分类入口 | [injection-checking](./skills/injection-checking/SKILL.md) | XSS、SQLi、SSRF、XXE、SSTI、CMDi、NoSQL 路由 | 输入进入解释器或执行环境 |
| 分类入口 | [file-access-vuln](./skills/file-access-vuln/SKILL.md) | 上传、下载、LFI、路径控制、处理链 | 文件名、路径、下载、预览、上传 |
| 分类入口 | [business-logic-vuln](./skills/business-logic-vuln/SKILL.md) | 竞态、价格、流程、状态机问题 | 优惠券、库存、支付、审批、配额 |

## 分类到专题映射

| 分类 | 推荐先读 | 常见下钻专题 |
|---|---|---|
| Recon | [recon-for-sec](./skills/recon-for-sec/SKILL.md) | [recon-and-methodology](./skills/recon-and-methodology/SKILL.md) |
| API | [api-sec](./skills/api-sec/SKILL.md) | [api-recon-and-docs](./skills/api-recon-and-docs/SKILL.md), [api-authorization-and-bola](./skills/api-authorization-and-bola/SKILL.md), [api-auth-and-jwt-abuse](./skills/api-auth-and-jwt-abuse/SKILL.md) |
| Auth | [auth-sec](./skills/auth-sec/SKILL.md) | [authbypass-authentication-flaws](./skills/authbypass-authentication-flaws/SKILL.md), [jwt-oauth-token-attacks](./skills/jwt-oauth-token-attacks/SKILL.md), [idor-broken-object-authorization](./skills/idor-broken-object-authorization/SKILL.md) |
| Injection | [injection-checking](./skills/injection-checking/SKILL.md) | [xss-cross-site-scripting](./skills/xss-cross-site-scripting/SKILL.md), [sqli-sql-injection](./skills/sqli-sql-injection/SKILL.md), [ssrf-server-side-request-forgery](./skills/ssrf-server-side-request-forgery/SKILL.md) |
| File Access | [file-access-vuln](./skills/file-access-vuln/SKILL.md) | [upload-insecure-files](./skills/upload-insecure-files/SKILL.md), [path-traversal-lfi](./skills/path-traversal-lfi/SKILL.md) |
| Business Logic | [business-logic-vuln](./skills/business-logic-vuln/SKILL.md) | [business-logic-vulnerabilities](./skills/business-logic-vulnerabilities/SKILL.md) |

## 仓库结构

```text
hack-skills/
├── README.md
└── skills/
    ├── BUGBOUNTY_SKILLS.md
    ├── hack/
    │   └── SKILL.md
    ├── api-sec/
    │   └── SKILL.md
    ├── auth-sec/
    │   └── SKILL.md
    ├── injection-checking/
    │   └── SKILL.md
    ├── file-access-vuln/
    │   └── SKILL.md
    ├── business-logic-vuln/
    │   └── SKILL.md
    ├── recon-for-sec/
    │   └── SKILL.md
    ├── jwt-oauth-token-attacks/
    │   └── SKILL.md
    ├── xss-cross-site-scripting/
    │   └── SKILL.md
    └── recon-and-methodology/
        └── SKILL.md
```

目录说明：

- `hack/`: 总入口，适合先装先用。
- `recon-for-sec/`: 分类入口 skill，负责信息收集和方法论路由。
- `injection-checking/`: 分类入口 skill，负责 XSS、SQLi、SSRF、XXE、SSTI、CMDi、NoSQL 的路由。
- `auth-sec/`: 分类入口 skill，负责登录、会话、JWT、OAuth、CSRF、IDOR、BOLA、BFLA 的路由。
- `api-sec/`: 分类入口 skill，负责 API recon、授权、认证和 GraphQL 的路由。
- `file-access-vuln/`: 分类入口 skill，负责路径穿越、LFI、上传与文件处理链路由。
- `business-logic-vuln/`: 分类入口 skill，负责竞态、价格篡改和流程绕过路由。
- 其他语义化目录例如 `xss-cross-site-scripting/`、`api-auth-and-jwt-abuse/`、`recon-and-methodology/` 都是可直接被加载的深度专题 skill。
- 原先的 payload-selection / brute-selection / API 中间路由型小 skill 已并入主专题或分类入口，用来减少入口噪音。

完整索引见 `skills/BUGBOUNTY_SKILLS.md`。

## 技能选择建议

如果你看到这些现象，优先从这些入口入手：

| 现象 | 推荐入口 | 说明 |
|---|---|---|
| 新目标、信息不足 | [recon-for-sec](./skills/recon-for-sec/SKILL.md) | 先做方法论和资产理解 |
| REST API、GraphQL、移动端后端 | [api-sec](./skills/api-sec/SKILL.md) | 先分流到 recon、authz、token 或 GraphQL |
| 登录、重置密码、2FA、JWT、OAuth、对象权限边界 | [auth-sec](./skills/auth-sec/SKILL.md) | 先分认证、授权、协议配置 |
| HTML/JS 反射、模板表达式、危险解析链路 | [injection-checking](./skills/injection-checking/SKILL.md) | 先确定是 XSS、SQLi、SSRF、XXE 还是 SSTI |
| 文件路径、下载接口、上传链路 | [file-access-vuln](./skills/file-access-vuln/SKILL.md) | 先分 LFI/Traversal 与 Upload workflow |
| 优惠券、库存、支付、状态机、多步骤流程 | [business-logic-vuln](./skills/business-logic-vuln/SKILL.md) | 先按业务规则和竞态建模 |

## 安装方式

### 通用安装

```bash
npx skills add yaklang/hack-skills
```

### Raw URL 安装

适用于支持拉取单文件技能的工具：

```bash
curl -fsSL https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md
```

### 本地作为知识库使用

```bash
git clone https://github.com/yaklang/hack-skills.git
cd hack-skills
```

建议先读：

- [./skills/hack/SKILL.md](./skills/hack/SKILL.md)
- [skills/BUGBOUNTY_SKILLS.md](skills/BUGBOUNTY_SKILLS.md)
- [./skills/recon-for-sec/SKILL.md](./skills/recon-for-sec/SKILL.md)
- [./skills/recon-and-methodology/SKILL.md](./skills/recon-and-methodology/SKILL.md)

如果你只是想让 loader 更稳定，优先让 loader 命中 `entry-00-hack` 和 `entry-10-*` 到 `entry-60-*` 这一组入口。现在中间层 helper skill 已大幅收缩，默认不再需要暴露一串小 skill 给 loader 选。

## 设计原则

- 安全知识优先于花哨包装。
- 内容可审查性优先于数量扩张。
- 优先服务授权测试、合法研究与防御验证场景。
- 目录名尽量让人一眼看出安全语义，而不是做机械后缀堆叠。

## 贡献方式

欢迎提交 PR，重点方向包括：

- 新漏洞类别与高价值案例
- 更好的漏洞赏金方法论
- Agent 容易忽略的边界条件
- 风险提示、术语统一与内容去噪

贡献内容建议满足：

- 可验证
- 可审查
- 不鼓励未授权攻击
- 能帮助 Agent 在真实任务中更稳健地推理与执行
