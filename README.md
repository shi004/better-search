# better-search

给 DeepSeek Harness（DSH）的**可溯源网页研究技能**：官方与一手信源优先，第三方内容只当线索，关键结论必须带 URL、日期与原文证据。

> **English** — Two DSH skills for traceable web research. `web-research` prefers official and first-party sources, treats third-party material only as leads, and requires URL/date/quote evidence for important conclusions. `use-my-browser` is a vendored MIT browser-routing skill.

本仓库提供两个技能：`web-research`（研究入口）与 `use-my-browser`（浏览器路由）。

## 这是什么

- **`web-research`**：先判任务类型，再按 L1/L2/L3 分级检索、取证和输出。适合查资料、核实信息、多源对比，以及市场、生活、设计类调研；纯本地文件、代码或数据任务不需要加载。
- **`use-my-browser`**：判断静态抓取是否足够；需要登录态、动态渲染、交互、视觉确认或真实浏览器状态时，路由到当前环境的 MCP 浏览器。来自 xixu-me/skills，MIT 原样再分发。

## 本项目的新贡献

本项目在 nWave（MIT）的信源判断、报告模板与质量门内容基础上，做了面向 DSH 的整合与增补：

- **单入口整合**：把 nWave 的多个研究/信源技能合并为 `web-research` 入口 + 两份按需读取的 references，去掉 nWave 专属流程与路径。
- **输出分级**：L1 快速查（短答 + 来源，不读模板）、L2 标准调研（结论 + 证据表 + 存疑项）、L3 深度报告（完整模板 + 质量门）。
- **事实与经验分流**：规则/事实型按官方与一手源取证；经验/操作型允许社区实践作为主要依据；混合型分开取证、分别标注。
- **新增经验证据规则**：可复现、共识度、版本/时间匹配、作者利益披露、样本范围、可验证出处；医疗、金融、法律等高风险主题不得只靠社区经验。
- **工具路由**：内置搜索/抓取优先；登录、动态渲染、交互、视觉确认、反爬等才升级到 MCP 浏览器；不绑定具体浏览器工具名。
- **DSH 适配**：中文改写、安全与失败边界、引用去重、安装与许可打包。
- **边界**：`use-my-browser` 是 xixu-me/skills 的 MIT 原样再分发，不是本项目原创；nWave 来源内容按 MIT 改写并保留署名。

## 安装

复制两个技能目录到 DSH 的技能根：

- **全局**：`<DSH_HOME>/skills/`（Windows 通常为 `%USERPROFILE%\.dsh\skills\`）
- **项目级**：项目根目录下的 `.dsh/skills/`

Windows PowerShell：

```powershell
Copy-Item -Recurse .\web-research, .\use-my-browser "$env:USERPROFILE\.dsh\skills\"
```

macOS / Linux：

```bash
mkdir -p ~/.dsh/skills
cp -r web-research use-my-browser ~/.dsh/skills/
```

DSH 会监视技能根目录并热加载；新增、改名或 frontmatter 变化后，下一轮的技能目录会更新，无需重启。

## 使用

- **L1 快速查**：只想“查一下/在哪/给个链接”时，直接给 1–3 句答案 + 1–3 条来源。
- **L2 标准调研**：需要对比、判断、核实或多源汇总时，给结论 + 证据表 + 存疑项。
- **L3 深度报告**：尽调、完整调研或需要方法论时，使用完整报告模板与质量门。
- **经验/操作型问题**：攻略、菜谱、使用技巧、维修、体验评测等，允许社区实践经验作为主要依据，但必须符合 `web-research/references/source-rules.md` 第 10 节。
- **高风险主题**：不得只靠社区经验；按规则从严取证并给出风险提示。

`web-research` 先尝试内置的搜索与静态抓取；遇到登录、动态渲染、交互、视觉确认、反爬等情况，再加载 `use-my-browser` 判断并操作浏览器。详细规则和输出格式见 `web-research/SKILL.md` 与 `web-research/references/`。

## 仓库结构

```
web-research/                  # 研究入口：L1/L2/L3、任务分流、工具路由
├─ SKILL.md
├─ ATTRIBUTION.md              # 来源、许可范围与改写说明
├─ LICENSE-nWave-MIT.md        # nWave 的 MIT 许可全文
└─ references/
   ├─ source-rules.md          # 信源标准、交叉验证、时效、经验证据
   └─ report-template.md       # L2 证据表 / L3 报告 / 质量门

use-my-browser/                # 浏览器路由（xixu-me/skills，原样再分发）
├─ SKILL.md
├─ ATTRIBUTION.md
├─ LICENSE                    # MIT
└─ references/（12 篇）
```

## 兼容性

- 适配 DSH 0.2.x 的技能目录与按需加载机制。
- 技能名使用 kebab-case，目录名与 frontmatter `name` 一致，格式为 `<name>/SKILL.md`。
- 使用内置 `web_search` / `web_fetch` 与当前环境提供的任意 MCP 浏览器实现。

## 来源与许可

| 内容 | 来源 | 许可 |
|---|---|---|
| `web-research/` | 改写自 [nWave](https://github.com/nWave-ai/nWave) | MIT；nWave 部分 © 2026 Alessandro Digioia & Michele Brissoni；本项目修改 © 2026 sjx；全文见 `web-research/LICENSE-nWave-MIT.md` |
| `use-my-browser/` | 原样再分发自 [xixu-me/skills](https://github.com/xixu-me/skills) | MIT；© 2026 Xi Xu；全文见 `use-my-browser/LICENSE` |
| README、LICENSE、THIRD-PARTY-NOTICES.md、.gitattributes | 本项目 | MIT；© 2026 sjx；全文见 `LICENSE` |

- 更完整的来源、commit 与许可说明：`THIRD-PARTY-NOTICES.md`、`web-research/ATTRIBUTION.md`、`use-my-browser/ATTRIBUTION.md`。
- 相关项目 [odysseus](https://github.com/odysseus-dev/odysseus)（AGPL-3.0）仅作一般流程概念参考；本仓库不包含其文件或文本，AGPL 仅适用于其上游项目。
- 顶级 `LICENSE` 不改变 `web-research/`、`use-my-browser/` 中第三方作者的版权。

## 免责声明

本项目为个人维护的非官方 DSH 技能分发，与 DeepSeek 官方无隶属或背书关系。内容按“现状”提供，不构成专业建议；涉及医疗、法律、金融等高风险决策时，请咨询有资质专业人士并自行承担使用风险。

## License

本项目原创与适配修改采用 [MIT](LICENSE)。第三方内容按各自许可分发，详见 `THIRD-PARTY-NOTICES.md`。
