# Newland Claude Code 插件市场

给 Claude Code 用的插件市场。装上之后，AI 助手就知道怎么接入 Newland 的开发者平台。

## 安装

在 Claude Code 里执行两条命令：

```
/plugin marketplace add caidc8252/claude-skills
/plugin install newland-pep@newland
```

装完重开一个会话即可生效。以后更新用 `/plugin update newland-pep@newland`。

## 现有插件

### `newland-pep`

引导 AI 助手接入 Newland PEP 平台：装好 `pep-cli` → 登录 → 同步平台下发的 skills → 读取
开发者文档。

装好之后直接跟 AI 说需求即可，例如「帮我接入 Newland 的 SDK」「帮我看 PEP 的文档」。

**它只负责引导。** 真正的接入指南由 PEP 平台通过 `pep skills sync` 下发、随时更新；本插件
刻意不复制那些内容——复制一份就会过期，而过期的接入指南比没有更糟。

需要 **Windows 或 macOS** + Node.js ≥ 24。Linux 暂不支持（令牌要存进操作系统凭据库，
Linux 那一侧还没实现）。

**登录那一步需要本人操作**：会打开浏览器让你用 PEP 账号登录并确认授权——这是 OAuth
授权码流程的要求，AI 代替不了。插件里已写明让它到这一步停下来交给你。

## 目录结构

```
.claude-plugin/marketplace.json     市场清单：本仓提供哪些插件
plugins/<插件名>/
├── .claude-plugin/plugin.json      插件清单：名称、版本、贡献哪些组件
└── SKILL.md                        技能本体
```

改动后本地先验，两条都要过：

```bash
claude plugin validate .                      # 市场清单
claude plugin validate plugins/newland-pep    # 插件清单
```

## 要注意的

**本仓必须保持 public。** `/plugin marketplace add` 走 GitHub，私有仓客户拉不下来。仓里不放
任何凭据——插件内容只是「装什么、去哪登录」，没有秘密。

**发版改 `plugin.json` 的 `version`。** 客户 `/plugin update` 靠它判断有没有新版。
