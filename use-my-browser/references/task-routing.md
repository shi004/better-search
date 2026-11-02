# Task Routing

This reference decides whether the task should stay on a static retrieval path or escalate into live browser work. It is about evidence quality and route selection, not page-operation mechanics.

## Goal-first routing

Start every task by answering two questions:

1. What outcome are we trying to produce?
2. What evidence would prove that outcome?

That framing should decide the route. Do not start from "which tool do I want to use?" Start from "what would count as done?"

Good examples:

- "Extract the page title and canonical URL from a known public page" is a static retrieval task.
- "Confirm whether the logged-in settings page still shows the new toggle after saving" is a live browser task.
- "Download the media source if it is exposed in the DOM, otherwise inspect the rendered video state" starts as media-aware routing and may escalate into browser plus media inspection.

Each step should produce evidence that moves the task closer to done. If the current route stops improving the evidence, change the route instead of retrying the same tactic. Escalate when needed, but do not downgrade a task that has already been classified as `browser-required`.

## Static vs live browser decision

Default to direct retrieval when browser state is not the point.

Use this quick routing table when the task shape is still ambiguous:

| Scenario                                                                          | Tool               |
| --------------------------------------------------------------------------------- | ------------------ |
| Search snippets or keyword results to discover likely sources                     | Web search         |
| The URL is known and you want targeted information extracted from the page        | Page retrieval     |
| The URL is known and you need raw HTML such as `meta` tags or JSON-LD             | `curl`             |
| The task depends on login state, rendered UI, or free-form in-browser exploration | Live browser stack |
| The site defeats static access methods or requires rendered-state inspection      | Live browser stack |
| Content lives on a logged-in social/community platform or WeChat article page      | Live browser stack |

Stay on the static path when:

- you already know the URL
- you need text, metadata, raw HTML, structured tags, or a small deterministic field set
- the task does not depend on login state, rendered interaction, gestures, or visible confirmation
- a browser action would only repeat what page retrieval or `curl` can already prove

Escalate to live browser work when:

- rendered state is itself the evidence
- the site requires login state, route transitions, expansion, hover, upload, or keyboard interaction
- the next step is easier to discover from the page than from URL guesswork
- static retrieval stops improving the answer and the remaining uncertainty is in the browser UI

Use this escalation ladder:

1. Try the cheapest direct retrieval path first.
2. Extract only the fields you actually need.
3. Escalate into the browser once visible state, session state, or interaction becomes the missing evidence.

The browser is not a purity prize. It is the right tool once the cheaper route no longer answers the real question.

The live browser path does not require a known URL. You can start from whatever entry point is available and navigate through the page itself by searching, clicking, and following links. Web search, page retrieval, and `curl` do not carry login state.

### Programmatic vs live browser modes

Programmatic access is usually faster when the target is already expressible as a stable URL plus a small extraction goal.

Live browser work is usually safer when the site expects a real page session and the next step is easier to discover through visible interaction than through URL construction.

Live browser work is also a probe. A small amount of real interaction can reveal:

- canonical links
- redirect behavior
- hidden parameters
- actual route shape
- UI-specific confirmation states

Once the page gives you a link, prefer that site-generated `href` over a hand-built URL. The DOM link is more likely to preserve routing details and required parameters.

## Static-first document and metadata retrieval

When the task is still on the static path:

1. Fetch the stable URL with the cheapest direct retrieval tool.
2. Extract the small fixed field set you actually need, such as `og:title`, `og:type`, canonical metadata, or RFC title / number / publication date.
3. Return to the browser only if visible confirmation is still needed, the page is client-generated, or the static response remains ambiguous.

## Login judgment

Do not escalate to user login just because a page looks restricted. First answer the operational question: can the target content or action already be reached from the current session?

Use this sequence:

1. Go to the most direct safe target you can inspect.
2. Check whether the content or control is already visible or extractable.
3. Continue without asking for login help if the task is already completable.
4. Ask for login only when the task remains blocked and login is a plausible unlock for the specific missing content or action.

Current live browser sessions often already carry the needed authenticated state. Do not assume a fresh login is required until the target content remains blocked in the current session.

Good evidence that login is truly required:

- the page redirects to a login route instead of the target view
- the content itself is missing behind an auth wall
- the control you need has been replaced by a sign-in requirement
- a verified domain note says the workflow depends on authenticated state

Be careful with false positives:

- a login modal does not always block DOM extraction
- a site can look restricted while still exposing the needed links or metadata
- "not found" can reflect the wrong route shape, missing parameters, or anti-automation behavior rather than true absence
- a static 403 / 412 / `环境异常` / captcha / `poc_token` page returned to `web_fetch`, `requests`, or `curl` is **not** evidence that the logged-in browser session is blocked
- do not carry a static failure forward as "需登录 / 被拦截" without a live read

When login is needed, say exactly what is blocked. The default wording is:

> "The current page is still unable to access [specific content] without login. Please sign in to [site name] in your current browser session, then tell me to continue."

After the user logs in, keep the existing workflow and continue with a refresh or a fresh task-owned page rather than rebuilding the whole browser setup from scratch.

