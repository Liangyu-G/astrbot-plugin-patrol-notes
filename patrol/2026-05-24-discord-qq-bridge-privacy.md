# AstrBot 插件自主开发巡逻记录 - 2026-05-24

## GitHub 可用性

- 已通过 GitHub API 完成仓库搜索、文件读取、新建仓库与提交文档操作。
- 未输出、记录或请求任何 token/密钥。

## 仓库盘点

账号 `SXP-Simon` 下检索到的 AstrBot 插件相关仓库：

1. `SXP-Simon/astrbot_plugin_qq_group_daily_analysis`：按本轮要求排除，未巡逻、未操作。
2. `SXP-Simon/astrbot_plugin_love_formula`
3. `SXP-Simon/astrbot_plugin_yandere_github_stalker`
4. `SXP-Simon/astrbot_plugin_discord_qq_bridge`
5. `SXP-Simon/astrbot_plugin_discord_self_embeded`

## 本轮选择

选择方向：`SXP-Simon/astrbot_plugin_discord_qq_bridge` 的隐私优先文档与仓库卫生改进。

选择原因：该插件负责 Discord → QQ 跨平台消息桥接，存在天然的聊天内容、群号/频道 ID、token 与日志泄露风险；小型文档与忽略规则改进最符合本轮“小而完整、可审计”的维护目标。

## 已审阅现状

- README 已包含安装、命令、配置、故障排除等基础说明。
- 仓库存在 `_conf_schema.json` 和 `bridge_config.example.json`。
- 仓库根目录当前未发现 `.gitignore`。
- 运行配置文件 `bridge_config.json` 存在于仓库中，当前仅包含空 `enabled_groups` 与模板；后续应避免写入真实生产映射。

## 建议改动设计

### 1. 新增 `.gitignore`

建议内容覆盖：

```gitignore
# Runtime and local configuration
bridge_config.local.json
*.local.json
.env
.env.*

# AstrBot runtime data
data/
logs/
*.log

# Python cache / tooling
__pycache__/
*.py[cod]
.pytest_cache/
.mypy_cache/
.ruff_cache/
.venv/
venv/

# OS / editor files
.DS_Store
.idea/
.vscode/
```

### 2. 新增 `docs/PRIVACY.md`

应说明：

- 不提交真实 QQ 群号、QQ 账号、Discord 服务器/频道 ID、token、Webhook、Cookie、原始聊天记录。
- 生产配置应保存在 AstrBot 数据目录或本地未跟踪文件。
- Issue/PR 日志需脱敏，移除用户 ID、群号、消息正文和凭据。
- 误转发时可在对应 QQ 群执行 `/bridge disable`，并轮换可能泄露的凭据。

### 3. README 增补“隐私与安全”章节

建议放在“配置说明”之后，链接 `docs/PRIVACY.md`。

## 本轮可审计产出

- 新建巡逻记录仓库：`Liangyu-G/astrbot-plugin-patrol-notes`
- 本文档：`patrol/2026-05-24-discord-qq-bridge-privacy.md`

## 写入目标插件仓库结果

尝试对 `SXP-Simon/astrbot_plugin_discord_qq_bridge` 执行以下写入操作：

- `push_files` 到 `main`：返回 `Not Found`。
- `create_branch`：返回 `Not Found`。
- `create_or_update_file`：返回 `Not Found`。
- `create_issue`：返回 `Validation Failed`。

因此本轮未能在目标插件仓库直接落地 commit/PR/issue，改为在当前可写账号下建立独立巡逻记录仓库，保留完整设计与审计链路。

## 测试/校验

- GitHub 读取能力正常：已读取目标仓库根目录、README、配置 schema、主代码文件。
- GitHub 写入能力部分可用：可新建当前账号仓库并写入巡逻记录。
- 本轮未修改插件运行时代码，无需运行单元测试。
- 文档内容未包含真实 QQ 号、Discord ID、聊天记录、token 或服务器敏感信息。

## 风险与回滚建议

- 当前产出为独立记录仓库文档，不影响任何 AstrBot 插件运行。
- 如需回滚，可删除本记录文件或归档该记录仓库；不涉及强推或 release。
- 后续若将建议同步到插件仓库，应避免提交真实 `bridge_config.json` 生产内容。

## 下一轮计划

1. 若获得 `SXP-Simon/astrbot_plugin_discord_qq_bridge` 写权限：提交 `.gitignore`、`docs/PRIVACY.md` 与 README 隐私章节。
2. 检查 `bridge_config.json` 是否应替换为 example 或移入忽略范围，避免未来写入真实群映射。
3. 为消息格式化逻辑补一个纯函数级测试，覆盖 Discord markdown/mention 脱敏转换。
4. 继续巡逻其他 `astrbot_plugin_*` 仓库，优先选择 README/schema/test 缺口明显的插件。
