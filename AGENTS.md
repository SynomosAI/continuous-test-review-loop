# AGENTS.md — 给 AI Agent 的工作指引

本文件面向自动化 AI Agent。人类读者请看 [README.md](README.md)。

## 这个仓库是什么

`continuous-test-review-loop` 是一个 **Agent Skill 发布包**，核心资产是 `SKILL.md`（循环四步 + 固定 5+1 测试清单 + 复盘模板 + 处置规则）。把本目录放入 Agent 技能目录，即可在每次重大变更后跑一轮实测-复盘-改进闭环。

## 可用的工作命令

```bash
cat SKILL.md    # 循环四步 / 清单 / 模板 / 处置规则
```

前置依赖：清单中的 `ai_gateway.py doctor`、`pre_publish_scan.py` 为外部项目脚本（已标依赖）；本地测试需 Ollama 与 DSH 服务在运行。

## 约定（Do）

- 修改 `SKILL.md` 时保持 YAML frontmatter 字段兼容（`name` / `version` / `license` / `author` 等）。
- 每轮实测必须记录**原始证据**（命令输出 / 返回值 / 耗时），不只写结论。
- 改进后必须**复测**对应测试项，确认修复且无回归。
- 测试残留产物必须清理，cwd 隔离，目录恢复原状。

## 禁止（Don't）

- 不要改动 `LICENSE.md` 的版权主体（© 2026 注册老炮@MedXpert），也不要改 `SKILL.md` 的 `author` 字段。
- 不要擅自动涉外部 / 安全 / 凭据的项——报告标注「待主理人」。
- 不要未经评估对外影响就改技能 / 发布包代码。
- 不要在仓库内提交任何密钥、令牌或测试产生的敏感输出。

## 边界

本技能专注**测试-复盘-改进闭环机制**；不实现被测试的外部脚本本身（网关 / 发布扫描等为外部依赖）。
