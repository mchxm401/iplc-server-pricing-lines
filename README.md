# IPLC dedicated server: how MKCloud's Shanghai–US and Shanghai–Japan lines work, full plan pricing and buying tips

An "IPLC dedicated server" search usually starts the same way: someone is running a real business between mainland China and somewhere else, the public internet route keeps flapping at 8pm, and a colleague mentions that "the专线 people" pay for a private circuit instead. From there the questions get practical very fast. What exactly am I renting? Why does the latency matter more than the bandwidth number? And what does something like this actually cost per month?

This article works through those questions using MKCloud, a China-based provider focused specifically on cross-border private-line servers, as the concrete example. Its current public price pages list six shared-bandwidth plans on the Shanghai–US IPLC route starting at ¥428/month, a dedicated-bandwidth ladder on the same route from ¥800/month, and a Shanghai–Japan IPLC from ¥358/month, all verified from the live store in the past few days. Along the way we'll cover what IPLC actually is, how it differs from CN2 GIA and regular BGP servers, the billing quirks that surprise first-time buyers, and the compliance rules you should read before clicking checkout.

## What "IPLC dedicated server" actually means

IPLC stands for International Private Leased Circuit. It is a point-to-point transmission line rented from carriers, and it runs outside the public internet backbone entirely. Your traffic enters the line on one side and exits on the other without touching the congested international gateways that ordinary VPS traffic has to traverse. In practice that removes the two biggest headaches of cross-border connectivity from mainland China: peak-hour congestion and unpredictable routing detours.

An "IPLC dedicated server" is almost never a bare circuit for consumers. Providers lease circuit capacity in bulk, then carve it into VPS products. You rent a cloud server whose traffic path runs over the private line. MKCloud describes its delivery model precisely in its knowledge base: every VPS gets one independent entry IP and one independent egress IP. You connect to the entry IP, your programs run on the VPS, and outbound traffic automatically leaves through the egress IP.

That one-way design has consequences. The egress IP does not accept inbound connections, which makes these servers a poor fit for public websites, payment callbacks, mail receiving, or game servers. They are built for outbound workflows: syncing inventory to an overseas platform, pulling from foreign APIs, running crawlers and automation that must not drop sessions mid-transfer, reaching admin panels and dev environments that punish unstable IPs.

There's also the question of what "dedicated" refers to. In shared-bandwidth plans, you get a peak bandwidth value (say 200Mbps) that isn't guaranteed around the clock, plus a monthly traffic quota. In dedicated-bandwidth plans, you get a guaranteed rate (say 5Mbps) with unlimited traffic. The server itself is yours either way. Understanding this split before comparing prices will save you from comparing apples to oranges, which is exactly what most cheap IPLC comparisons on the internet get wrong.

## IPLC vs CN2 GIA vs regular BGP: why the latency gap is real

Most people arrive at IPLC after being burned by one of the cheaper alternatives, so a quick comparison helps. A regular BGP VPS rides the default public internet. CN2 GIA is China Telecom's premium optimized public route, better than default BGP but still public infrastructure. IPLC is a physical private circuit, which puts it in a different category altogether.

The latency numbers illustrate the gap. Data published by Hong Kong provider Simcentric puts IPLC at roughly 20–40ms between mainland China and Hong Kong, while CN2 GIA averages 50–70ms on the same corridor. Inside the line, IPLC traffic doesn't traverse the public backbone at all, so the value stays stable through the evening peak instead of degrading exactly when your customers are awake.

The tradeoff is price, and it's steep at the carrier level. Industry analysis of IPLC circuit pricing puts telecom-grade IPLC at around ¥500 per Mbps per month, with private suppliers generally quoting above ¥300. That's why a 200Mbps-peak shared VPS on a private line costs hundreds of yuan per month instead of the $10–20 a commodity VPS commands. You're not paying for the 1-core CPU. You're paying for reserved capacity on a scarce international route.

