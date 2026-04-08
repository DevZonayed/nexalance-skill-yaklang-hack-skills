# HACKING SKILLS / HackSkills

这是一个面向漏洞赏金、Web 安全、API 安全和授权测试的 Agent Skills 知识库。

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

- skill id: `hack`
- raw URL: `https://raw.githubusercontent.com/yaklang/hack-skills/main/skills/hack/SKILL.md`

装完以后，建议先从总入口开始，再按现象进入具体专题。

## 怎么使用

推荐顺序：

1. 先加载 `hack`，让 Agent 判断当前更像是 recon、API、认证授权、注入检查、文件访问还是业务逻辑问题。
2. 再进入对应目录，加载更细的专题技能。
3. 最后回到总索引补链路，避免只盯住单点。

比较适合这些场景：

- 刚接一个新目标，需要先定测试路线。
- Web/API 安全测试里，想把专题方法补全。
- 需要系统化过一遍认证、授权、输入边界和业务边界。
- 手上只有零散现象，想快速路由到正确漏洞类别。

## 仓库结构

```text
hack-skills/
├── README.md
└── skills/
    ├── BUGBOUNTY_SKILLS.md
    ├── hack/
    │   └── SKILL.md
    ├── recon-for-sec/
    ├── injection-checking/
    ├── auth-sec/
    ├── api-sec/
    ├── payloads-for-sec/
    ├── payloads-for-brute/
    ├── file-access-vuln/
    └── business-logic-vuln/
```

目录说明：

- `hack/`: 总入口，适合先装先用。
- `recon-for-sec/`: 信息收集、方法论、目标理解。
- `injection-checking/`: XSS、SQLi、SSRF、XXE、SSTI、CMDi、NoSQL 这一类输入到危险解释器的问题。
- `auth-sec/`: 登录、会话、JWT、OAuth、CSRF，也包括 IDOR、BOLA、BFLA 这类权限边界问题。
- `api-sec/`: API 安全专项。
- `payloads-for-sec/`: 面向漏洞验证与利用前期的 payload 分类与选型入口。
- `payloads-for-brute/`: 面向默认凭证、用户名、端口和字典规模选择的轻量索引。
- `file-access-vuln/`: 路径穿越、LFI、下载接口、文件访问控制，也覆盖 upload workflow、存储路径、预览处理和文件分享边界。
- `business-logic-vuln/`: 竞态、价格篡改、流程绕过、优惠券和库存类问题。

完整索引见 `skills/BUGBOUNTY_SKILLS.md`。

## 技能选择建议

如果你看到这些现象，优先从这些目录入手：

- HTML/JS 反射、模板表达式、危险解析链路：`injection-checking`
- 登录、重置密码、2FA、JWT、OAuth、CSRF、对象权限边界：`auth-sec`
- REST API、GraphQL、移动端后端：`api-sec`
- 文件路径、下载接口、上传链路：`file-access-vuln`
- 优惠券、库存、支付、状态机与多步骤流程：`business-logic-vuln`
- 新目标、未知攻击面：先从 `recon-for-sec` 开始

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

- `skills/hack/SKILL.md`
- `skills/BUGBOUNTY_SKILLS.md`
- `skills/recon-for-sec/Recon_and_Methodology.skill.md`

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
