# amazon proxies: Choosing the Right IP Type for Buy Box Tracking, Review Scraping, and Seller Account Isolation

Most guides to Amazon proxies spend a thousand words explaining that Amazon has anti-bot systems, then hand you a list of ten providers and no way to choose between them. The actual problem is narrower. You have a job — a price sweep, a review crawl, three seller accounts in the same region — and it either survives contact with Amazon's rate limits or it doesn't. What decides that is the IP type, how long each IP lives, and whether you're paying by the address or by the gigabyte.

So here's the practical version: what breaks Amazon jobs, which proxy type fixes which one, what the bandwidth actually costs, and where a budget residential network like 9Proxy fits and where it honestly doesn't.

## Three things that kill an Amazon job

**Rate limiting is per IP, not per account.** Amazon throttles repeated hits from a single address fast — often within a handful of pages. Rotating the exit IP per request is the fix, and it's the reason a "one fast datacenter IP" setup dies in the first minute.

**Prices and the Buy Box are decided per visitor.** Amazon serves different prices, delivery promises and Buy Box winners depending on the marketplace and the delivery address your request appears to come from. A US IP asking for amazon.co.uk gets a location banner, different availability and occasionally a different number. If you want to know what a shopper in Munich actually sees, the request has to leave from Munich — or at least from Germany.

**Datacenter ranges get robot-checked early.** Residential exits carry a real ISP and a real device behind them, which is why a request from a household connection is treated as an ordinary shopper. This is not a marketing distinction; it's the single largest variable in success rate on Amazon.

> Amazon permits one seller account per region unless you can demonstrate genuinely distinct businesses or product lines. Running several accounts from the same IP address is one of the fastest ways to trip its anti-fraud systems.

That last point is why seller-account work and scraping work need different things from the same proxy provider, and people who shop for a single solution usually get one of the two wrong.

## Which IP type does an Amazon job actually need?

| IP type | What it is | Works for | Fails at |
| --- | --- | --- | --- |
| Rotating residential | Real household IPs, new address per request | Catalogue crawls, price and Buy Box sweeps, review collection | Keeping a login alive for months |
| Static residential / ISP | ISP-registered IP hosted on a server line | Seller Central, repricers, daily account work | High-volume crawling (one address throttles) |
| Mobile | 4G/5G carrier IPs | Heaviest protection, low volume | Budget — usually the priciest per GB |
| Datacenter | Cloud-hosted ranges | Cheap internal testing, low-stakes checks | Amazon, at anything resembling scale |

For most Amazon work — price monitoring, Buy Box tracking, product and review collection — rotating residential is the right answer. For seller accounts you want a fixed address that doesn't wander, and that is a different product line.

Worth knowing before you buy anywhere: 9Proxy's public catalogue is residential, in two billing models, plus bundle packages. There's no datacenter tier. If your plan was "cheap datacenter IPs for light Amazon poking", this isn't that vendor — and, honestly, light poking is the one Amazon job where you'll get blocked either way.

## The five Amazon jobs people buy proxies for

### 1. Seller accounts and Seller Central

Two or three accounts in the same marketplace need two or three addresses that never touch each other. The requirement here is boredom: the same IP, every day, for months. A rotating pool is actively the wrong tool, because a login that appears to move between countries on Tuesday afternoon is exactly what Amazon's security systems flag.

### 2. Buy Box and price monitoring

The Buy Box is decided per marketplace and per visitor, so monitoring it means requesting the product page from an IP in that marketplace's country, often several times a day, across hundreds or thousands of ASINs. Each of those requests can leave from a different residential IP. This is the highest-volume, lowest-value-per-request job on the list, which makes billing model matter more than anything else.

### 3. Product, review and search data collection

Product research needs more than prices: titles, bullet points, variations, review counts, star distributions and the order results appear in for a keyword. All of it varies by marketplace. Search result pages and review pages are heavier than a single product page, and paginating through reviews of one product is the one place where a short sticky session (a few minutes on the same identity) beats rotating every request.

### 4. Ad and listing verification by region

Sponsored Products and Sponsored Brands placements are only visible to the audience they target. Verifying that a campaign shows where it should, next to which competitors, means loading the results page as that audience — from the campaign's country and city. A datacenter IP usually sees no ads or a different set. The same trick covers listing hygiene: unauthorised sellers, MAP breaches, hijacked listings, stale images.

### 5. Brand protection and delivery-promise checks

Delivery estimates, Prime eligibility and price ladders differ store to store across the EU. Zip or postal-code level targeting is what makes those checks meaningful rather than approximate.

## Sticky or rotating: the setting that decides most of these jobs

Rule of thumb that holds up in practice:

- **Catalogue crawls, price sweeps, category rankings** → rotate per request. Every request is an independent errand.
- **Review pagination, multi-step product flows** → sticky for a few minutes, long enough to look like one shopper reading a page.
- **Cart, checkout, account login** → sticky and fixed, and ideally a static IP rather than a rotating pool.

Getting this backwards produces the two most common complaints in Amazon scraping threads: "I get CAPTCHAs on every page" (you're hammering one identity) and "my session drops mid-flow" (you rotated when you shouldn't have).

