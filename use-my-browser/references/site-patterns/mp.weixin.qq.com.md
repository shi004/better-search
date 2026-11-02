---
domain: mp.weixin.qq.com
aliases: [微信公众号, 公众号文章, WeChat article]
updated: 2026-11-02
confidence: high
evidence: 2026-11-02 匿名/静态请求返回带 poc_token 的验证页；同一 URL 在登录态浏览器完整渲染并可读正文
---

# mp.weixin.qq.com

## Platform traits

- Article pages live under `/s?...` with ephemeral `timestamp` / `signature` / `sn` parameters; links copied from search engines or other apps may carry `src=11&timestamp=...&ver=...&signature=...`.
- Anonymous static retrieval (`web_fetch`, `requests`, `curl`) usually receives a verification page whose URL is `/mp/wappoc_appmsgcaptcha?...poc_token=...` and whose visible text is `环境异常，完成验证后即可继续访问` or similar.
- The live browser session renders the same article normally; the page title becomes the article title.
- Article body renders into `.rich_media_content` (also inside `#js_article`).
- Article attachments (`.xlsx` / `.doc` / `.pdf`) are usually published as links to another `mp.weixin.qq.com` article, and the file itself may require the WeChat client to download.

## Effective patterns

- Open the article URL directly in the live browser page, or discover it through a search engine / 搜狗微信 and click the site-generated link; wait for navigation before reading.
- Read body text with `document.querySelector('#js_article')?.innerText || document.querySelector('.rich_media_content')?.innerText`.
- Verify the page title equals the expected article title before trusting the body.
- Cross-check any job/policy claim against the publishing unit's official site; the article is a lead, not the primary source.

## Known pitfalls

- A `poc_token` / `环境异常` verification page is returned to anonymous clients only. It is `static-blocked` (undetermined), never evidence that the logged-in browser is blocked.
- A search-engine or 搜狗微信 list snippet is `static-only` (and partial) at best: it gives a title and a truncated summary, never the article body, attachment, or deadline. Do not treat the snippet as the body or as proof of readability; `static-only` never upgrades to `read-in-browser` without a live read.
- Search-engine `site:mp.weixin.qq.com` results often link to expired or re-signed URLs; prefer opening the fresh link in the browser rather than reconstructing parameters.
- 搜狗微信 time sort (`tsn=1`) may redirect to the search homepage instead of results; treat that as anti-bot friction.
- Do not screenshot only the top of an article: attachments and the job table often sit at the bottom.
