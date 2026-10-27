# 信源标准（Source Rules）

> 用途：网页信息搜索/调研中判断来源是否可信、如何分级、如何交叉验证、如何处理冲突与时效、如何引用。
> 仅在需要**信源判断或引用**时读取本文件；检索与抓取步骤见 `../SKILL.md`；浏览器操作见 `use-my-browser` 技能；输出结构见 `report-template.md`。

## 1. 默认可信域清单

以下为基线清单（来自 nWave 的 Default Trusted Sources）。域名是**默认档位**，具体页面仍按第 3 节分级与第 5-7 节验证；可按任务需要扩展，但扩展需记录理由。**经验/操作型任务（攻略、菜谱、使用技巧、体验评测等）另见第 10 节。**

### 1.1 academic —— 高信誉（1.0）

| 域名 | 备注 |
|---|---|
| `*.edu`、`*.ac.uk` | 高校域名 |
| `scholar.google.com` | 学术检索 |
| `arxiv.org` | 预印本 |
| `pubmed.ncbi.nlm.nih.gov` | 生物医学文献 |
| `researchgate.net` | 学术社交/全文 |
| `ieee.org`、`acm.org` | 学会出版 |
| `springer.com`、`sciencedirect.com`、`jstor.org` | 学术出版 |
| `nature.com`、`science.org` | 顶级期刊 |

验证要求：优先同行评审、追踪引用、核对作者资质。

### 1.2 official —— 高信誉（1.0）

| 域名 | 备注 |
|---|---|
| `*.gov`、`*.gov.uk` | 政府 |
| `w3.org`、`ietf.org`、`iso.org` | 标准组织 |
| `nist.gov` | 美国标准与技术研究院 |
| `docs.microsoft.com`、`docs.oracle.com`、`docs.python.org` | 官方文档 |
| `kubernetes.io/docs`、`docker.com/docs` | 官方文档 |

验证要求：官方发布、版本追踪、标准符合性。

### 1.3 industry_leaders —— 中高信誉（0.8）

`github.com`、`stackoverflow.com`、`martinfowler.com`、`refactoring.guru`、`enterpriseintegrationpatterns.com`、`microservices.io`、`12factor.net`、`reactivemanifesto.org`、`agilemanifesto.org`、`thoughtworks.com/insights`、`infoq.com`。

验证要求：需至少 1 个高信誉来源交叉、核对作者专业度、参考社区共识。

### 1.4 technical_documentation —— 高信誉（1.0）

`developer.mozilla.org`、`developers.google.com`、`aws.amazon.com/documentation`、`cloud.google.com/docs`、`learn.microsoft.com`、`devdocs.io`、`readthedocs.org`。

验证要求：版本准确性、官方源确认。

### 1.5 open_source —— 高信誉（1.0）

`apache.org`、`eclipse.org`、`cncf.io`、`opensource.org`、`fsf.org`、`linuxfoundation.org`。

验证要求：社区验证、项目成熟度。

### 1.6 medium_trust —— 中信誉（0.6）

`medium.com`、`dev.to`、`hashnode.com`。

验证要求：作者身份验证、至少 3 个独立来源交叉、强制事实核查。

### 1.7 excluded —— 排除（0.0）

`*.blogspot.com`、`wordpress.com`、`tumblr.com`、`pastebin.com`、`quora.com`。

理由：无编辑把关、潜在偏见、质量控制低。动作：拒绝采用、记录警告、寻找替代来源。

## 2. 通用官方源定义（非技术领域补充）

技术域之外的权威来源按“**实体自己的官方渠道**”认定：

| 类型 | 认定方式 | 例子 |
|---|---|---|
| 政府 | 对应政府部门官网，域名含 `gov` | `*.gov`、`*.gov.cn`、`*.gov.uk`、部委官网 |
| 学校 | 学校官网，域名含 `edu` | `*.edu`、`*.edu.cn`、学校招生/教务/科研官网 |
| 公司 | 公司主域名、官方公告/新闻室、官方财报、官方备案信息、官方产品文档 | 企业官网 `about/press/investor` 页面、官方帮助中心 |
| 标准组织 | 国际/国家标准机构 | ISO、IEC、W3C、IETF、国家标准委、行业标准发布机构 |
| 其他权威机构 | 统计/监管/司法/国际组织 | 统计局、监管机构、法院/立法公开渠道、世界银行/WHO 等 |

**第三方规则**：第三方媒体、聚合站、论坛、自媒体只能作为**线索**；必须回到上述官方渠道（或第 1 节高信誉域）核实后才能作为结论依据。**自媒体新闻、匿名帖、营销稿不得作为关键结论的最终依据。**

## 3. 来源分级与评分

对每个实际使用的来源评定档位（域名默认档 + 页面事实核查可升降，升降须在来源分析中写理由）：