## The bandwidth math nobody puts in the comparison tables

Proxy vendors' published figures put an Amazon product page at roughly 600 KB of HTML if you skip images, scripts and media, and somewhere near 4 MB when you don't. Fetch HTML only and you cut roughly 85% of the bytes per page.

Do the arithmetic on a real number: 100,000 product pages HTML-only is around **57 GB**. That 57 GB is the entire cost question.

- At a $3.00/GB entry rate, that crawl is not going to happen.
- At $1.50/GB it's about $85.
- At $1.00/GB it's roughly $57.

Now compare it to a provider that charges per IP with unmetered traffic. 9Proxy's IP-based packages start at $24 for 100 IPs and $72 for 500 IPs, and bandwidth is not counted at all — you scrape 100 pages or 10,000 through one IP and the price doesn't move. If your Amazon workload is data-heavy and unpredictable (4 MB product pages because you need the rendered version, image catalogues, video metadata), that's a structurally different deal from paying per gigabyte.

The catch, and it's a real one: on 9Proxy's IP-based model each IP works for a few hours up to about 24 hours, and one IP equals one usage once forwarded. So 500 IPs is a rotating supply of addresses you draw down over a campaign, not 500 permanent ones. For a crawl that runs continuously, you size the package by how many addresses you'll burn through per week, not by peak concurrency.

## Where 9Proxy sits in this picture

9Proxy is a residential-only network: 20M+ residential IPs across 90+ countries, HTTP/HTTPS and SOCKS5, with targeting down to country, state, city, ZIP and ISP. Two product models, and the difference between them matters more than the branding:

- **Residential by IPs** — pay per address, unmetered traffic per IP, unused IPs never expire. Each IP lives from a few hours up to ~24h. Rotation is available through an Auto Rotation Proxy that switches addresses at intervals you set on selected ports. Access runs through the desktop app (local port forwarding), or via Proxy2Web from the dashboard if you don't want to install anything.
- **Residential by GB** — pay per gigabyte, generate unlimited endpoints, 180-day validity (unlimited on Enterprise), rotating or sticky sessions, authentication by username/password or IP whitelist, entirely dashboard-based. Bundles combine both: 100 IPs + 5 GB for $30, 1,500 IPs + 50 GB for $180, 5,000 IPs + 500 GB for $720.

One editorial note on the pricing you'll find elsewhere: 9Proxy raised prices on its IP-based and bundle packages on 1 June 2026 and left GB-based pricing untouched. Older reviews still quote $0.015/IP and $20 for 100 IPs. Those numbers are stale. The tables below use the current published rates.

On performance, third-party testing rather than vendor claims is worth more. Geekflare ran 300 sequential requests through 9Proxy's rotating residential IPs against a major e-commerce site sitting behind Cloudflare's bot protection — the same class of defence that stalls datacenter proxies immediately. 293 passed (97.7%), 5 hit CAPTCHAs, 2 hard-blocked, average response 0.63 seconds. The same pattern through a datacenter pool blocked 34% of requests on the first pass. Both the CAPTCHA cluster and the two blocks came from specific IP ranges and cleared when the test rotated away from them.

That's a fair picture of what budget residential gets you: high success on standard and moderately protected targets, a small tail of bad exits to rotate past. Where it gets thinner is the heavily defended end of the market — high-frequency Amazon SERP work, Google, LinkedIn at volume. For Amazon *product pages* at moderate frequency, residential from real ISPs is the correct tool. For a SERP API that handles CAPTCHAs for you, it isn't the same product.

## The full 9Proxy plan list and current prices

Everything 9Proxy sells publicly, in one place. All prices are as published on its pricing page after the June 2026 adjustment.

