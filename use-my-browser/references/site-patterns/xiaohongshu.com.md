---
domain: xiaohongshu.com
aliases: [小红书, RED, xhs]
updated: 2026-11-02
confidence: medium
evidence: 2026-11-02 登录态浏览器中 /search_result 正常返回 30+ 笔记卡片，未出现登录弹窗
---

# xiaohongshu.com

## Platform traits

- SPA; the logged-in web session carries the auth state. Anonymous or static requests hit login or risk-control walls.
- Search route: `https://www.xiaohongshu.com/search_result?keyword=<urlencoded>&source=web_explore_feed` (may be rewritten with `&type=51`).
- Result cards: `section.note-item`; each card links to `/explore/<note-id>`.
- Content is creator-generated: job posts are usually reposts of official announcements, agency marketing, or personal experience notes.

## Effective patterns

- Navigate to the search route, wait for the cards, then extract per card: text snippet, author, and `/explore/` href.
- Use the note text as a lead only; trace claims to the official announcement before recording them as facts.
- Prefer notes that quote the announcement title plus a deadline, and prefer unit-named or 招聘搬运 accounts for discovery.

## Known pitfalls

- Treating note text as evidence: it often drops eligibility conditions (户籍 / 学历 / 届别) or is outdated.
- Rapid navigation can trigger risk-control or empty states; slow down and re-read instead of retrying hard.
- The "大家都在搜" row contains search suggestions, not content.
