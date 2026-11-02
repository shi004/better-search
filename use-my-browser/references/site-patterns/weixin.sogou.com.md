---
domain: weixin.sogou.com
aliases: [搜狗微信, 搜狗微信搜索]
updated: 2026-11-02
confidence: medium
evidence: 2026-11-02 登录态浏览器中 weixin?type=2&query=... 正常返回结果；结果链接跳转后落在 mp.weixin.qq.com
---

# weixin.sogou.com

## Platform traits

- Search endpoint: `https://weixin.sogou.com/weixin?type=2&query=<urlencoded>`; `type=2` is article search.
- Results render as `li` blocks: title anchor `h3 a`, snippet `.s-p`, and a source/date line inside the same `li`.
- Result hrefs are redirect links `https://weixin.sogou.com/link?url=...&type=2&query=...&token=...`; following one eventually lands on `mp.weixin.qq.com/s?...` with `src=11&timestamp=&ver=&signature=` parameters.
- There is no reliable per-article date filter exposed in the URL; results are relevance-ranked.

## Effective patterns

- Search, then extract `{title, snippet, href}` from `li` elements before clicking.
- Follow the site-generated link (click or `page.goto(link)`) and wait for the cross-domain navigation; then read the article with the `mp.weixin.qq.com` pattern.
- Use 搜狗微信 only for discovery; the authoritative version of the same announcement is usually on a `.gov.cn` or official unit site.

## Known pitfalls

- Appending `tsn=1` (time-sort) can redirect to `https://weixin.sogou.com/` instead of results; treat it as anti-bot friction and fall back to relevance order.
- Anonymous static fetches of the result page may be challenged; use the live browser.
- Titles are truncated in the list and snippets may be stale; always open the article to confirm the publish date and deadline.
