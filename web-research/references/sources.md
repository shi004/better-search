# 信源清单与分级（Sources）

> 本文件只回答“去哪里找、默认怎么分级、平台账号是否官方”。
> 核验、交叉验证、冲突裁决、偏见、时效、引用格式、经验证据标准见 `source-handling.md`；输出格式见 `report-template.md`。
> 域名是默认档位；具体页面仍按 §3 分级，并按 `source-handling.md` 验证。

## 1. 默认可信域清单

以下为基线清单（来自 nWave 的 Default Trusted Sources）。域名是**默认档位**，具体页面仍按 §3 分级与 `source-handling.md` 验证；可按任务需要扩展，但扩展需记录理由。**经验/操作型任务（攻略、菜谱、使用技巧、体验评测等）另见 `source-handling.md` 第 6 节。**

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

验证要求：需至少 1 个高信誉来源交叉、核对作者专业度、参考社区共识。平台上的内容仍需看具体作者/页面，不因域名自动升级。

### 1.4 technical_documentation —— 高信誉（1.0）

`developer.mozilla.org`、`developers.google.com`、`aws.amazon.com/documentation`、`cloud.google.com/docs`、`learn.microsoft.com`、`devdocs.io`、`readthedocs.org`。

验证要求：版本准确性、官方源确认。

### 1.5 open_source —— 高信誉（1.0）

`apache.org`、`eclipse.org`、`cncf.io`、`opensource.org`、`fsf.org`、`linuxfoundation.org`。

验证要求：社区验证、项目成熟度。

### 1.6 medium_trust —— 中信誉（0.6）

`medium.com`、`dev.to`、`hashnode.com`。

验证要求：作者身份验证、至少 3 个独立来源交叉、强制事实核查。这些是发布平台，作者/机构仍需单独核验。

### 1.7 lead_only —— 仅线索（0.0）

以下来源默认**不作为结论证据**，但也不拒绝使用：把它们当线索检索，记录 URL/日期/账号，再回到官方/一手或经独立核验后升级。

| 域名/类型 | 说明 |
|---|---|
| `*.blogspot.com`、`wordpress.com`、`tumblr.com` | 托管博客：可能是个人、媒体或官方；先按 §2.1 判账号主体 |
| `pastebin.com` | 匿名粘贴，默认仅线索 |
| `quora.com` | 问答 UGC，默认仅线索 |
| 未验证个人博客、无编辑把关站点、匿名帖 | 默认仅线索 |

注意：平台域名不等于内容性质。公司官方博客托管在 `wordpress.com`/`*.blogspot.com` 时，经 §2.1 验证账号主体后可按官方一手处理。

### 1.8 platform_community —— 第三方媒体、平台与社区（默认仅线索）

平台只是载体，不等于信源。同一平台可能同时有官方账号、媒体号、个人号。以下平台默认作为**线索入口**：

- 第三方媒体、聚合站；
- 微信公众号（`mp.weixin.qq.com`）：账号主体决定官方性；官方认证号按 §2.1；个人号/自媒体/转载按线索；
- 微博、小红书、B 站、知乎、贴吧/论坛、Steam 评测、小黑盒、抖音、快手、YouTube、美食博客/个人博客。

**评论区与回复**：帖子/视频/文章下的评论区、回复、弹幕、留言、楼中楼默认属于同平台 UGC 线索，不是独立信源。需要全面搜索时可按主题抽样展开；记录原帖 URL、平台、评论/回复时间、账号或匿名状态、抽样范围；同一帖/同一视频下的多条评论只算一个线索池。官方账号的官方回复按 §2.1 判定；刷评、控评、广告、断章取义或截图不能作为关键结论依据。评论动态加载/登录可见时按 `../SKILL.md` 第 2 节升级浏览器，不绕过登录/验证码；打不开就记录未覆盖。

取证时至少检查：

1. 账号主体/认证，以及它与所涉实体的关系；
2. 内容是原创、转载、切片还是营销；
3. 发布日期、版本/型号/地区是否匹配；
4. 是否有广告/赞助/带货披露；
5. 截图、封面、搜索摘要不能替代原文；视频记录关键时间点；
6. 同一内容是否只是多平台搬运；
7. 评论区/回复/弹幕是否只是同一帖、同一账号或同一话术的重复，是否存在刷评/控评/广告。