| Type | Plan | What you get | Price | Billing & validity | Buy |
| --- | --- | --- | --- | --- | --- |
| By IP | 100 IPs | Unmetered traffic per IP, unused IPs don't expire | $24 ($0.24/IP) | One-off balance | Get the 100 IP pack |
| By IP | 500 IPs | Same, wider rotating supply | $72 ($0.144/IP) | One-off balance | See this plan |
| By IP | 1,000 IPs + 500 bonus | 1,500 addresses total | $126 ($0.084/IP) | One-off balance | Check this plan |
| By IP | 2,500 IPs | Mid-size monthly sweeps | $210 ($0.084/IP) | One-off balance | Get this plan |
| By IP | 5,000 IPs | Agency-scale rotation | $360 ($0.072/IP) | One-off balance | See pricing |
| By IP | 15,000 IPs | Multi-region operations | $720 ($0.048/IP) | One-off balance | Get this plan |
| By IP | 25,000 IPs | Heavy automation | $863 ($0.035/IP) | One-off balance | See pricing |
| By IP | 50,000 IPs | Reseller-scale | $1,438 ($0.029/IP) | One-off balance | Get this plan |
| Business IP | 100,000 IPs | Volume tier | $2,300 ($0.023/IP) | One-off balance | Check this tier |
| Business IP | 200,000 IPs | Volume tier | $4,140 ($0.021/IP) | One-off balance | Check this tier |
| Business IP | 500,000 IPs | Lowest per-IP rate | $8,625 ($0.018/IP) | One-off balance | Check this tier |
| By GB | 5 GB | Unlimited endpoints, sticky or rotating | $15 ($3.00/GB) | 180 days | Start with 5 GB |
| By GB | 50 GB + 5 GB bonus | 55 GB usable | $105 ($2.10/GB listed) | 180 days | Get the popular pack |
| By GB | 100 GB | Regular automation | $150 ($1.50/GB) | 180 days | See this plan |
| By GB | 200 GB | Medium monitoring jobs | $200 ($1.00/GB) | 180 days | Get this plan |
| By GB | 1,000 GB | Daily monitoring at scale | $800 ($0.80/GB) | 180 days | See pricing |
| By GB | 2,000 GB | Multiple tools and regions | $1,500 ($0.75/GB) | 180 days | Get this plan |
| Enterprise GB | 3,000 GB | Unlimited validity, team mode (1 owner + 5 members), per-member traffic controls, activity logs, VIP support | $2,160 ($0.72/GB) | No expiry | See Enterprise |
| Enterprise GB | 6,000 GB | Same terms, larger balance | $4,200 ($0.70/GB) | No expiry | See Enterprise |
| Enterprise GB | 10,000 GB | Lowest per-GB rate | $6,800 ($0.68/GB) | No expiry | See Enterprise |
| Bundle | Starter: 100 IPs + 5 GB | Both models in one balance | $30 | 180-day traffic validity | Get the starter bundle |
| Bundle | Popular: 1,500 IPs + 50 GB | Mixed workloads | $180 | 180-day traffic validity | Get the popular bundle |
| Bundle | Pro: 5,000 IPs + 500 GB | One all-in pack | $720 | 180-day traffic validity | Get the pro bundle |

## Which plan suits which Amazon job

**Price and Buy Box sweeps on a tight budget.** 100 IPs at $24 with unmetered traffic covers a small ASIN list checked a few times a day without a bandwidth meter running in the background. If your pages are heavy rendered versions rather than HTML-only, this is where per-IP billing starts paying for itself.

**Continuous catalogue crawling.** Either 1,000+500 IPs at $126 or a GB pack, depending on how much of the page you actually download. Run the 600 KB versus 4 MB arithmetic on your own page count first — that single decision is worth more than the per-plan comparisons.

**Multi-account seller work.** Nothing in 9Proxy's rotating residential line is designed to hold a single address for months. The IP-based packages let you control rotation, but each address still ages out within about a day. If you need permanent per-account addresses, that is a static ISP product and you should buy one.

**Agency work with several clients.** The Popular bundle at $180 is the awkward middle that often fits: enough IPs to keep client workloads separated, enough traffic that you're not rationing requests.

**Ongoing infrastructure.** The Enterprise GB tiers are the only plans with unlimited validity and shared team balances — worth it if 180 days is a deadline you'd otherwise lose money to.

## Setup notes that stop you wasting requests

1. Set the marketplace country in the proxy username before anything else. Half of "Amazon is blocking me" reports are requests hitting the wrong storefront.
2. Fetch HTML only. It removes roughly 85% of the bytes per page and most of what's slow.
3. Keep a fixed number of workers per marketplace and add a short delay. Ten threads against one ASIN is a block waiting to happen.
4. Rotate per request for catalogue work; switch to a few-minute sticky session only when you're walking review pages of one product.
5. Clear cookies between identities and disable images and media in the headless browser.
6. Rotate away from a CAPTCHA rather than retrying through it. The IP is the problem, not the request.
7. Track success rate per IP range, not just overall. Bad exits cluster, and finding the cluster is how you fix it.

## FAQ

**Do I need residential proxies for Amazon?**
For anything beyond a handful of pages, yes. Amazon throttles repeated requests from one address quickly, and datacenter ranges are robot-checked earlier than household IPs.

**How much bandwidth does an Amazon crawl use?**
Around 600 KB per page HTML-only and roughly 4 MB with images and scripts. 100,000 HTML-only pages comes to roughly 57 GB.

**Can I run multiple Amazon seller accounts through one proxy provider?**
You can isolate each account on its own address, but the addresses need to be stable and stay in one country. Rotating pools are the wrong tool for logins — and Amazon's one-account-per-region rule still applies.

**What's the cheapest way to test this before committing?**
Buy the smallest package that matches your model: 5 GB ($15) if your workload is light and bursty, 100 IPs ($24) if pages are heavy. 9Proxy has also run limited trial allocations for new users from time to time, subject to availability — worth asking support directly rather than assuming.

**Which 9Proxy model should an Amazon scraper pick?**
If pages are heavy or your volume swings, per-IP with unmetered traffic. If you rotate aggressively and each request is a small HTML fetch, pay per GB and skip the IP bookkeeping.

Start with the model, not the discount. Whichever fits your Amazon workload — unmetered per IP or metered per gigabyte — 👉 [check 9Proxy's current residential plans and pricing](https://bit.ly/9-Proxy) and size it against your actual page count before you pay.
