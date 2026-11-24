# Cheap Sydney VPS: How Much It Really Costs, Which Plan Fits a WordPress Site or a Docker Stack, and What the $3/Month Ads Leave Out

A Sydney VPS that holds up in production costs roughly **$5 to $6 a month on monthly billing**. The $3 headline you keep seeing is almost always an annual-plan rate, and the plan behind it is usually 1 GB of RAM with no backup and no DDoS filtering.

Evoxt's Sydney location starts at **$2.99/month for a 512 MB tier** and **$5.99/month for 1 vCore and 2 GB**, priced in USD and billed monthly. Every VM in the lineup ships with a weekly offsite backup at no extra cost, which is rare below $10 and changes what you have to build yourself. DDoS protection is the thing it doesn't include, and that decides where your DNS should point.

What follows is Evoxt's full price list for the Sydney region, three pricing mechanics that decide whether "cheap" survives month two, measured Sydney throughput, and a workload-by-workload rule for choosing a plan.

> **The default pick: Evoxt VM-1 at $5.99/month.** 1 vCore, 2 GB RAM, 20 GB storage, 1 Gbps port, weekly offsite backup included, no bandwidth billing. Enough for one WordPress site with MySQL, a small API, or a WireGuard endpoint for a handful of people. If you run more than two containers plus a database, move up to VM-2.
> 👉 [Deploy VM-1 on Evoxt's Sydney node](https://bit.ly/EvoXt)

## Evoxt Sydney plans and prices

| Plan | vCPU | RAM | Storage | Price (USD/month) | Order |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 | 512 MB | 5 GB | $2.99 | [Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 | 1 GB | 10 GB | $4.99 | [Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 | 2 GB | 20 GB | $5.99 | [Deploy VM-1](https://bit.ly/EvoXt) |
| VM-2 | 2 | 4 GB | 30 GB | $11.99 | [Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 | 4 GB | 30 GB | $14.99 | [Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 | 8 GB | 60 GB | $23.99 | [Deploy VM-4](https://bit.ly/EvoXt) |
| VM-8 | 8 | 16 GB | 80 GB | $47.99 | [Deploy VM-8](https://bit.ly/EvoXt) |

Prices are USD, billed monthly; Evoxt does not offer hourly billing, so the smallest test commitment is one month. VM-1 through VM-8 are the tiers VPSBenchmarks still tracks at these exact prices in its Evoxt plan list.

Three details sit outside the price column and matter more than the RAM figure:

- **Every plan runs a 1 Gbps port**, including the $2.99 tier.
- **Bandwidth is allowance-then-throttle.** VPSBenchmarks records a 2 TB monthly allowance for the 2-core/4 GB instance and notes the provider "does not charge for bandwidth" — traffic past the allowance is throttled, not invoiced. A slow site beats a surprise bill.
- **Weekly offsite backup is included on all VMs**, restore-on-demand, no add-on purchase.

VPSBenchmarks' feature record also lists DDoS protection as **not** included, IPv6 as supported, a control-panel firewall, an admin API at `api.evoxt.com`, and payment by card, PayPal or Bitcoin. One benchmark trial had a server accepting connections about 2 minutes 20 seconds after ordering. The company has operated since 2020, so its track record is shorter than the incumbents in this price bracket; that's a real caveat, not a dealbreaker.

## Why the $3 cheap Sydney VPS ads don't survive month two

Host4Fun is the most honest example because it prints the mechanics in one sentence: plans "start from $3/month on the annual plan", while monthly billing starts at **$5/month**. That $3 buys 1 vCPU, 1 GB DDR4, 15 GB NVMe and a 2 TB transfer allowance, and it requires twelve months paid up front at a stated 40% annual discount. Committing $36 to a provider you haven't tested is a fine trade for a known host and a poor first order. The same page prices its Nova plan at $12.80/month on annual billing.

OVHcloud shows the second mechanic. The header advertises "Up to 3 Gbps unmetered bandwidth." The footnote says Asia-Pacific VPS locations (Mumbai, Singapore, Sydney) carry a monthly quota: **500 GB on VPS-1, 1 TB on VPS-2 and VPS-3, 3 TB on VPS-4**, after which "the bandwidth is capped at 10 Mbps." Ten megabits is about 1.25 MB/s. Fine for a text site with modest traffic, useless for a download endpoint or anything video. To its credit, OVHcloud VPS-1 at $4.54 includes daily backup of the previous 24 hours and Anti-DDoS on every tier, coverage most sub-$5 plans skip.

The third mechanic is the one that makes cross-brand tables lie. OVHcloud VPS-1 gives 2 vCores, 4 GB RAM and 40 GB NVMe for $4.54. EDIS Global's KVM Basic Plus gives 2 vCPU, 4 GB RAM and 45 GB SSD for €21.99. Nearly five times apart for what looks like the same box. The difference lives in the surroundings: EDIS bundles 2 TB of traffic on a dual 1 Gbps uplink plus a 100 GB starter traffic credit, and assigns backups and security to the customer in writing. OVHcloud caps transfer at 500 GB and includes the backup. Neither is wrong; comparing only the RAM line is.

Currencies don't merge either. Evoxt and OVHcloud quote USD. EDIS quotes EUR. Nothing in these pages gives an exchange rate, so a single "cheapest" number across all of them would be invented.

## Sydney latency, from measured tests rather than marketing pages

Two facilities carry most of the cheap Sydney VPS market: **Equinix SY1 in Mascot**, used by EDIS Global and is*hosting, and **Equinix SY3 in Alexandria**, used by ExtraVM. Same metro, different carrier mixes. Both sit close enough to the Sydney IX peering fabric that the facility name matters less than who the provider peers with.

EDIS published Speedtest CLI results taken from its Sydney host platform on 21 September 2026:

| Target | Download | Upload | Idle ping | Loss |
| --- | --- | --- | --- | --- |
| Aussie Broadband, Sydney | 4,672.67 Mbps | 4,266.92 Mbps | 12.91 ms | 0% |
| Telstra, Sydney | 6,632.12 Mbps | 9,195.55 Mbps | 1.19 ms | 0% |
| Spintel, Sydney | 2,993.27 Mbps | 5,158.77 Mbps | 0.69 ms | not reported |

Those are host-to-Speedtest-server figures, and EDIS says plainly that they don't guarantee throughput or latency for an individual VPS. Read them as a ceiling for a well-peered Sydney box, not as your number.

Realistic round trips from a Sydney node: **5–30 ms across Australia, 20–40 ms to New Zealand, 100–130 ms to Singapore, 150–170 ms to the US west coast**. If your audience is in Sydney, Melbourne, Brisbane or Auckland, hosting in Sydney removes more than 100 ms compared with a Singapore node. For a checkout flow or a login page, that's the difference between responsive and laggy.

👉 [Compare Evoxt's Sydney plans and live pricing](https://bit.ly/EvoXt)

## Which Evoxt plan fits your workload

**Static site behind a CDN, or a VPN endpoint for two or three people.** VM-0.5 at $2.99 covers it, and 512 MB is genuinely enough because nothing dynamic is running. The 5 GB disk is the real constraint; a photo-heavy static build will fill it. If you want headroom for logs and a Docker daemon, VM-0.75 at $4.99 doubles both RAM and disk for two dollars.

**One WordPress site with MySQL and a normal plugin load.** VM-1 at $5.99 is the floor. PHP-FPM plus MySQL plus a control panel eats 1 GB before the first traffic spike, and the memory pressure shows up as slow admin pages and failed cron runs rather than an obvious crash.

**Two or three sites, a staging copy of production, or a small Docker Compose stack with Postgres and Redis.** VM-2 at $11.99 doubles RAM and cores. If your bottleneck is threads rather than memory — image resizing, scraping, scheduled compile jobs, a small game server — VM-3 at $14.99 keeps 4 GB and gives you 4 vCores for $3 more. That $3 is the best value jump in the lineup for CPU-bound work and wasted money for a database that wants RAM.

**Five or more services in Compose, a small Elasticsearch node, or a single-node Kubernetes cluster.** VM-4 at $23.99 with 8 GB and 60 GB. Below 8 GB those workloads spend their time in swap.

**Windows Server or MetaTrader 4/5.** Windows images are on Evoxt's OS list with RDP access. Budget 4 GB rather than the 2 GB minimum, so VM-2 or VM-4. Host4Fun bundles a free 180-day evaluation licence with its Windows plans, which is worth knowing if you need a licensed Windows box on a small budget. ExtraVM's Sydney page contradicts itself on Windows availability, so don't plan around it there.

## Six things to confirm before you pay

**Backup terms.** is\*hosting includes free weekly backups, retains 4–5 copies on remote servers, and sells a daily option with 30-day retention. OVHcloud includes daily backup of the previous 24 hours on every VPS. EDIS Global puts backups, security and software configuration on the customer. Evoxt includes weekly offsite backup on all VMs. A provider with no backup means you're configuring `restic` or `borg` in week one.

**DDoS coverage and its ceiling.** ExtraVM states that Sydney "does not come with native network DDoS protection" and offers only local filtering under 10 Gbps via eBPF/XDP, pointing enterprise-grade protection to its Singapore or Tokyo locations. VPSBenchmarks lists DDoS protection as absent for Evoxt. Host4Fun advertises network-level protection on all plans. If you're a plausible target, put a CDN with L3/L4 scrubbing in front regardless of provider, and keep the origin IP off public DNS history.

**Behaviour past the traffic allowance.** OVHcloud throttles to 10 Mbps. Evoxt throttles instead of billing. Neither suspends you, which is the outcome you want.

**Resize cost and whether it needs downtime.** EDIS charges €10/month per additional vCPU and €5/month per extra IPv4, and RAM, vCPU or storage changes require a full shutdown and restart. After a storage upgrade you expand the partition and filesystem yourself. Ask the same question of any host before you buy, because a resize that requires a reboot in business hours is a different product.

**Payment rails.** Evoxt accepts cards, PayPal and Bitcoin. Host4Fun takes 50+ cryptocurrencies including USDT on TRC-20, ERC-20 and BEP-20. EDIS takes Monero, Litecoin and USDT. If crypto is a requirement rather than a preference, confirm before you sign up.

**Exit cost.** ExtraVM's refund window is 5 days and applies to fiat payments only. Evoxt bills monthly with no hourly option, so the cheapest way to test it is a single month, not a year.

## Before you click deploy

One small site, one database, backup included, no traffic billing: **VM-1 at $5.99**. More services or a staging copy: **VM-2 at $11.99**. CPU-bound work at 4 GB: **VM-3 at $14.99**. Windows or 8 GB of RAM: **VM-4 at $23.99**. Absolute lowest monthly figure with no expectation of support: **VM-0.5 at $2.99**, accepting 512 MB and 5 GB of disk.

Two last checks. Bring your own DDoS layer, since none is included. And take a manual snapshot or run your own backup job in the first week even where weekly offsite backup is bundled; a seven-day recovery window is long when the site is down on a Tuesday.

👉 [Pick your Evoxt Sydney plan and check the current monthly price](https://bit.ly/EvoXt)
