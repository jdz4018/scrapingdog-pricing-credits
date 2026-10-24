# scrapingdog api: Pricing, Credit Costs, and What Your Plan Actually Buys — With a Side-by-Side Look at ScraperAPI

The Scrapingdog API is a credit-based scraping service: you send a request to its `/scrape` endpoint with your API key and a target URL, and the service handles proxies, browsers, and CAPTCHAs before returning the page. Paid plans start at $40/month for 200,000 credits, and there's a permanent free tier with 100 credits if you want to poke at it first.

Most people searching for "scrapingdog api" are really trying to answer a bigger question: which scraping API deserves my budget, and how many requests will my money actually buy? That second half is where most reviews go vague. This article covers what Scrapingdog offers and charges, then puts it next to ScraperAPI — a service that says it handled over 11 billion requests in the past 30 days — with the two details that decide your real cost: per-domain credit pricing and what happens when your credits run out.

> **Quick take:** For most projects, ScraperAPI's Hobby plan at **$49/month** (100,000 credits, 20 concurrent threads, annual billing drops it to $44.10) is a solid starting point, and the **7-day trial gives you 5,000 credits without a credit card** — enough to test your real target sites before spending anything. 👉 [Start the free trial — 5,000 credits, no credit card](https://www.scraperapi.com/?fp_ref=coupons)

## What does the Scrapingdog API actually offer?

Scrapingdog gives you one general-purpose scraping endpoint plus a set of dedicated APIs for specific platforms — Google Search, Google News, Google Jobs, Amazon, YouTube, and more. The company describes the library as 60+ site-specific scrapers on its SDK listing, while its pricing FAQ says a single subscription unlocks "all 40+ APIs." Either way, the shape is the same: one account, many pre-built endpoints, no add-on purchases.

Two recent additions are worth knowing about if you're building in 2026-era stacks:

- Official SDKs for Node.js and Python. The `scrapingdog-sdk` npm package was updated in July 2026 and covers every endpoint, with a generic `get()` method for anything released after you installed it.
- An MCP server that plugs the API into Claude, Cursor, and other AI agents — useful if your "scraper" is increasingly an LLM workflow.

The pricing FAQ also spells out the billing behavior plainly: credits are shared across every API on your plan, and failed, blocked, and timed-out requests are automatically credited back. "You only ever pay for data you successfully receive." That last promise matters more than headline pricing, and it's something both services in this article honor.

## Scrapingdog pricing: what the tiers actually look like

Scrapingdog's pricing page lists 29 plans, from a free tier up to $30,000/month, under names like LITE, PRO, TITAN, and NOVA. Every plan unlocks every API — the tiers differ only in credits, concurrency, and support level. The plans most people will realistically consider:

| Plan | Price | Credits | Concurrency |
| --- | --- | --- | --- |
| FREE | $0 forever | 100 | 1 |
| LITE | $40/mo | 200,000 | 5 |
| STANDARD | $90/mo | 1,000,000 | 50 |
| PRO (flagged as popular) | $200/mo | 3,000,000 | 100 |
| PREMIUM | $350/mo | 6,000,000 | 150 |
| BUSINESS | $500/mo | 9,000,000 | 200 |
| BUSINESS PLUS | $1,000/mo | 19,000,000 | 250 |

Above that, the ladder keeps climbing in the same rhythm — corporate tiers from $2,000 to $3,000/month, enterprise tiers from $4,000 to $6,000, then GLOBAL, ULTRA, TITAN, and NOVA lines topping out at NOVA PRO: $30,000/month for 1.1 billion credits and 2,200 concurrent requests. Custom plans are available for workloads beyond that, with dedicated infrastructure and a named account manager.

Two billing details from the official page:

- **Annual billing** is priced at ten months for twelve — effectively two months free on every plan. The page shows a Monthly/Annual toggle, though the exact conditions behind its "2 months Extra" label aren't spelled out anywhere, so confirm the discounted figure at checkout rather than assuming.
- **Upgrades are not prorated.** You pay the full amount for the new plan either way. On an upgrade, your unused credits roll over; on a downgrade, your credits reset to the new plan's allowance. That's an unusual quirk — upgrading mid-month costs more than a prorated model would — but the new credits are available immediately.