具体经验证据标准见 `source-handling.md` 第 6 节。

## 2. 通用官方源定义（非技术领域补充）

技术域之外的权威来源按“**实体自己的官方渠道**”认定：

| 类型 | 认定方式 | 例子 |
|---|---|---|
| 政府 | 对应政府部门官网，域名含 `gov` | `*.gov`、`*.gov.cn`、`*.gov.uk`、部委官网 |
| 学校 | 学校官网，域名含 `edu` | `*.edu`、`*.edu.cn`、学校招生/教务/科研官网 |
| 公司 | 公司主域名、官方公告/新闻室、官方财报、官方备案信息、官方产品文档 | 企业官网 `about/press/investor` 页面、官方帮助中心 |
| 标准组织 | 国际/国家标准机构 | ISO、IEC、W3C、IETF、国家标准委、行业标准发布机构 |
| 其他权威机构 | 统计/监管/司法/国际组织 | 统计局、监管机构、法院/立法公开渠道、世界银行/WHO 等 |

### 2.1 平台账号的官方性判定（含微信公众号）

平台账号的“官方性”取决于**账号主体与所涉事实的关系**，不是平台域名，也不是认证标识本身。

判定顺序：

1. 账号是否由所涉实体认证/运营（公众号认证主体、微博认证、机构号、官方频道）。
2. 实体官网、官方新闻稿、官方 App/客服页是否链接该账号。
3. 内容性质：官方公告/原创，还是转载/评论/营销。
4. 不能仅凭账号名含品牌词判断官方；仿冒号按线索处理。

微信公众号特别规则：

- `mp.weixin.qq.com` 文章由该实体认证公众号发布，且内容属于该实体自身业务/职权范围，可按官方一手处理。
- 个人号、自媒体号、未知主体、官方媒体的报道、官方号的转载，均按第三方/二手线索。
- 截图、聊天记录、转述文本不算原文；必须保留文章 URL、公众号名称、认证主体、发布日期、访问日期。
- 文章被删除时记录“已删除”，改用官网/其他官方渠道核实，不凭截图补结论。

**第三方规则**：第三方媒体、聚合站、论坛、社交平台、自媒体默认只能作为**线索**；其中经 §2.1 判定为所涉实体官方账号的，可按官方一手处理；官方账号转载他人内容仍按二手处理。其他线索必须回到官方渠道或经独立核验后才能作为结论依据。**未经核验的自媒体新闻、匿名帖、营销稿不得作为关键结论的最终依据。**

## 3. 来源分级与评分

对每个实际使用的来源评定档位（域名默认档 + 页面事实核查可升降，升降须在来源分析中写理由）：

| Tier | 分数 | 例子 | 使用要求 |
|---|---|---|---|
| High | 1.0 | `*.edu`/`*.gov`、arxiv/ieee、W3C/IETF、MDN、OSS 基金会、官方文档 | 常规引用即可 |
| Medium-High | 0.8 | 行业领袖（martinfowler.com、stackoverflow、infoq 等） | 需 1 个以上 High 来源交叉 |
| Medium | 0.6 | 社区（medium/dev.to/hashnode 的认证作者） | 作者验证 + 3 源交叉 |
| Lead only | 0.0 | 未验证博客、quora、pastebin、匿名/无编辑把关站点、平台 UGC 线索 | 仅作线索；核验后按实际来源升级；不直接拒绝 |

平台/社区来源不按域名自动给分：官方账号按 §2.1 视为官方一手；经验/体验内容按 `source-handling.md` 第 6 节评估；其余按线索处理。平台名称出现在 §1.8 不代表该平台所有内容都低可信。

## 4. 技术域权威源库（附录：仅技术问题使用）

非技术问题（生活/设计/消费/政策/职业等）请用第 2 节通用定义 + 第 3 节分级；经验/操作型问题（攻略/菜谱/体验等）见 `source-handling.md` 第 6 节；本节只作技术类问题的快捷清单。

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

## 5. 来源扩展与边界

- 可按任务扩展域名/平台；扩展需在来源分析或研究记录中写理由。
- §1.7/§1.8 是默认线索，不是永久黑名单；账号主体/内容性质符合 §2.1 的可升级。
- 本文件不写核验流程、冲突裁决、时效判断或输出结构；这些分别见 `source-handling.md` 与 `report-template.md`。
