Short answer: you’re right to call BS.

Here’s the quick teardown—using their own page and Google’s rules.

* **Bait-and-switch between claim and samples.** They boast “publishing platforms like Medium, VentureBeat… Sub-Editorial media under Mashable, Bloomberg, The Guardian, and The New York Times,” then their **actual “Monthly Backlinks Example”** is Pexels, TripAdvisor, Quora/Pinterest profiles, Posteezy, Pastelink, a Laravel pastebin, Ranker profile, Academia.edu, PBase—i.e., user profiles and paste sites anyone can make in minutes. That’s not editorial coverage. ([support.soogle.io][1])

* **“High-DR” is a smokescreen.** Google doesn’t use Moz DA or Ahrefs DR as ranking signals; those are third-party metrics. Selling “high-DR links” is classic agency theater. ([support.google.com][2])

* **Most sample placements are UGC/profile links—commonly rel=ugc/nofollow.**
  Quora: outbound links are nofollow (Ahrefs confirmed with examples). Pinterest profiles commonly nofollow/indirect; they’re for referral, not PageRank. Reddit links are typically nofollow/UGC. By Google’s own guidance, UGC/nofollow links aren’t endorsements and shouldn’t pass ranking credit (treated as “hints,” not signals you can buy at scale). ([Ahrefs][3])

* **The specific URLs are low-signal “self-serve” pages.**
  The Pexels “backlink” is just a blank profile listing a site URL; the Pastelink and Laravel paste pages are copy-paste link dumps. None are editorial, topical, or earned—exactly the kind of thing Google ignores as link spam/noise. ([Pexels][4])

* **“Guaranteed backlink delivery” + mass self-serve sites = link scheme risk.** Google’s spam policies call out creating links “primarily to manipulate rankings,” including using services to mass-create links. Guarantees tied to quantity on profile/paste sites are a bright red flag. ([support.soogle.io][1])

* **“Contextually relevant” is contradicted by the list.** Stock-photo profiles, generic pastebins, and random social/profile pages are not topical endorsements; they’re low-trust UGC surfaces whose outbound links platforms intentionally de-value to prevent abuse. ([support.soogle.io][1])

What to do in 60 seconds to verify any “backlink report”:

1. **Open 10 samples.** Is the link in the main article body by an editor, or in a user profile/paste page? (Profiles/pastes ≈ junk.)
2. **Check rel attribute.** If you see `rel="nofollow"` or `rel="ugc"` → don’t count it toward “authority.” (It can still send referral clicks—that’s different.) ([Google for Developers][5])
3. **Ignore DR/DA.** Judge page-level relevance and whether humans would click it; Google doesn’t rank on DR/DA. ([support.google.com][2])
4. **Scan for spam policy conflicts.** Promised volume from self-serve sites = link scheme risk. ([Google for Developers][6])

Bottom line: their own “sample report” shows profile/paste links that are mostly nofollow/UGC, not earned coverage, and misrepresented as “high-authority” SEO value. That’s not “real authority,” and it’s not what moves rankings in 2025.

[1]: https://support.soogle.io/en/articles/11389379-sample-backlink-report " Sample Backlink Report | Soogle Help Center"
[2]: https://support.google.com/webmasters/thread/104618869/domain-authority-domain-rating-is-not-improving?hl=en&utm_source=chatgpt.com "Domain Authority & Domain Rating is not improving"
[3]: https://ahrefs.com/blog/nofollow-links/?utm_source=chatgpt.com "Nofollow vs. Follow Links: Everything You Need to Know"
[4]: https://pexels.com/%40shoe-lace-supply-2154193278 "Shoe Lace Supply - Photography"
[5]: https://developers.google.com/search/docs/crawling-indexing/qualify-outbound-links?utm_source=chatgpt.com "Qualify Outbound Links for SEO | Google Search Central"
[6]: https://developers.google.com/search/docs/essentials/spam-policies?utm_source=chatgpt.com "Spam Policies for Google Web Search"