One caution on the free tier: one third-party roundup listed 200 free credits, but Scrapingdog's own pricing FAQ states "every account starts with 100 free credits." The official number is 100.

Also worth noting before you pick a plan: concurrency is capped hard. A third-party review (proxyhorizon, 2026) points out that Lite allows just 5 parallel requests, Standard 50, and Pro 100, which throttles heavily parallel scrapers. If your architecture fires hundreds of requests at once, the concurrency number will bottleneck you before the credits do.

## The detail most reviews skip: credits are not requests

Here's the part that trips people up. "200,000 credits" does not mean "200,000 scraped pages." Both Scrapingdog and ScraperAPI charge differently depending on the domain and the parameters you use, and the difference is dramatic.

ScraperAPI documents its costs openly, and they're worth internalizing because they apply broadly to how this whole category of tools prices:

| Request type | Credit cost |
| --- | --- |
| Standard page | 1 |
| Amazon, Walmart, eBay | 5 |
| Google, Bing (all subdomains) | 25 |
| LinkedIn | 30 |
| Anti-bot bypass (Cloudflare, Datadome, PerimeterX, Akamai) | +10 per scrape |
| `render=true`, `premium=true`, `screenshot=true` | +10 each |
| `ultra_premium=true` | +30 |

Scrapingdog works the same way structurally — its pricing page lists premium proxies at 10 credits and its AI parser at 5 credits per use.

Do the math on a realistic example: if your project scrapes Google SERPs at 25 credits per request, a 100,000-credit plan buys you about 4,000 searches, not 100,000 pages. A pricing page headline of "200K requests" can mean very different things depending on whether you're scraping blog posts or LinkedIn profiles.