| Tier | 分数 | 例子 | 使用要求 |
|---|---|---|---|
| High | 1.0 | `*.edu`/`*.gov`、arxiv/ieee、W3C/IETF、MDN、OSS 基金会、官方文档 | 常规引用即可 |
| Medium-High | 0.8 | 行业领袖（martinfowler.com、stackoverflow、infoq 等） | 需 1 个以上 High 来源交叉 |
| Medium | 0.6 | 社区（medium/dev.to/hashnode 的认证作者） | 作者验证 + 3 源交叉 |
| Excluded | 0.0 | 未验证博客、quora、pastebin、无编辑把关站点 | 拒绝、记录、换替代源 |

## 4. 独立来源与交叉验证（交叉引用）

1. 先明确要验证的具体断言。
2. 找 **2 个以上互不引用**的独立来源（避免循环引用）。
3. 验证独立性 = 不同作者、不同发布方、不同组织。
4. 比对实质内容是否一致（措辞差异可接受）。
5. 每条发现标注：已核实 / 部分核实 / 未核实。
6. **循环引用判定**：B 引用 A 只算 1 个来源；多个来源引用同一原始研究时，引用原始研究。
7. 优先一手来源；二手只在无一手或一手不可得时使用，并标注。
8. 关键结论/不稳定信息（价格、政策、版本、数字）必须额外交叉核对，争议大时增加来源数量。

## 5. 冲突处理

- **记录全部冲突来源**及各自证据（不要只留下支持自己结论的一方）。
- 评估每个来源的可信度（第 3 节 Tier + 第 6 节偏见 + 第 7 节时效）。
- 呈现双方证据与权威判断，明确标注不确定性。
- **裁决顺序**：版本匹配的官方一手来源 > 官方发布说明/变更日志 > 一手示例或数据 > 可靠二手 > 其他二手；裁决理由写进输出。
- 经验类冲突（社区经验之间的分歧）另见第 10.5 节。

## 6. 偏见检测清单

引用前逐条检查；命中即在来源分析中标注并降低置信度：

1. **商业利益**：是否在推销相关产品/服务？
2. **赞助/资助**：是否带赞助或资金关系？
3. **利益冲突**：作者是否从结论中获益？
4. **地理/文化偏见**：是否只覆盖单一地区/文化？
5. **时间偏见**：来源日期是否集中在某一时期？
6. **挑樱桃（cherry-picking）**：是否承认相反证据？
7. **逻辑谬误**：把相关当因果、以权威代替证据等。
8. **免责声明/局限**：是否披露数据来源、样本与限制？

## 7. 时效规则

| 类别 | 最长期限 | 原因 |
|---|---|---|
| 安全漏洞 | 6 个月 | 威胁演变快 |
| 框架版本 | 1 年 | API/实践变化 |
| 云服务文档 | 1 年 | 频繁更新/下线 |
| API 参考 | 1 年 | 破坏性变更常见 |
| 架构模式 | 长期有效 | 核心模式稳定 |
| 方法论参考 | 长期有效 | 基础著作稳定 |
| 语言规范 | 按版本长期有效 | 每版本永久 |
| 研究论文 | 3 年 | 需查后续工作 |
| 行业趋势报告 | 1 年 | 只引用当版 |

过期处理：
1. 检查是否有新版本。
2. 稳定概念可引用并标注 `[Published {year}; concept remains current]`。
3. 时效性内容找当前来源，或把“信息过时”写入知识空白。
4. 不得把过期的安全通告当作当前威胁情报。

## 8. 技术域权威源库（附录：仅技术问题使用）

非技术问题（生活/设计/消费/政策/职业等）请用第 2 节通用定义 + 第 3 节分级；经验/操作型问题（攻略/菜谱/体验等）见第 10 节；本节只作技术类问题的快捷清单。

### 软件架构
martinfowler.com（一手：模式/重构/企业架构）、c2.com/wiki（历史：模式语言起源）、microservices.io（领域）、architecturenotes.co（策展：ADR 与权衡）、infoq.com（行业报道）、thoughtworks.com/radar（趋势/采纳阶段）。

### 云平台
docs.aws.amazon.com、cloud.google.com/docs、learn.microsoft.com、kubernetes.io/docs、docs.docker.com。

### 安全
owasp.org（标准）、nist.gov（政府：CSF/SP 800）、cve.mitre.org / nvd.nist.gov（漏洞库）、csrc.nist.gov（密码标准）、cisa.gov（政府通告）。

### 标准组织
ietf.org / datatracker.ietf.org（RFC）、w3.org、iso.org、ecma-international.org、unicode.org。

### 编程语言与框架
docs.python.org、go.dev/doc、typescriptlang.org、rust-lang.org/learn、developer.mozilla.org（MDN）、docs.oracle.com/javase。

### 数据与数据库
postgresql.org/docs、dev.mysql.com/doc、redis.io/docs、mongodb.com/docs、cassandra.apache.org/doc。

### DevOps/SRE
sre.google、12factor.net、dora.dev、openpolicyagent.org。

