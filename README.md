# continuous-test-review-loop · 持续测试评审闭环

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-blue.svg)](SKILL.md)
[![Test-Review-Improve Loop](https://img.shields.io/badge/loop-test%20%7C%20review%20%7C%20improve-brightgreen.svg)](SKILL.md)
[![Fixed Checklist](https://img.shields.io/badge/checklist-5%2B1%20items-2ea44f.svg)](SKILL.md)
[![Regression Aware](https://img.shields.io/badge/regression-retest-informational.svg)](SKILL.md)
[![Version](https://img.shields.io/badge/version-1.0.0-informational.svg)](SKILL.md)

SynomosAI 四支柱体系：**身份（Identity）· 溯源（Traceability）· 治理（Governance）· 共生（Symbiosis）**——当 AI 进入商业，可信是唯一的硬通货。

> 本仓库属于 [SynomosAI](https://github.com/SynomosAI) 生态技能包的一员。生态全景见 [`synomosai-skills`](https://github.com/SynomosAI/synomosai-skills)，理论站位见 [`traceability-audit`](https://github.com/SynomosAI/traceability-audit)。

**关键词 / Keywords**：持续测试 · 复盘 · 改进闭环 · 回归复测 · 固定测试清单 · 发布前扫描 · 质量门禁 · continuous testing · regression · test review loop

把「不断测试 → 复盘 → 改进 → 复测」做成**常态化机制**：固定测试清单、复盘模板、改进闭环、每轮报告入方案池。每次重大变更（新方案入库 / 技能发布 / 工具升级）后跑一轮，也可每周例行（配自动化）。未清零的问题项进入下轮清单，直至清零。

---

## ✨ 特性 / Features

- **循环四步**：① 实测（按固定清单跑，记录原始证据）→ ② 复盘（通过项 / 发现项 / 认知修正 / 处置状态）→ ③ 改进（内部可做的立即改，涉外部 / 安全先问）→ ④ 复测确认无回归。
- **固定测试清单 5+1**：统一大模型网关（doctor + 真实调用）、本地算力链（Ollama + DSH 探测）、发布扫描（0 命中）、参赛包 / 发布包端到端 run、展示页渲染 + 敏感词自查、待接入项逐轮推进。
- **复盘模板**：结果总览表 / 分项明细 / 认知修正 / 改进点处置（✅本轮 / 🔶待下轮）/ 循环状态。
- **改进处置规则**：文档过时立即修订；脚本小 bug 可修则修 + 复测；技能 / 发布包代码谨慎评估对外影响；涉外部 / 安全 / 凭据不动，标注「待主理人」。
- **工程经验沉淀**：如 qwen thinking 模式 token 消耗、冷启动预热、发布扫描豁免清单等实测踩坑。

---

## 🚀 快速开始 / Quick Start

> 前置：把本目录放入 Agent 技能目录；清单中的外部脚本（`ai_gateway.py doctor`、`pre_publish_scan.py`）已标注为外部依赖。

```bash
# 1. 克隆本仓
git clone https://github.com/SynomosAI/continuous-test-review-loop.git
cd continuous-test-review-loop

# 2. 查看技能主文件（循环四步 / 固定清单 / 复盘模板 / 处置规则）
cat SKILL.md
```

重大变更后按清单跑一轮实测，记录原始证据（命令输出 / 返回值 / 耗时），再按复盘模板成稿。

```text
触发词示例：
  测试 / 复盘 / 改进 / 打磨 / 实际运行测试 / 验证方案
```

---

## 📖 使用方式 / Usage

1. 克隆本仓库或将技能目录放入 Agent 技能目录；
2. 每次重大变更后，按固定测试清单跑「实测」并留证；
3. 按复盘模板整理本轮报告（通过项 / 发现项 / 认知修正 / 处置）；
4. 内部可做的改进立即改并复测；未清零项进下轮清单。

### 复盘报告示例（节选）

```text
# 实测报告 · 第 N 轮 · 2026-08-28
  #1 网关 doctor：✅ 全绿，真实调用有返回
  #2 本地算力链：🔶 qwen3.5:4b 默认 thinking，num_predict=40 时 content 为空
       → 处置：调用加 "think": false（本轮改进，已复测通过）
  #3 发布扫描：✅ 0 命中（豁免清单已含官方邮箱）
  循环状态：#2 已清零，无下轮遗留
```

---

## 🧩 仓库结构 / Repository layout

```text
continuous-test-review-loop/
├── README.md                # 本文件
├── README.en.md             # 英文版说明
├── SKILL.md                 # 技能主文件（循环四步 / 清单 / 模板 / 处置规则）
├── LICENSE.md               # MIT License
├── llms.txt / llms-full.txt # 给 AI 的索引与完整文本
├── AGENTS.md                # 给 AI Agent 的工作指引
├── SECURITY.md              # 安全策略
└── CODEOWNERS               # 代码所有者
```

---

## 🔎 固定测试清单 / Checklist（5+1）

| # | 测试项 | 方法 | 通过标准 |
|---|---|---|---|
| 1 | 统一大模型网关 | `ai_gateway.py doctor` + 真实 text 调用 | doctor 全绿 + 有返回 + 计费正常 |
| 2 | 本地算力链 | Ollama `/api/tags` + qwen 推理 + DSH 8081 探测 | 模型在册 + 推理返回 + 8081 有响应 |
| 3 | 发布扫描 | `pre_publish_scan.py <包/zip>` | 0 命中 |
| 4 | 参赛包 / 发布包 | 端到端 run（含 demo 输入） | 产物齐全 + 无报错 |
| 5 | 展示页 | 渲染 + 敏感词 Grep 自查 | 渲染正常 + 0 命中 |
| 6 | 待接入项 | 网关接入 / 冷启动预热 / 台账落盘 | 逐轮推进 |

---

## ❓ 常见问题 / FAQ

- **测试要跑多频繁？** 每次重大变更后一轮；也可每周例行（配自动化）。
- **发现问题立即改吗？** 内部文档 / 记忆 / 脚本小 bug 可立即改并复测；涉发布包代码谨慎评估；涉外部 / 安全 / 凭据不动，标注待主理人。
- **测试产物要清理吗？** 必须。测试残留产物清理、cwd 隔离、目录恢复原状。

---

## License / 许可

本项目以 **MIT** 许可发布，详见仓库根目录 [LICENSE.md](LICENSE.md)。版权：© 2026 注册老炮@MedXpert。

---

## 🔒 安全 / Security

如发现安全问题，请按 [`SECURITY.md`](SECURITY.md) 的方式私下报告，不要在公开 issue 中披露。

## 🤝 贡献 / Contributing

欢迎补充测试清单项、复盘模板字段与工程经验；修改 `SKILL.md` 时保持 YAML frontmatter 字段兼容。代码所有者见 [CODEOWNERS](CODEOWNERS)。

---

## 免责声明

本仓库内容为 SynomosAI 的**理论站位与工具化探索**，不代表任何已获认证、已商业化交付或已服务特定客户的声明；文中涉及的外部脚本与标准信息为公开资料转述，正式引用前请**独立核实**。API、授权码与形象大使等为路线图（roadmap）事项，尚未上线。