The practical move: estimate before you buy. ScraperAPI gives you three ways to check the exact cost of any URL — the Domain Cost Estimator in the dashboard, the API Playground for test runs, and a direct endpoint (`api.scraperapi.com/account/urlcost`) that accepts all the same parameters as a real request and returns the credit price. Every response also includes an `sa-credit-cost` header showing what that request actually consumed, and you can set a `max_cost` parameter to cap any single request. 👉 [Check each plan's current price and credit terms](https://www.scraperapi.com/pricing?fp_ref=coupons)

## ScraperAPI's full plan lineup

ScraperAPI's pricing page shows seven fixed tiers plus a custom Enterprise option. Every tier includes JS rendering, premium residential and mobile IPs, CAPTCHA and anti-bot bypass, automatic JSON parsing, custom sessions and headers, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee.

| Plan | Monthly | Annual (per month) | Credits | Concurrency | Buy |
| --- | --- | --- | --- | --- | --- |
| Hobby | $49 | $44.10 | 100,000 | 20 | [ Get Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | [ Get Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | [ Get Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling (most popular) | $475 | $427.50 | 5,000,000 | 200 | [ Get Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | [ Get Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | [ Get Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom quote | — | 22,000,000+ | 500+ | [ Contact sales](https://www.scraperapi.com/?fp_ref=coupons) |

Annual billing takes 10% off every plan. A few restrictions on the cheaper tiers don't show up in the headline numbers: Hobby and Startup get geotargeting for US and EU locations only, and their analytics dashboards only retain the last 30 days of data. If you need to target Japan or Brazil, or you want to review scraping performance over longer stretches, Business is where both restrictions lift. Enterprise pricing is custom, with one wrinkle from the docs: requests to "Ultra Premium" domains carry their own minimum rate even on custom deals — $3 per thousand requests without rendering, $7 with rendered pages.

## What happens when you run out of credits

This is the other question comparison posts tend to hand-wave, and the two services handle it differently.

**ScraperAPI:** by default, scraping pauses until your credits renew. Beyond that, your options depend on the plan. Hobby through Professional can switch on auto-upgrade, which moves your account to the next tier automatically when credits run out — opt-in, not a surprise bill. Scaling and above support pay-as-you-go, letting you keep scraping past your limit at a fixed per-credit rate up to a monthly spending cap you set. Exceeding your concurrency limit returns a 429 response: the request is rejected rather than queued, and it costs you nothing.

**Scrapingdog:** once credits are used up, API requests return an over-limit response until they reset on your next billing date. Failed and blocked requests are credited back automatically, and you can upgrade at any time from the dashboard with credits available immediately.

Both only bill successful requests. ScraperAPI's documentation is unusually specific about it: only responses with 200 or 404 status codes are charged, plus requests you cancel yourself before the 70-second timeout. Either way, a CAPTCHA the service can't solve shouldn't cost you money — still, it's worth verifying with a few deliberate test requests during whatever trial you use, because that behavior is the difference between a predictable bill and a nasty one.

## Scrapingdog vs ScraperAPI: which fits which project?

Both are established, credit-based scraping APIs, and both handle proxies, browsers, and CAPTCHAs for you. The honest differences are in the entry points, the trial, and the tooling:

|  | Scrapingdog | ScraperAPI |
| --- | --- | --- |
| Free tier | 100 credits, 1 concurrency, no card | 1,000 credits, 5 concurrency |
| Trial | — | 7 days, 5,000 credits, no card |
| Cheapest paid plan | $40/mo — 200,000 credits, 5 concurrency | $49/mo — 100,000 credits, 20 concurrency |
| Annual discount | ~2 months free (conditions not detailed) | 10% off every plan |
| Structured data endpoints | 60+ dedicated scrapers (per SDK listing) | Amazon, Google, Walmart endpoints returning JSON/CSV |
| Over-limit behavior | Over-limit response until billing reset | Pause by default; auto-upgrade or pay-as-you-go |

**Scrapingdog makes sense if** you want the lowest possible paid entry ($40/month), you need one of its platform-specific scrapers, or you're wiring scraping into AI-agent workflows and want the MCP server. Its 100-credit free tier is thin, but enough to check whether its endpoints return the data shape you need. Annual billing saves roughly two months if the discount applies to your plan.

**ScraperAPI makes sense if** you want a longer evaluation window — 5,000 credits over 7 days versus 100 — more concurrency per dollar at the low end (Hobby's 20 threads against Scrapingdog Lite's 5), and per-domain cost documentation precise enough to model your spend before committing. Its structured data endpoints for Amazon, Google, and Walmart return parsed JSON or CSV without you writing a parser, which can matter more than the credit math if frontend time is your bottleneck. 👉 [Compare the plans and start with the free trial](https://www.scraperapi.com/?fp_ref=coupons)

One thing to keep in perspective: Scrapingdog's Lite plan is cheaper in absolute terms, but a $40 plan with 5 concurrent connections will strangle any project running more than a handful of parallel workers. Compare concurrency alongside price, or the "cheaper" plan ends up costing you in wall-clock time.

## FAQ

**Is there a free version of Scrapingdog?** Yes. Every account starts with 100 free credits and full access to all APIs, no credit card required, per the pricing FAQ.

**Does either service charge for failed requests?** No. Scrapingdog automatically credits back failed, blocked, and timed-out requests. ScraperAPI only bills responses with 200 or 404 status codes and requests you cancel before the 70-second timeout.

**How many credits does scraping Google cost?** On ScraperAPI, 25 credits per request, including all Google subdomains; LinkedIn costs 30, Amazon-type e-commerce sites cost 5, and a standard page costs 1. Scrapingdog's per-API costs are listed in its documentation and vary by endpoint.

**Can I change plans later?** On both, yes. ScraperAPI upgrades happen anytime from the billing page, and auto-upgrade is opt-in. Scrapingdog upgrades and downgrades are allowed anytime, though neither is prorated — you pay the full new-plan amount, and unused credits roll over on upgrades but reset on downgrades.

## Before you commit to a plan

Run your actual target URLs through a cost estimator first — ScraperAPI's `urlcost` endpoint works the moment you have an API key, and it accounts for rendering and bypass parameters. Then use the trial on your real project, not on a test page; an API that behaves perfectly on example.com can still stumble on the site you actually care about.

If you're pulling a few hundred thousand requests a month with a mix of standard pages and Google queries, ScraperAPI's Hobby or Startup tier with annual billing lands around $44–$134/month with enough concurrency to keep workers busy. If you need the cheapest possible paid tier or a specific platform scraper Scrapingdog offers, its $40 Lite plan is the honest pick — just budget for the concurrency cap. And if neither fits, remember that both publish custom enterprise options, so an odd volume doesn't have to force you into an oversized tier. 👉 [Start ScraperAPI's free 7-day trial and test it on your own targets](https://www.scraperapi.com/?fp_ref=coupons)
