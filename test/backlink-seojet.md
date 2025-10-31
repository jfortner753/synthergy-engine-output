Here’s a quick **legitness scan** of that SEOJet page — what’s coherent, what’s risky, and what doesn’t line up with Google’s rules.

# TL;DR

* They **sell links** (guest posts, “link insertions”) and tell you to “just go get the links” their map prescribes. Selling/placing paid links to pass ranking credit is **explicitly link spam** unless marked `rel="sponsored"` (and then it shouldn’t pass credit). Their pages don’t say they use `rel="sponsored"`. ([SEOJet][1])
* They promote **tiered link building** (“build links to your links”), a classic manipulation pattern Google targets under link spam. ([SEOJet][2])
* Their core pitch hinges on **anchor text “ratios”** and “fill-in-the-blanks” link maps. Google teaches “write good, descriptive anchor text” — no ratios, no fixed percentages. Ratios = a footprint. ([SEOJet][2])

---

## Specific red flags (with receipts)

1. **Paid links presented as an SEO lever**

   * “Guest Posts on high-quality blogs… watch your rankings soar.” Pricing by DA/traffic; delivery timelines; “fix or replace any broken links.” That’s a *commercial link placement* service. Google’s spam policy lists **buying or selling links** for ranking purposes as link spam; paid links must be marked `rel="sponsored"`. The sales copy doesn’t mention that. ([SEOJet][1])

2. **“Link insertions” (retrofits) at scale**

   * They sell link insertions into existing articles with price tiers by DA, promising ranking impact. That’s textbook **paid placement** unless sponsored/nofollowed; if followed, it’s a violation. ([SEOJet][3])

3. **Tiered link building (“links to your links”)**

   * The blog instructs building 2nd/3rd/4th-level links to pump “authority” into your tier-1 links. Google’s policy: creating links **primarily to manipulate rankings** = link spam. Tiering is not named explicitly, but it *is* creating artificial link networks to move PageRank. ([SEOJet][2])

4. **Anchor “ratio” engineering**

   * They push anchor categories and target distributions (e.g., 80–95% “natural” anchors for homepages, then “match the top 10” for inner pages). Google’s guidance is about **clarity and relevance**, not fixed mixes; engineering anchors to match competitor “ratios” is a manipulation footprint. ([SEOJet][4])

5. **Guest posts positioned to pass PageRank**

   * Multiple places say guest posts will “help your rankings.” Google and John Mueller have repeatedly said **guest post links should be nofollowed**; using them to transfer PageRank is against policy. ([SEOJet][1])

6. **Outdated framing & overclaims**

   * The article invokes **E-A-T** (omits the current **E-E-A-T** framing), and promises “up-to-the-minute No. 1 ranked data on backlinks” — vague marketing language with no method transparency. ([SEOJet][2])

---

## Why this matters (risk profile)

* **Algorithmic devaluation / manual action risk:** Paid placements and tiered schemes are exactly what Google’s link spam systems try to detect & neutralize. Money + followed links = risk; at best ignored, at worst a site-wide headache. ([Google for Developers][5])
* **Footprint risk:** Anchor-ratio templating and link maps can produce **predictable patterns** across clients — easy for spam systems to learn and discount. Google advises on anchor *quality*, not quotas. ([Google for Developers][6])

---

## What’s coherent (the fair bits)

* **Backlinks can help** when they’re *editorial, relevant, in-content*, and earned via PR/research/useful assets. Their copy nods at “quality,” but the **products** (paid posts/insertions, anchor quotas, tiering) point toward manipulative implementations. ([SEOJet][2])

---

## Quick vendor due-diligence checklist (copy/paste)

Ask them — in writing:

1. “Do all paid placements use `rel="sponsored"` (or `nofollow`)?” If not, it violates Google policy. ([Google for Developers][7])
2. “Do you build tiered links? If yes, how is that compatible with Google’s link spam policy?” ([Google for Developers][5])
3. “Are anchor ‘ratios’ mandatory? Why not follow Google’s anchor guidance (descriptive/relevant) instead of quotas?” ([Google for Developers][6])
4. “Can you show examples of **editorial** (not paid) in-body links you’ve earned via PR/research, and confirm no compensation?” (This is the real signal.)

---

### Bottom line

Legit link earning = **editorial citations and PR**.
What’s sold here is largely **paid placements + pattern engineering** (tiering, anchor ratios). That’s the kind of thing Google’s spam policies are designed to ignore or punish — and their own pages read like a shopping cart for it. ([SEOJet][1])

[1]: https://seojet.net/guest-post-service/ "High Quality Backlinks From Blogs With Organic Traffic"
[2]: https://seojet.net/blog/build-backlinks/ "How To Get Backlinks To Boost Your Website’s RankingHow To Get Backlinks To Boost Your Website’s Ranking - SEOJet"
[3]: https://seojet.net/link-insertions/ "High Quality Link Insertions From Blogs With Organic Traffic"
[4]: https://seojet.net/blog/anchor-text-ratio-seo/ "Anchor Text Ratio SEO - Faster Rankings With Less Backlinks Anchor Text Ratio SEO - Faster Rankings With Less Backlinks - SEOJet"
[5]: https://developers.google.com/search/docs/essentials/spam-policies?utm_source=chatgpt.com "Spam Policies for Google Web Search"
[6]: https://developers.google.com/search/docs/crawling-indexing/links-crawlable?utm_source=chatgpt.com "SEO Link Best Practices for Google | Google Search Central"
[7]: https://developers.google.com/search/docs/crawling-indexing/qualify-outbound-links?utm_source=chatgpt.com "Qualify Outbound Links for SEO | Google Search Central"
