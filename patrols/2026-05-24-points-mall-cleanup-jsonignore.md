# 2026-05-24 14:02 UTC 巡逻记录：astrbot_plugin_points_mall

## 范围

- 已按要求跳过 `SXP-Simon/astrbot_plugin_qq_group_daily_analysis`，未巡逻、未读取、未修改。
- 盘点 `Liangyu-G` 下 AstrBot 相关仓库：
  - `Liangyu-G/astrbot_plugin_points_mall`
  - `Liangyu-G/astrbot_plugin_ops_health`
  - `Liangyu-G/astrbot-plugin-patrol-notes`

## 本轮处理

优先处理 `Liangyu-G/astrbot_plugin_points_mall`：

- 已创建分支 `patrol/cleanup-points-mall-cache-jsonignore`。
- 已提交 `.gitignore` 修正：移除过宽的根级 `*.json`，改为 `data/**/*.json`，避免误忽略 `_conf_schema.json`。
- 已创建 PR：https://github.com/Liangyu-G/astrbot_plugin_points_mall/pull/2
- 已确认 `_conf_schema.json` 在分支中仍可见。
- 已确认主分支存在已跟踪字节码缓存：`__pycache__/main.cpython-312.pyc`。

## 未完成项

当前 GitHub MCP 文件工具支持创建/更新文件，但未提供删除已跟踪文件的接口；因此 `__pycache__/main.cpython-312.pyc` 暂未能通过本轮工具直接删除。建议在 PR 合并前或后执行：

```bash
git rm __pycache__/main.cpython-312.pyc
git commit -m "chore: remove tracked pycache"
```

## 安全约束

- 未泄露 token/密钥。
- 未删除仓库。
- 未发布 release。
- 未强推。
- 未修改源码逻辑。

## 回滚建议

如需回滚本轮 `.gitignore` 修改，可关闭 PR #2，或在分支中恢复 `.gitignore` 到提交前内容：

```gitignore
__pycache__/
*.pyc
*.json
*.json.bak
```

但不建议长期保留 `*.json`，否则会再次误忽略 `_conf_schema.json` 等仓库配置文件。
