# geo targeted proxies: country, city, ZIP and ISP targeting explained, and what each tier actually costs

Most people searching for geo targeted proxies aren't confused about what a proxy is. They already tried one. The problem is that it came out of the wrong place.

You bought a proxy, checked the exit IP, and it said "United States." Then you tried to load a page that only shows up for someone in Ohio, or you needed a ZIP-level location for a local ad test, or you needed a household connection from a specific ISP so the fingerprint matched, and the whole thing fell apart. Or it worked, but you burned through a gigabyte quota in an afternoon while paying per GB.

That's the real fork in the road: two separate decisions that get bundled into one purchase.

1. **How precise is the targeting?** Country is easy. City, ZIP, and ISP are where most cheap pools quietly give up.
2. **How are you billed?** Per IP with unlimited traffic, or per GB with rotation across the whole pool. Same network, very different economics for the same job.

This article covers both, using 9Proxy as the concrete example — a residential network with 20M+ IPs across 90+ countries that sells targeting down to country, state, city, ZIP and ISP level, and that prices the two billing models separately rather than forcing you into one.

## What "geo targeting" actually covers

The phrase gets used loosely, so it helps to separate the levels. Not every provider supports all of them, and the ones they do support often behave differently.

**Country.** The baseline. Nearly every residential provider does this. Narrowing to one country is also the fastest option, because the pool is largest.

**State / region.** Available on many but not all providers, and usually only for countries where the provider's inventory is dense — the US and Australia are the common examples. Useful for jurisdiction-specific rules, state-level pricing, or regional ad campaigns.

**City.** This is where targeting stops being decoration. Local search results, restaurant delivery availability, city-level ride-hailing pricing, local inventory checks — none of these work with a country-level IP.

**ZIP / postal code.** The precision tier. Fewer IPs available, so matching is slower and success rates get more variable. Worth it when you genuinely need postal-code-level accuracy for retail or ad verification.

**ISP / ASN.** An underrated one. If the site you're hitting fingerprints the network operator, an IP from a random residential ISP may not match what you're simulating. Filtering by ASN lets you pin the connection to a specific carrier.

There's a tradeoff that doesn't get mentioned often enough: **precision costs you pool size.** Every filter you stack — state plus city plus ISP — shrinks the set of IPs that can serve your request. On a nationwide country target, rotation is fast. On a ZIP-level target in a small town, you may get a handful of usable IPs and slower responses. Providers don't always say this loudly, and it's the reason "why is my highly targeted proxy slow" is such a common support ticket.

## Rotating, sticky, and why the distinction decides everything

Before pricing, decide what kind of session your job needs. This matters more than which provider you pick.

**Rotating** gives you a fresh IP on every request. Good for scraping product listings, checking SERP rankings across many locations, monitoring prices, or polling an API. You don't care which specific IP you exit from, only that it's in the right place.

**Sticky** holds one IP for a defined window. Necessary when you log in somewhere, keep a cart session open, run a multi-step form, or manage an account that would look suspicious if its IP changed mid-session.

A provider that only does one of these is only half a tool. On 9Proxy, sticky sessions are set by a duration parameter in the proxy username, and you can run several parallel sticky IPs from one configuration by assigning different session IDs — which is what you need if you're managing multiple accounts from the same city at the same time.

## How targeting is actually configured

This is the part worth reading the documentation for, because the whole thing lives in the proxy username. 9Proxy uses a structured username rather than a dashboard dropdown, which means you can drop the same logic into a curl command, a browser automation script, or a scraping framework without clicking through a UI first.

The general shape is:


<sub-user>-country-<country_code>-st-<state_code>-city-<city_name>-isp-<isp_code>-sst-<session_time>-ssid-<session_id>


In practice, that produces usernames like:


subaccount-country-us                          # rotating US IP
subaccount-country-us-city-newyork             # rotating IP from NYC
subaccount-country-vn-city-hanoi-sst-20        # Hanoi IP held for 20 minutes
subaccount-country-us-sst-15-ssid-device1      # sticky session, custom ID


A few things that save time later:

- Cities with spaces use underscores (`city-newyork`, and `city-sanfrancisco` style formatting).
- `sst` is the sticky duration in minutes. Leave it out for rotation.
- `ssid` isn't required, but without it your parallel sessions collapse into one. If you're running five devices through the same city, give each its own `ssid`.
- **Don't over-filter.** Country-only targeting is the fastest. Stacking state, city and ISP narrows the available pool and can hurt both speed and success rate. Add filters because your task requires them, not because more precision sounds better.

For the IP-based model, targeting works differently — through a desktop app on Windows, macOS or Linux where you filter by country, state, city, ZIP or ISP and forward chosen proxies to specific local ports. That's a different workflow: you're binding an IP to a port rather than generating endpoints on the fly.

## Where geo-targeted proxies actually earn their money

The use cases are narrower than the marketing implies, but the ones that matter are genuinely hard to do any other way.