### 按主题的检索策略
- **架构**：`{topic} site:martinfowler.com` / `site:microservices.io`；会议 QCon/StrangeLoop/GOTO；书/论文；`site:thoughtworks.com/radar`；本地工作区已有文档/研究笔记（如有）。
- **安全**：`site:cve.mitre.org` / `site:nvd.nist.gov`；`site:cisa.gov` / `site:owasp.org`；`site:nist.gov`；产品特定时查厂商通告；优先近 6 个月。
- **框架/库**：官方文档 → release notes/changelog（版本）→ 迁移指南 `{framework} migration guide {version}` → GitHub issues/discussions → `site:stackoverflow.com`。
- **方法论/流程**：原始作者/出处 → 案例研究 → 批评/替代/比较 → 学术（arxiv/Google Scholar）→ 实践者改编 vs 原始定义。

## 9. 证据标准与引用格式

**证据标准**：直接引用或具体数据；完整归属与引用；技术文档带版本信息；带发布日期或最后更新日期；作者资质（可得时）。

**引用格式**：

```
[1] {Author/Organization}. "{Title}". {Publication/Website}. {Date}. {Full URL}. Accessed {YYYY-MM-DD}.
```

**每个来源的必需元数据**：`来源 URL | 域名 | 访问日期 | 信誉分（Tier） | 验证状态`

**付费墙/受限来源**：标 `[Paywalled]`/`[Restricted Access]`，给出 URL，寻找开放获取替代；找不到时记入“知识空白”。

**禁止**：编造 URL、标题、作者、数字、日期；引用不到就不写该结论。

## 10. 经验类证据规则（社区经验为主要依据的场景）

### 10.1 适用场景

当官方/权威来源对“具体怎么做/实际体验如何”基本不覆盖，或只给规则而实操细节只能来自实践者时，适用本节。典型场景：

- 游戏攻略（打法/路线/配装，随版本变化）；
- 菜谱与烹饪；
- 软件/设备使用技巧、DIY/维修；
- 旅行路线与经验、消费体验/评测（主观）；
- 学习资源与方法、求职/留学经验；
- 办事中的实操细节（非官方规定部分）。

这些场景里若包含规则/事实（政策、收费、时限、安全、版本变更、官方参数），那部分**仍按第 1-9 节官方/一手优先处理**；混合型见 10.2。

### 10.2 任务分层（先判类型）

- **规则/事实型**：按第 1-9 节（官方/一手优先、Tier、交叉验证、时效、冲突）。
- **经验/操作型**：以社区/实践者为主要依据，按 10.3 经验证据标准。
- **混合型**：分开取证、分别标注；官方事实回退 Tier 规则，经验细节按 10.3；输出中标明每条结论的性质。

### 10.3 经验证据标准（替代机械 Tier 排除）

对论坛、贴吧、小红书、B 站、知乎、Steam 评测、美食博客、YouTube、个人博客等来源，按下述标准评估（不因“不是官方”直接判 0；仍须标注来源性质）：

1. **可复现**：步骤/条件完整，普通人能照做；只给结论不给过程的不算强证据。
2. **共识度**：≥2–3 个独立实践者一致（争议大取更多）；单一来源标“个例”，不得当普遍结论。
3. **版本/时间匹配**：游戏版本号、软件版本、设备型号、地区/政策时间；过期内容降级或注明。
4. **作者利益披露**：商家/带货/推广/赞助须标注并降权，但不直接排除。
5. **样本范围**：单次体验 vs 大量用户反馈；区分“个例/常见”。
6. **可验证出处**：能给出链接、日期、版本；给不出且无法复现的不作为证据。
7. **安全/合规**：不得用于规避安全机制或违法用途。

### 10.4 呈现要求

- 每条经验结论标注：来源性质（官方/经验/个例/共识）+ 日期或版本。
- 输出中区分“官方事实”“实践者经验”“我的推断”三类。
- L1 可只给 1–2 条实践来源（带日期/版本）；L2 用证据表的“性质”列；L3 在“发现”中标注证据性质/版本。

### 10.5 冲突处理（经验类）

- 裁决顺序：版本匹配 > 共识度 > 可复现性 > 作者利益披露。
- 无法裁决时给多个方案 + 各自适用条件，不强行统一；明确哪些是社区经验、哪些有官方依据。

### 10.6 高风险例外（不得只靠社区经验）

医疗/用药/心理健康、金融投资、法律、危险 DIY/维修、未成年人安全、安全机制规避等：必须官方/专业来源优先；社区经验只能作补充并给风险提示；沿用第 6 节偏见与第 7 节时效规则。

### 10.7 与 Tier 的关系

- 经验任务不机械套用 Excluded 名单；来源按 10.3 评估，仍需标注性质。
- 一旦结论涉及官方可查事实，回退第 3 节 Tier 与第 4-9 节规则。
- 本节的放宽范围仅限“经验/操作型”证据，不放宽安全、法律、医疗、金融等高风险领域。

## 11. 边界声明

- 本文件**不写**：如何检索/抓取（`../SKILL.md` 工作流）、如何操作浏览器（`use-my-browser`）、输出文档结构（`report-template.md`）。
- 冲突的判断规则在本文件第 5 节（经验类见第 10.5 节）；冲突在输出中的呈现格式见 `report-template.md`。
- 置信度定义与阈值见 `report-template.md` 第 3 节（本文件第 3 节只定义来源分数）。
