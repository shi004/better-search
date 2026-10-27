# better-search

**DeepSeek Harness（DSH）的两个网页研究技能：`web-research` 与 `use-my-browser`。**

> **English** — Two skills for DeepSeek Harness (DSH). `web-research` performs source-first web research: use the built-in search/fetch tools first, escalate to an MCP browser only when the task needs it, treat official and first-party sources as authoritative, use third-party material only as leads that must be traced back, and require URL/date evidence for important conclusions. `use-my-browser` is a vendored MIT-licensed browser-routing skill.
>
> The repository name `better-search` means “better search”. The skill IDs stay `web-research` and `use-my-browser`; renaming the repository does not change them.

本仓库是这两个 DSH 技能的公开分发副本。技能名称、规则与引用结构保持原样；仓库名只用于发布，不改变技能 ID。

## 内容

```
web-research/                  # 入口技能：网页信息搜索与调研
├─ SKILL.md                    # L1/L2/L3 分级、工具路由（内置优先，按需升级浏览器）、工作流
├─ ATTRIBUTION.md              # 来源、commit、许可范围、改写与核验说明
├─ LICENSE-nWave-MIT.md        # nWave 的 MIT 许可全文
└─ references/
   ├─ source-rules.md          # 信源标准：权威源、交叉验证、时效、冲突裁决、经验类证据
   └─ report-template.md       # 输出：L2 证据表、L3 完整报告、置信度、质量门

use-my-browser/                # 浏览器路由规范（来自 xixu-me/skills，原样再分发）
├─ SKILL.md
├─ ATTRIBUTION.md
├─ LICENSE                    # 上游 MIT 许可全文
└─ references/（12 篇）
```

## 安装

把两个技能目录复制到 DSH 的技能根：

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

DSH 会监视技能根目录并热加载：新增、改名或 frontmatter 变化后，下一轮的技能目录会更新，无需重启。技能正文只在模型调用 `skill` 工具或用户显式调用时加载。

## 使用方式

- **L1 快速查**：只问“是什么/在哪/给个链接”时，直接给 1-3 句答案 + 1-3 条来源，不读报告模板。
- **L2 标准调研**：需要对比、判断、核实或多源汇总时，给结论 + 证据表 + 存疑项。
- **L3 深度报告**：尽调、完整调研、需要方法论与质量门时，使用完整报告模板。
- **经验/操作型问题**（攻略、菜谱、使用技巧、维修、体验评测等）：允许社区实践经验作为主要依据，但必须满足 `source-rules.md` 第 10 节的可复现、共识、版本匹配、利益披露、样本范围与可验证出处标准。
- **高风险主题**（医疗、用药、金融、法律、危险操作）：不得只靠社区经验，按规则从严取证并给出风险提示。

浏览器工具名不写死：按当前环境实际提供的 MCP 浏览器工具清单选择能力（打开页面、读取内容、交互、脚本、截图、网络、控制台）。不同 DSH 配置可以使用不同的浏览器 MCP 实现。

## 信源与证据标准

1. **官方与一手优先**：政府、学校、公司官方站点、标准组织、原始文件与直接责任方发布的信息优先。
2. **第三方只作线索**：媒体、自媒体、论坛、聚合页、搜索摘要都不能直接当证据；必须回溯到原始出处，并记录回溯路径。
3. **搜索摘要不是证据**：只摘取原文片段 + 发布日期 + 完整 URL；拿不到原文就不下结论。
4. **独立来源与循环引用**：多个来源可能互相抄同一篇通稿；检查独立性与循环引用，不把转载数量当可信度。
5. **时效与版本**：规则、收费、政策、软件版本等易变信息必须核对发布日期/生效日期/版本。
6. **冲突保留**：不同来源矛盾时保留冲突、说明裁决依据，不静默挑选有利结论。
7. **不编造**：不编造 URL、标题、作者、数字、日期；引用不到就明说“未找到可靠来源”。

详细规则见 `web-research/references/source-rules.md`，输出格式见 `web-research/references/report-template.md`。

## 浏览器路由

`web-research` 先尝试内置的搜索与静态抓取；遇到以下情况才加载 `use-my-browser` 判定并操作浏览器：

