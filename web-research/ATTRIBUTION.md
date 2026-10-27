# ATTRIBUTION（web-research）

`web-research` 是 nWave（MIT）相关技能的改写衍生版本，并包含本仓库作者的适配修改。本目录整体按 MIT 分发，但 nWave 部分的版权仍归其原作者。

## 1. nWave（MIT）

- 仓库：https://github.com/nWave-ai/nWave
- commit：`da401a8384dc867314ba2f4a5fd802fafa593e4f`
- 许可：MIT，Copyright (c) 2026 Alessandro Digioia & Michele Brissoni
- 许可全文：本目录 `LICENSE-nWave-MIT.md`
- 使用的文件：
  - `nWave/skills/nw-source-verification/SKILL.md`（来源 Tier 表、交叉验证/循环引用、偏见清单、引用格式）
  - `nWave/skills/nw-authoritative-sources/SKILL.md`（权威域数据库、主题检索策略、时效规则）
  - `nWave/skills/nw-research-methodology/SKILL.md`（报告模板、置信度、每 claim 来源要求、质量门）
  - `nWave/skills/nw-research/SKILL.md`（仅摘取 “Default Trusted Sources” 默认可信域清单）
- 去向：`SKILL.md` 与 `references/source-rules.md`、`references/report-template.md`。
- 修改：已翻译、合并、删减并适配 DeepSeek Harness，删除 nWave 专属流程与路径；原规则内容保留。
- 版权与许可范围：nWave 部分版权归原作者，按 MIT 使用；本仓库的适配修改 © 2026 sjx，同样按 MIT 分发。再分发时必须保留本文件、`LICENSE-nWave-MIT.md` 与 MIT 版权声明。

## 2. odysseus（AGPL-3.0）— 仅设计参考

- 仓库：https://github.com/odysseus-dev/odysseus
- commit：`9d0d3720f4ca181d87bef94da826d730acc6d483`
- 许可：AGPL-3.0
- 使用的文件：无。仅参考 `resources/skills/research/web-research-fallback/SKILL.md` 的一般流程概念（一手源优先、打开原文取证、失败先换一手源、记录每页所得、事实与推断分离）。
- 公开版核验（2026-10-27）：**本仓库不包含 odysseus 的任何文件或逐字文本**。以其上游 `SKILL.md`（881 bytes）与本仓库文本做 8-gram 比对，重合为 0。AGPL-3.0 仅约束其上游项目，不构成本仓库的许可来源，也不产生再分发义务。

## 3. xixu-me/skills（MIT）

- 仓库：https://github.com/xixu-me/skills
- commit：`c54367d693e7700bed0e3ebf55c9ac4c61db3b54`
- 许可：MIT
- 使用的文件：`skills/use-my-browser/`
- 去向：作为独立技能 `use-my-browser/` **原样再分发**（未修改规则）；其版权与许可见该目录的 `ATTRIBUTION.md` 与 `LICENSE`。

## 4. 获取时间

2026-10-27（Asia/Shanghai），通过 GitHub 官方仓库 raw 文件获取。

## 5. 公开版本核验

- `LICENSE-nWave-MIT.md` 与上游 nWave MIT 文本 SHA-256 一致。
- `use-my-browser/` 的 13 个文件与 `LICENSE` 与上游 commit 逐字节一致（SHA-256）。
- odysseus 8-gram 重合为 0。
- 本仓库不含密钥、凭据、本机绝对路径或会话数据。

## 6. 再分发

再分发本目录时，请保留：本 `ATTRIBUTION.md`、`LICENSE-nWave-MIT.md`、上游版权声明与 MIT 许可文本，以及仓库根目录的 `THIRD-PARTY-NOTICES.md`。