## Access-state claims

A claim that a source is "blocked", "requires login", or "cannot be read" is an evidence claim, not a fallback. Record an access state per source before making it.

| Access state | Meaning | Allowed wording |
| --- | --- | --- |
| `read-in-browser` | Content was read in the live browser session | "可读 / read via browser" |
| `static-only` | Static retrieval only, no browser read; completeness is stated in Evidence (complete / partial / stale) | "static-only, browser not used；完整性见 Evidence" — never upgrade this to `read-in-browser` without a live read |
| `static-blocked` | Static retrieval hit a wall (`环境异常`, captcha, `poc_token`, 403, 412) and no browser read was attempted | "静态抓取受限（未证实不可读）/ undetermined" |
| `browser-blocked` | A live-browser attempt failed and the URL plus page text are recorded | "blocked / 需登录" (only state that allows this) |
| `capability-missing` | The live browser stack or the required logged-in session is unavailable in this agent | "未尝试：本会话无登录态浏览器 / capability missing" — an environment statement, never a source verdict |
| `not-attempted` | No attempt yet | no verdict |

Rules:

- The only state that may produce "需登录 / 被拦截 / blocked" is `browser-blocked`, with the URL and the page text that shows the wall.
- Static-fetch failures on walled sites are `static-blocked`, which is **undetermined**, not a conclusion about the site.
- If the user or runtime context states a session is logged in, that outranks any anonymous-fetch failure: do one live read before reporting anything.
- Sub-agent reporting (authoritative list; other files reference this instead of restating it): `read-in-browser` only when the sub-agent owns a live session and did the read itself; otherwise `static-only`, `static-blocked`, `capability-missing`, `not-attempted`. Only the page owner may declare `browser-blocked`.
- `capability-missing` describes the agent's environment, not the source: record it together with the missing capability (no browser stack / no logged-in session) and hand the source to an owner that has the capability. Record it only after a capability probe actually failed (tool inventory checked, or one call attempted) and include that evidence; if no probe was made, use `not-attempted`.
- Mixed evidence: if static retrieval returns only discovery fields (search snippet, list title, summary) while the substantive content (article body, attachment, job table) hits a wall, record the obtained fields as `static-only` **and** the substantive claim as `static-blocked`; never present a snippet as the body. When a single source yields mixed evidence, use one ledger row per claim instead of collapsing both into one state.
- `static-only` does not mean incomplete: when static retrieval obtained the full text (typical for a `.gov.cn` notice), keep `static-only` and write `complete` in Evidence. Only a live read may change the state to `read-in-browser`.
- Precedence: when a task names walled sources, this access-state model overrides static-first defaults from other skills (for example `web-research`'s "prefer built-in search, escalate as needed"). Escalation is the default for these sources.
- When the deliverable's value depends on platform content, include a short source-access ledger in the output.

Example ledger:

| Source | Route | Access state | Evidence |
| --- | --- | --- | --- |
| 公众号文章 A | live browser | `read-in-browser` | article body read, title matched |
| 搜狗微信列表（同一篇 A） | static fetch | `static-only` | only title + snippet obtained (partial); snippet is not the body |
| 某市人社局公告 | static fetch | `static-only` | full text + deadline obtained statically (complete); browser not used |
| 小红书 keyword search | live browser | `read-in-browser` | 30 cards parsed; note text used as lead only |
| 某招聘网站列表 | static fetch | `static-blocked` | 412 response; browser not attempted → undetermined |
| 某平台（本会话无登录态） | none | `capability-missing` | no live session in this agent; escalated to browser owner |

## Primary-source verification

Verification means finding the most authoritative source that can actually support the claim. Search engines and aggregators help you discover candidates; they do not prove correctness on their own.

Prefer these source classes:

| Information type       | Primary source                                        |
| ---------------------- | ----------------------------------------------------- |
| Policy or regulation   | The publishing authority's official site              |
| Company announcement   | The company's newsroom or official announcement page  |
| Academic claim         | The original paper or the institution's official page |
| Tool behavior or usage | Official docs and source code                         |

Use repeated secondary reporting only as a discovery aid. Once you have a credible lead, go read the original text.

Social-platform posts (公众号/小红书/抖音/微博) are leads, not evidence. Trace each claim to an official or first-party page before recording it as a fact; if no first-party page can be found, label it as a single non-official source.

If the primary source cannot be located after reasonable effort:

- fall back to the most authoritative original secondary source you can find
- say explicitly that the evidence is second-hand
- say explicitly if the conclusion rests on a single non-official source

Useful wording:

> "I couldn't locate the official source. The following is based on [source], so it may contain transcription or interpretation error."

If only one non-official source supports the conclusion:

> "This conclusion currently rests on a single non-official source."

## Reference boundary

This file chooses the route. It should not become a second routing hub.

Once you know which route the task needs, return to [the skill entrypoint](../SKILL.md) and load the next reference from the entrypoint's loading guide. That keeps reference loading one level deep and makes the entrypoint the only place that fans out to other files.