**Ad verification.** Your campaign is supposed to show in Chicago, not Rockford. Checking that requires a Chicago IP and a clean one, because ad networks serve differently to traffic they've flagged. This is probably the single most defensible use of city and ZIP-level targeting.

**Localized SERP and rank tracking.** Rankings change by location. A country-level IP tells you roughly what a national average looks like; a city-level IP tells you what a customer in that city sees.

**Retail price and availability monitoring.** Same product, different price, different stock status. Often only visible from inside the target region, and sometimes only at postal-code precision.

**Market research and compliance checks.** Comparing what a site publishes in one jurisdiction versus another — pricing disclosures, regional offers, availability restrictions.

**Multi-account and profile management.** Each identity needs a stable residential IP that matches its supposed location. This is where the sticky sessions and the sub-account structure matter: you want each profile pinned to a consistent city, not sliding around.

**Accessing region-locked content.** Worth setting expectations. Residential IPs handle geo-restrictions on most ordinary sites, but major streaming platforms run their own detection layers. A third-party review of 9Proxy noted it works well against retail site restrictions while still running into detection on services like Netflix. That's a fair description of residential proxies generally — region-blocking on a shopping site and region-blocking on a streaming platform are not the same problem.

## 9Proxy pricing: the full picture

9Proxy bills through a balance-based system, and the packages split into four families. Two notes before the numbers: IP-based and bundle pricing was adjusted upward on June 1, 2026 (the company's first price change since launch), while **GB-based pricing was left unchanged**. The figures below reflect the post-adjustment list prices.

### IP-based packages (unlimited bandwidth per IP)

You buy a fixed number of residential IPs. Traffic isn't metered, and unused IPs don't expire.

| Package | Effective price per IP | Total | Best suited to |
| --- | --- | --- | --- |
| 100 IPs | $0.24 | $24 | Testing the network, one-off jobs |
| 500 IPs | $0.144 | $72 | Solo operators, light scraping |
| 1,000 IPs + 500 bonus | $0.084 | $126 | Small teams, steady workloads |
| 2,500 IPs | $0.084 | $210 | Several verticals running at once |
| 5,000 IPs | $0.072 | $360 | Agencies, mid-scale SEO and price monitoring |
| 15,000 IPs | $0.048 | $720 | Businesses with regional teams |
| 25,000 IPs | $0.035 | $863 | Resellers, heavy automation |
| 50,000 IPs | $0.029 | $1,438 | High-volume reselling |
| 100,000 IPs | $0.023 | $2,300 | Industrial-scale operations |
| 200,000 IPs | $0.021 | $4,140 | Industrial-scale operations |
| 500,000 IPs | $0.018 | $8,625 | Platform-level operations |

👉 [Check current IP package pricing](https://bit.ly/9-Proxy)

One caveat specific to this model: IP-based residential IPs naturally stay alive anywhere from a few hours to about 24 hours. That's the nature of residential inventory, not a defect. It matters if you're planning long-lived account sessions — you'll want the per-IP replacement policy and the 24-hour reuse list, both covered below.

### GB-based packages (pay for traffic, unlimited endpoints)

You pay for bandwidth and generate as many proxy endpoints as you want. This is the model to pick when your targeting needs to rotate across a large pool, or when each request is small but you need geographic variety.

| Package | Price per GB | Total | Validity |
| --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days |
| 50 GB + 5 bonus | $2.10 | $105 | 180 days |
| 100 GB | $1.50 | $150 | 180 days |
| 200 GB | $1.00 | $200 | 180 days |
| 1,000 GB | $0.80 | $800 | 180 days |
| 2,000 GB | $0.75 | $1,500 | 180 days |

👉 [See the GB packages](https://bit.ly/9-Proxy)

That 180-day window is more useful than it sounds. If your geo-targeted work is project-based — a campaign that runs for three weeks, then nothing for a month — you're not racing a monthly clock to burn through the balance.

### Enterprise GB packages (no expiry)

Same bandwidth model, with the validity limit removed and team features attached.

| Package | Price per GB | Total | Validity |
| --- | --- | --- | --- |
| 3,000 GB | $0.72 | $2,160 | Unlimited |
| 6,000 GB | $0.70 | $4,200 | Unlimited |
| 10,000 GB | $0.68 | $6,800 | Unlimited |

Enterprise also adds a team mode covering one owner plus up to five members, per-member traffic controls, full activity logs, unlimited share code creation, and unlimited validity on bandwidth shared inside the team. If you're an agency distributing geo-targeted IPs across clients, that structure is the reason to look at this tier rather than buying multiple separate GB plans.

👉 [Compare Enterprise pricing](https://bit.ly/9-Proxy)

### Bundle packages (IPs plus bandwidth)

For workloads that need both stable IPs and metered rotation. Bundled traffic is valid for 180 days.

| Bundle | Package | Total |
| --- | --- | --- |
| Starter | 100 IPs + 5 GB | $30 |
| Popular | 1,500 IPs + 50 GB | $180 |
| Pro | 5,000 IPs + 500 GB | $720 |

👉 [View the bundle options](https://bit.ly/9-Proxy)

## Which one fits your targeting job

Rules of thumb, based on the numbers above and how the two models behave:

**You need sticky city-level IPs for account sessions.** Go IP-based. Unlimited bandwidth means a long session costs you nothing extra, and the account stays pinned to one location. The $0.084/IP tier at 1,000+500 IPs is the most commonly flagged package on the platform, and the price curve makes it easy to see why — that's the point where per-IP cost drops sharply without committing to tens of thousands of IPs.

**You need to check 40 cities once a week.** Go GB-based. You'll rotate across the whole pool, use very little data per request, and paying per IP for IPs you touch once a week is waste. The 50 GB tier at $2.10/GB is the sane starting point; it leaves room to experiment with targeting levels without a big commitment.

**You're an agency with both patterns running.** Either the Popular bundle (1,500 IPs + 50 GB) or Enterprise, depending on whether you need the team structure and unlimited validity. If multiple people need to share the same traffic pool across clients, the bundle math stops making sense and Enterprise usually does.

**You're testing whether targeting actually solves your problem.** Start at 100 IPs for $24 or 5 GB for $15. Both are cheap enough to answer the question "does a location-correct residential IP get me what I need?" before you commit to a larger balance. 9Proxy also runs limited free trials depending on availability, though you have to request them.

## Limitations worth knowing before you buy

**Precision reduces speed.** Covered above, but it's the number one thing people get wrong. City and ZIP targeting narrow the pool. If your workflow is high-volume and location needs are broad, target by country and save yourself the headache.

**The IP-based model requires a desktop app.** Windows, macOS and Linux are supported, so it's not a blocker for most people, but it's a different setup than the browser-extension-plus-username model. The GB-based model runs entirely from the dashboard with username/password or IP whitelisting — no app needed. If you're running on cloud infrastructure, that difference matters.

**Residential IP lifespans are variable.** Hours to about 24 hours on the IP-based side. Third-party reviews describe a policy where an IP that fails within the first 60 seconds of activation gets replaced or credited, and a "Today List" lets you reuse any IP from the last 24 hours at no additional cost. Both help, but neither turns residential inventory into static ISP connections. If you need fixed IPs that never change, that's a different product category.

**No datacenter or mobile line as of now.** 9Proxy is a residential-focused network. Coupon and comparison pages list datacenter proxies as coming soon rather than available. If your workflow specifically needs mobile carrier IPs, this isn't the provider for it.

**Third-party ratings are middling-to-positive, not exceptional.** ProxyLook scores it around 3.9 stars and describes it as a budget residential option. A separate published review put aggregated ratings near 9/10. Treat both as directional. The consistent themes across reviews are strong targeting granularity, competitive per-IP pricing, and a smaller pool than the largest competitors — which shows up exactly where you'd expect, in specialized or low-population targeting.

## Answering the questions people actually search

**Does city-level targeting work on mobile networks?** Only if the network supports it. Mobile IPs are identified by carrier, not by city, and geolocation on mobile is inherently fuzzier. City and ZIP targeting is most reliable on residential connections, which is what 9Proxy sells.

**Can I use both country and city at once?** Yes, and that's the normal pattern: country sets the national pool, state/city/ISP narrow it. Just remember that each additional filter shrinks what's available.

**How do I verify the IP is genuinely in the target location?** Check it against an independent geolocation service rather than trusting the provider's own label. This is also how you'd document work for a client. Run the check on the exact username configuration you plan to use, not on a default proxy.

**Why does my ZIP-targeted proxy sometimes return a different ZIP?** Because postal-code-level inventory is small and the match isn't always exact. Adding a city or state filter instead of ZIP alone often gives better and faster results than demanding exact postal precision.

**Can I run several locations at the same time?** Yes — separate sticky session IDs let you hold multiple simultaneous IPs from the same configuration. Different `ssid` values produce different IPs even when the rest of the username is identical.

**Is geo-targeted pricing more expensive than standard?** No. On this platform, filtering by location is a setting inside the package you already bought, not a premium add-on. You pay for IPs or for gigabytes, not for the targeting parameter.

## The short version

If your requirement is country-level access, almost any residential provider will do and you should shop purely on price. If your requirement is city, ZIP or ISP-level — and that's usually why people search for geo targeted proxies in the first place — the deciding factors are pool coverage at that precision level and how you're billed for it.

9Proxy's structure is straightforward: pick per-IP with unlimited bandwidth when you need stable location-pinned sessions, pick per-GB when you need to rotate across many locations cheaply, and take a bundle or Enterprise when you need both. Start at the smallest tier, verify the targeting actually lands where you need it, then scale.

👉 [Open a 9Proxy account and check the current packages](https://bit.ly/9-Proxy)
