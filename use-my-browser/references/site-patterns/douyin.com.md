---
domain: douyin.com
aliases: [抖音, Douyin]
updated: 2026-11-02
confidence: medium
evidence: 2026-11-02 登录态浏览器中 /search/<keyword> 可加载；DOM 快照为空但等待后 body.innerText 含视频卡片与平台 AI 回答
---

# douyin.com

## Platform traits

- SPA search route: `https://www.douyin.com/search/<urlencoded keyword>`; the page title may load later than the DOM.
- The accessibility snapshot can be empty or near-empty while the page has rendered content; `document.body.innerText` becomes the reliable read after a short wait.
- Results include video cards (author, caption, publish date, like count) and a platform-generated "为你生成回答" summary block.
- Anonymous or static retrieval is heavily challenged; use the logged-in live browser.

## Effective patterns

- Navigate, wait about 2-3 seconds, then read `document.body.innerText` and/or card elements for captions mentioning 招聘.
- Open the author/account page for likely-official accounts (for example local talent-market accounts).
- Use 抖音 for signal detection only: job listings are mostly blue-collar or agency-promoted; corroborate everything on the employer's official page.

## Known pitfalls

- The platform AI summary is generated text, not a source; never cite it as evidence.
- Empty accessibility snapshot does not mean an empty page; read `body.innerText` before concluding "no results".
- Captions often omit deadlines and eligibility, and the video may be a repost with no official link.