- 需要登录态、验证码或用户本人会话；
- 页面由客户端脚本渲染，静态抓取为空壳；
- 需要点击、输入、滚动、上传/下载或视觉确认；
- 需要查看 DOM、Shadow DOM、iframe、网络请求或控制台；
- 页面被限流、反自动化或返回伪 404。

`use-my-browser` 是浏览器是否必需的唯一裁判：一旦判定为 `browser-required`，不得静默退回静态抓取。需要登录或验证码时，由用户接管浏览器；不存储凭据、不绕过付费墙或人机验证。

## DSH 兼容性

- 技能名使用 kebab-case（`^[a-z0-9]+(?:-[a-z0-9]+)*$`），目录名与 frontmatter `name` 一致。
- 每个技能是 `<name>/SKILL.md` 目录包；`references/` 只作为按需读取的资源，不参与技能发现。
- `description` 必填，并作为会话技能目录的摘要；DSH 默认最多渲染 500 个字符。
- `whenToUse` 会被解析并保存，但当前 DSH 的会话目录只渲染 `name` + `description`，不渲染 `whenToUse`。
- 在 DSH `0.2.1-rc.3` 上验证；使用内置 `web_search` / `web_fetch` 与任意 MCP 浏览器实现。

## 来源、许可与版权

本仓库包含改写与再分发的第三方材料。各部分的版权与许可如下：

| 路径 | 来源 | 版权 | 许可 |
|---|---|---|---|
| `web-research/` | 改写自 nWave（commit `da401a8384dc867314ba2f4a5fd802fafa593e4f`） | nWave 部分 © 2026 Alessandro Digioia & Michele Brissoni；适配修改 © 2026 sjx | MIT；全文见 `web-research/LICENSE-nWave-MIT.md` |
| `use-my-browser/` | 原样再分发自 xixu-me/skills（commit `c54367d693e7700bed0e3ebf55c9ac4c61db3b54`） | © 2026 Xi Xu | MIT；全文见 `use-my-browser/LICENSE` |
| `README.md`、`LICENSE`、`THIRD-PARTY-NOTICES.md`、`.gitattributes` | 本仓库原创 | © 2026 sjx | MIT；全文见 `LICENSE` |

补充说明：

- **nWave**（https://github.com/nWave-ai/nWave ，MIT）：`web-research` 的信源分级、权威源库、报告模板与质量门来自其相关技能，已翻译、合并、删减并适配 DSH；nWave 版权与 MIT 全文保留。
- **xixu-me/skills**（https://github.com/xixu-me/skills ，MIT）：`use-my-browser` 的 `SKILL.md` 与 `references/` 原样复制，未修改规则；仅新增 `ATTRIBUTION.md` 说明来源；上游版权与 MIT 全文保留。
- **odysseus**（https://github.com/odysseus-dev/odysseus ，AGPL-3.0，commit `9d0d3720f4ca181d87bef94da826d730acc6d483`）：仅作一般流程概念的设计参考；**本仓库不包含其任何文件或逐字文本**。2026-10-27 以其 `web-research-fallback/SKILL.md` 与本仓库文本做 8-gram 比对，重合为 0。AGPL-3.0 仅约束其上游项目，不适用于本仓库。
- 顶级 `LICENSE` 不会改变 `web-research/` 与 `use-my-browser/` 中第三方作者的版权；详见 `THIRD-PARTY-NOTICES.md`。

## 核验

发布前已执行以下核验（2026-10-27）：

- `use-my-browser` 的 13 个文件（`SKILL.md` + 12 篇 references）与上游 commit 逐字节一致（SHA-256）。
- `use-my-browser/LICENSE` 与上游根目录 `LICENSE` SHA-256 一致。
- `web-research/LICENSE-nWave-MIT.md` 与上游 nWave MIT 文本 SHA-256 一致。
- odysseus 上游文本与本仓库文本 8-gram 重合为 0。
- 仓库不含密钥、凭据、本机绝对路径或会话数据。

## 免责声明

本项目是个人维护的非官方 DSH 技能分发，与 DeepSeek 官方无隶属或背书关系。技能内容按“现状”提供，不构成专业建议；涉及医疗、法律、金融等高风险决策时请咨询有资质的专业人士，并自行承担使用风险。

## License

[MIT](LICENSE) © 2026 sjx。第三方组件另见 `THIRD-PARTY-NOTICES.md` 与各自目录内的许可文件。