Two more distinctions matter when reading plan lists. IEPL is IPLC's ethernet-based sibling, functionally similar point-to-point private transport with a different interface standard; MKCloud sells both (its Guangzhou–Hong Kong product is IEPL, the Shanghai routes are IPLC). And "IX" or cloud-interconnect lines are a cheaper hybrid: the cross-border leg is still private, but the entry side runs through a major cloud provider's internal network, which is why those products require an Aliyun, Tencent, or similar cloud server as a front and why their prices start much lower.

## MKCloud's IPLC line-up at a glance

MKCloud (mkcloud.net) is a Chinese provider founded in 2023 that builds its entire catalog around cross-border private lines for e-commerce and business users. The official product overview currently lists seven product groups:

- **Guangzhou–Hong Kong IEPL**, in-circuit latency 1–2ms, shared and dedicated variants, with entry options across Guangzhou BGP, Guangdong Telecom, Mobile, Unicom, and a three-line mix
- **Shenzhen–Hong Kong IX (cloud-interconnect)**, 1–2ms, the cheapest official entry point at ¥158/month, requires a supported cloud server in front
- **Shanghai–Hong Kong IPLC**, 21ms in-circuit, shared and dedicated
- **Shanghai–Hong Kong IX**, same 21ms corridor with cloud-front access
- **Shanghai–Japan IPLC and IX**, 25–28ms, the low-latency favorite for Japan-facing work
- **Shanghai–US IPLC and IX**, 124–134ms in-circuit, the flagship for US-facing operations
- **Fujian–Hong Kong high-defense IPLC** (Xiamen and Quanzhou entries), 1–2ms, dedicated bandwidth with 100Gbps DDoS protection built in

A separate **Shanghai CN2** product (domestic optimization, not an overseas exit) rounds out the catalog. Every cross-border plan ships with dual independent IPv4 addresses, one per side, and all products are delivered as cloud or dedicated servers running your pick of Linux images, from Ubuntu 24.04 and Debian 13 to Rocky, AlmaLinux, Fedora, Alpine, Arch, and CloudLinux 9.

The homepage advertises "from ¥158/month" across the line-up, which is true but worth unpacking: that figure belongs to the Shenzhen–Hong Kong IX entry tier. The Shanghai Telecom IPLC pages start higher, at ¥358/month for Japan and ¥428/month for the US. Per-line starting prices differ by several times, so the table section below matters more than any single headline number.

## Full plan and pricing breakdown

MKCloud's store splits each route into two billing families. Here are the Shanghai–US plans as currently listed, all with Shanghai Telecom entry, US BGP egress, dual IPv4, and 124–134ms in-circuit latency. All prices are in CNY, monthly.

### Shanghai–US IPLC, shared bandwidth (traffic billing)

| Plan | CPU / RAM / Disk | Peak bandwidth | Monthly traffic | Price | Purchase |
| --- | --- | --- | --- | --- | --- |
| 1TB | 1 core / 2GB / 20GB | 200Mbps | 1TB | ¥428/mo | [ Check current price](https://bit.ly/MKCLoud) |
| 2TB | 2 cores / 4GB / 40GB | 300Mbps | 2TB | ¥698/mo | [ Check current price](https://bit.ly/MKCLoud) |
| 4TB | 2 cores / 4GB / 40GB | 300Mbps | 4TB | ¥1258/mo | [ Check current price](https://bit.ly/MKCLoud) |
| 6TB | 4 cores / 8GB / 60GB | 500Mbps | 6TB | ¥1758/mo | [ Check current price](https://bit.ly/MKCLoud) |
| 10TB | 4 cores / 8GB / 60GB | 500Mbps | 10TB | ¥2888/mo | [ Check current price](https://bit.ly/MKCLoud) |
| 20TB | 4 cores / 8GB / 60GB | 1Gbps | 20TB | ¥5666/mo | [ Check current price](https://bit.ly/MKCLoud) |

### Shanghai–US IPLC, dedicated bandwidth (unlimited traffic)

| Plan | CPU / RAM / Disk | Guaranteed bandwidth | Monthly traffic | Price | Purchase |
| --- | --- | --- | --- | --- | --- |
| 5M | 2 cores / 4GB / 40GB | 5Mbps | Unlimited | ¥800/mo | [ Configure this plan](https://bit.ly/MKCLoud) |
| 10M | 2 cores / 4GB / 40GB | 10Mbps | Unlimited | ¥1100/mo | [ Configure this plan](https://bit.ly/MKCLoud) |
| 20M | 2 cores / 4GB / 40GB | 20Mbps | Unlimited | ¥2100/mo | [ Configure this plan](https://bit.ly/MKCLoud) |
| 50M | 4 cores / 8GB / 60GB | 50Mbps | Unlimited | ¥5000/mo | [ Configure this plan](https://bit.ly/MKCLoud) |
| 100M | 4 cores / 8GB / 60GB | 100Mbps | Unlimited | ¥9000/mo | [ Configure this plan](https://bit.ly/MKCLoud) |
| 200M | 4 cores / 8GB / 60GB | 200Mbps | Unlimited | ¥18000/mo | [ Configure this plan](https://bit.ly/MKCLoud) |
| 300M | 4 cores / 8GB / 60GB | 300Mbps | Unlimited | ¥27000/mo | [ Configure this plan](https://bit.ly/MKCLoud) |

The dedicated page also carries a custom-specification row where CPU, RAM, disk, and bandwidth are filled in per quote, for buyers whose requirements don't fit the ladder.

### Shanghai–Japan IPLC, shared bandwidth (25–28ms, Shanghai Telecom entry, Japan BGP egress)

| Plan | CPU / RAM / Disk | Peak bandwidth | Monthly traffic | Price | Purchase |
| --- | --- | --- | --- | --- | --- |
| 1TB | 1 core / 2GB / 20GB | 200Mbps | 1TB | ¥358/mo | [ See the Japan plan list](https://bit.ly/MKCLoud) |
| 2TB | 2 cores / 4GB / 40GB | 300Mbps | 2TB | ¥568/mo | [ See the Japan plan list](https://bit.ly/MKCLoud) |
| 4TB | 2 cores / 4GB / 40GB | 300Mbps | 4TB | ¥998/mo | [ See the Japan plan list](https://bit.ly/MKCLoud) |
| 6TB | 4 cores / 8GB / 60GB | 500Mbps | 6TB | ¥1388/mo | [ See the Japan plan list](https://bit.ly/MKCLoud) |
| 10TB | 4 cores / 8GB / 60GB | 500Mbps | 10TB | ¥2288/mo | [ See the Japan plan list](https://bit.ly/MKCLoud) |
| 20TB | 4 cores / 8GB / 60GB | 1Gbps | 20TB | ¥4500/mo | [ See the Japan plan list](https://bit.ly/MKCLoud) |

### Other lines currently on sale

| Line | Type | In-circuit latency | Entry tier | Purchase |
| --- | --- | --- | --- | --- |
| Guangzhou–Hong Kong IEPL | Shared, traffic billing | 1–2ms | ¥358/mo (1TB) | [ Browse the Guangzhou–HK plans](https://bit.ly/MKCLoud) |
| Guangzhou–Hong Kong IEPL | Dedicated bandwidth, incl. big-bandwidth 200M–2000M tiers with 300Gbps DDoS protection | 1–2ms | On the plan page | [ Browse the Guangzhou–HK plans](https://bit.ly/MKCLoud) |
| Shanghai–Hong Kong IPLC | Shared / dedicated | 21ms | ¥288/mo shared, ¥388/mo dedicated (5Mbps) | [ Check Shanghai–HK pricing](https://bit.ly/MKCLoud) |
| Shenzhen–Hong Kong IX (cloud-interconnect) | Shared, requires supported cloud front | 1–2ms | ¥158/mo | [ Check the IX entry tier](https://bit.ly/MKCLoud) |
| Fujian–Hong Kong high-defense IPLC (Xiamen / Quanzhou) | Dedicated, 100Gbps DDoS protection | 1–2ms | On the plan page | [ View high-defense plans](https://bit.ly/MKCLoud) |

A note on the ¥198 and ¥228 "starting prices" you'll see in third-party roundups on GitHub: those correspond to smaller 100GB/500GB tiers and older price lists, not the current six-plan ladder on the official Shanghai–US page. When the store page and a blog disagree, trust the store page. The same roundups are useful for one thing, though: their latency checks roughly matched the official figures, with Shanghai–Japan landing in the 25–30ms range and Shanghai–US around 124ms.

## Which plan fits which use case

The pricing structure makes more sense once you map it to actual workloads.

For a **US-facing cross-border operation** (Amazon seller workflows, US-hosted SaaS and ERP, APIs that hate session drops), the ¥698 2TB plan is the natural starting point. It doubles the compute and raises peak bandwidth to 300Mbps for a ¥270 step over the entry tier. If your monthly volume is predictable and above 4TB, the ¥1258 plan works out to about ¥0.31 per GB, noticeably cheaper per unit than the 1TB plan's ¥0.43.

For **continuous large transfers** (nightly database syncs, video assets, bulk backups to US storage), stop comparing traffic quotas and look at the dedicated ladder instead. The ¥800 5Mbps plan runs 24/7 at full rate with no counting, which is exactly what a scheduled sync wants. A useful mental checkpoint from the provider's own pricing guide: shared plans count traffic in both directions and pause when the quota runs out, while dedicated plans trade peak speed for guaranteed, unmetered throughput. Neither is "better." They meter different resources.

For **Japan-facing latency work**, the ¥358 Shanghai–Japan entry tier is the sweet spot of the whole catalog. A 25–28ms in-circuit figure approaches LAN-like feel for cross-border standards, and the third-party tests that checked this route found it performing as advertised.

If budget is the binding constraint and your front end already lives on a major cloud, the **Shenzhen–Hong Kong IX at ¥158/month** undercuts everything, with the catch that it only works behind a supported cloud network and you're paying that cloud server separately.

## Coupons and discounts: what's actually active

MKCloud runs frequent promotional campaigns, and this is where you should double-check anything you read, including this article. The official coupon page currently marks the last sitewide campaign (codes MK-8.8 for 12% off recurring on traffic-billed plans, MK-7.8 for 22% off the first month on dedicated bandwidth) as **ended**, with an explicit note that the codes were valid only during the campaign window.

Third-party roundups published on GitHub list a separate set of codes as long-running: MK-IEPL-WELCOME and MK-IPLC-WELCOME, described as 10% recurring discounts for new customers on the IEPL and IPLC product families respectively, plus CLOUD-2T-NEW and IXCLOUD for cloud-interconnect plans. One of those roundups notes it could stack a new-customer code at checkout. Whether each code still applies to your specific plan is only confirmable in one place: the coupon box on the checkout page, which appears after you log in. Type the code there and let the order total answer the question. It costs nothing to try, and the store's own knowledge base repeatedly says current promotions live in the store, not in archived announcements.

Billing cycles run from one-time payment through monthly, semi-annual, annual, and up to three-year terms, so if a code doesn't apply, longer cycles are the other lever on effective monthly cost.

## Rules and limits to check before you buy

These are the terms that generate support tickets and one-star reviews when people skip them. All of the following come from the official purchase pages and knowledge base:

- **Real-name verification is mandatory.** Purchase requires Chinese identity information, and products are positioned for lawful business use.
- **Province whitelist.** Direct-connect products bind to a single Chinese province and only accept connections from IPs in that province. You select it in the options dropdown at purchase and can change it later. This is an anti-abuse compliance measure, and it means the server is not a general-purpose worldwide access product.
- **Outbound-only egress.** The egress IP doesn't accept inbound connections, so no public websites, no payment callbacks, no receiving mail, no game servers.
- **Refunds are quality-issue-only.** You'll need to submit concrete evidence (specific latency and speed data) through a ticket, and MKCloud adjudicates. There is no no-questions trial period, and after provisioning you cannot switch to a different region's product.
- **Shared bandwidth is peak, not guaranteed.** The 200M/300M figures are ceilings. Sustained throughput depends on current line load.
- **Metered traffic counts both directions** (uplink and downlink), pauses at quota, and can be restored via self-serve traffic reset or a paid upgrade.
- **Upgrades and downgrades go through support tickets**, and downgrading to a cheaper plan does not refund the difference.
- **No SLA by default.** Service-level guarantees, custom routing, and protection details are quote-on-quote via their contact channels.
- **Snapshots and backups are not offered** as product features, so run your own.
- **IPs are datacenter IPs.** The provider explicitly doesn't guarantee native, residential, or streaming-unlocked status.

## How to order, step by step

The purchase flow itself is unremarkable, in a good way. Pick your route and billing type on the store page, choose a plan tier, select an OS image, and in the add-on options dropdown choose the province your connecting IPs belong to. Confirm that you've read the terms (the checkbox text repeats the whitelist and refund rules, so it's worth actually reading), then proceed to cart. Billing cycle and the coupon code field sit right above the order summary; the coupon field only shows usable codes after login.

Provisioning is listed at roughly one minute for in-stock plans, automatic, though payment confirmation and system installation can stretch that a little. Remember that the clock on your real setup time starts after the VPS boots: deploying your own software and, for IX products, wiring up the cloud front are on you. If anything about the route, the whitelist, or your intended use feels uncertain, their knowledge base suggests asking through a ticket before paying rather than negotiating a refund after.

For a compliance-focused cross-border setup with verified dual-IP delivery and published latency figures, [👉 the MKCloud store's IPLC section](https://bit.ly/MKCLoud) is the place to compare live prices across routes before committing to a cycle length.

## Frequently asked questions

**Is an IPLC dedicated server worth it over a cheap CN2 GIA VPS?**
It depends on how much instability costs you. CN2 GIA is far cheaper and fine for latency-tolerant work, but it's still a public route with 50–70ms typical China–Hong Kong latency and peak-hour variance. IPLC removes the public backbone from the equation entirely. If a dropped sync or a stuck checkout session costs real money, the price gap starts to look reasonable; if you're browsing, it never will.

**Can I host a public website on it?**
No. The egress IP is outbound-only by design, so these servers can't receive inbound connections for web serving, callbacks, or mail.

**Does the latency figure on the plan page equal my real-world ping?**
No, and MKCloud says so plainly. The listed 124–134ms (US) or 25–28ms (Japan) covers the in-circuit segment only. Your total round trip adds your local connection to the entry point plus the overseas egress to the destination. Plan around the listed numbers as the fixed floor, not the ceiling of your experience.

**What happens when I hit my traffic quota?**
The server pauses until you buy a traffic reset or upgrade the plan via ticket. Traffic counts in both directions, so a heavy download month burns quota twice as fast as you might expect.

**Can I get a refund if it doesn't work for me?**
Only for demonstrated quality problems, with evidence, through their ticket system, and never as a region switch. Treat the first month as a month you should size conservatively rather than a free trial.

**Are the ¥158 or ¥198 plans the cheapest way in?**
¥158 is real but belongs to the Shenzhen–Hong Kong cloud-interconnect line and requires a supported cloud server in front of it. The Shanghai Telecom IPLC routes start at ¥358 (Japan) and ¥428 (US). Match the route to where your users and platforms actually are, then compare plans within that route.
