# Unmanaged VPS Hosting: What You Actually Manage, What $12/Month Buys at Spin Servers, and Which Plan Fits

Unmanaged VPS hosting gives you a virtual machine with root access and nobody looking after what runs on it. You pick the OS, install the stack, apply the patches, and rebuild the box when an upgrade goes sideways. The provider's responsibility stops at the hypervisor: hardware, RAID, power, network, datacenter.

Spin Servers' KVM VPS line starts at **$12.00/month** for 2 vCPU, 2 GB DDR4 RAM, 40 GB RAID-10 SSD and 4 TB of monthly transfer on a 1 Gbps port, with one IPv4 and one IPv6 address. The order form labels server management as **Self-Managed**, and the default build is AlmaLinux 9.4 in Dallas, TX.

That price reflects the absence of support, not a discount on the same thing. If nobody on your side can read a `systemctl status` output and act on it, a $12 unmanaged box will cost you more than a managed one before the first month is out.

> **Quick pick:** the 2 vCPU / 2 GB plan at $12/month covers a single low-traffic site, a dev or staging box, a VPN endpoint, or a small bot. Move to the 6 vCPU / 8 GB at $39/month once you're running several sites, a database with real traffic, or a handful of containers. Neither comes with a control panel or a backup service.
>
> 👉 [See every Spin Servers KVM VPS plan and its current price](https://bit.ly/Spinservers)

## Spin Servers KVM VPS plans, all seven of them

The lineup splits into "Simple Application Servers" and "Advanced Application Servers," but the difference is just cores, memory and disk. Every plan is KVM, every plan gets a 1 Gbps port, one IPv4 and one IPv6 address.

| Plan | vCPU · RAM · Storage | Monthly transfer | Price (USD/month) | Order |
| --- | --- | --- | --- | --- |
| Simple 2 vCPU | 2 · 2 GB DDR4 · 40 GB RAID-10 SSD | 4 TB @ 1 Gbps | **$12.00** | [Check this plan](https://bit.ly/Spinservers) |
| Simple 4 vCPU | 4 · 4 GB DDR4 · 80 GB RAID-10 SSD | 8 TB @ 1 Gbps | Not published on the plan page | [Check this plan](https://bit.ly/Spinservers) |
| Simple 6 vCPU | 6 · 8 GB DDR4 · 120 GB RAID-10 SSD | 8 TB @ 1 Gbps | **$39.00** | [Check this plan](https://bit.ly/Spinservers) |
| Simple 8 vCPU | 8 · 8 GB DDR4 · 160 GB RAID-10 SSD | 10 TB @ 1 Gbps | Not published on the plan page | [Check this plan](https://bit.ly/Spinservers) |
| Advanced 12 vCPU | 12 · 12 GB DDR4 · 160 GB RAID-10 SSD | 10 TB @ 1 Gbps | Not published on the plan page | [Check this plan](https://bit.ly/Spinservers) |
| Advanced 16 vCPU | 16 · 16 GB DDR4 · 320 GB RAID-10 SSD | 15 TB @ 1 Gbps | **$74.00** | [Check this plan](https://bit.ly/Spinservers) |
| Advanced 32 vCPU | 32 · 32 GB DDR4 · 500 GB SSD | 20 TB @ 1 Gbps | Not published on the plan page | [Check this plan](https://bit.ly/Spinservers) |

Four of the seven only reveal their price once you choose a billing cycle inside the order form, so I've left those blank instead of rounding them into something that looks tidy. The three figures above are what the product page displays as starting prices.

One detail worth knowing before you assume annual billing saves money: on the 2 vCPU plan the cycles are $12.00 monthly, $36.00 quarterly, $72.00 semi-annually and $144.00 annually. That works out to $12.00/month every time. There is no prepay discount to chase, so pick the shortest cycle you're comfortable with.

## Where the responsibility actually splits

The phrase "unmanaged" hides the only question that matters: which layer of the stack does the ticket window cover? For this class of hosting the split is consistent, and it's strict.

| Layer | Who handles it |
| --- | --- |
| Physical host, RAID array, power, network uplinks, datacenter | Provider |
| Hypervisor, VM provisioning, boot-level connectivity | Provider |
| OS choice, install, reinstalls, kernel and package updates | You |
| Security patching, firewall rules inside the OS, SSH hardening | You |
| Web server, database, PHP/Node/Python runtime, containers | You |
| Control panel (cPanel, Plesk, InterWorx) and its licence | You |
| Backups and restore testing | You, unless a backup service is explicitly included |
| Monitoring, alerting, capacity decisions | You |

How bluntly providers state this varies a lot. Hostwinds spells it out: on an unmanaged VPS it guarantees the server starts and that power, networking and connectivity work, and "will supply no other assistance or support." Liquid Web takes the opposite editorial position, arguing that even an unmanaged plan ought to come with 24/7 support channels and sub-minute first response. Both are describing the same product category with different service promises attached.

The practical test is not what the marketing page says, it's what happens on your first real outage. Before you buy anywhere in this category, find the sentence that describes the support boundary and read it twice. If it isn't there, assume the strictest reading.

Spin Servers' plan pages don't describe a backup service, so treat backups as your own job: snapshot or `rsync` to separate storage, and test a restore before you need one.

👉 [Open the Spin Servers order form and check the plan details](https://bit.ly/Spinservers)

## Picking a plan from the workload, not the spec sheet

Cores and RAM numbers are easy to compare and rarely the deciding factor. Start from what you'll actually run.

**One site, a staging environment, a VPN, a monitoring node.** The 2 vCPU / 2 GB at $12 is enough. A static site or a lightly trafficked WordPress install with a cache in front won't touch 2 GB. This is also the cheapest sensible box for learning server administration with a real public IP.

**Three to ten sites, or one shop with steady traffic.** The 6 vCPU / 8 GB at $39 is the sweet spot in this lineup. 8 GB is where MySQL/MariaDB and a PHP worker pool stop competing for memory, and 120 GB of SSD leaves room for uploads, logs and a local backup copy.

**Heavy application servers, CI runners, game servers, multi-container deployments.** The 16 vCPU / 16 GB at $74 carries 320 GB of disk and 15 TB of transfer. At this size, check whether your workload actually scales across cores; many single-threaded apps won't.

**The 32 vCPU entry.** 32 GB of RAM and 20 TB of transfer is dedicated-server territory in a VM. Confirm the price and the region in the order form before planning around it.

Two sizing rules that save money: choose for today's load rather than a guess at next year's, and upgrade when memory or CPU sits consistently near its ceiling rather than when it spikes once. A VPS you outgrow in three months is cheaper than a big one you never fill.

## Five things that surprise people after they order

**Port 25 is closed by default.** Spin Servers blocks SMTP on all VPS plans to limit IP abuse. If you need outbound mail, you file a ticket with a justification, and the company reserves the right to refuse. Anyone planning a mail server, a newsletter sender or an app that sends transactional email should plan around this from day one, or route mail through a relay.

**No control panel is included.** The order form lists the server as Self-Managed, and a control panel is a separate concern with its own licence cost. If you want cPanel or Plesk, price the licence before comparing totals. Across the category, panels are almost always billed monthly on top of the server, and the licence is the buyer's responsibility on unmanaged plans.

**Backups are not a default.** Managed plans typically bundle daily backups; unmanaged plans usually list them as optional or omit them. A provider that does include nightly backups in an unmanaged plan is the exception worth noting, not the norm.

**Uptime SLA numbers aren't comparable.** You'll see 99.9%, 100% and 99.9999% quoted in the same shopping session. Those figures describe different things: some cover only power and network to the rack, some cover network only, and none of them promise your application stays up. Read what the SLA measures before you treat the number as a ranking. For context on why the distinction matters, third-party downtime research cited in provider comparisons puts the average cost of an outage at around $9,000 per minute for businesses; your own number will differ, but the point stands: an SLA that doesn't cover the failure you had is worth nothing.

**Scaling comes in two flavours.** Some providers let you add RAM or disk individually without a rebuild; others only sell you the next tier up. The difference shows up in year two, when you need 4 GB more memory and the only option is doubling both cores and price. Ask which model applies before you commit.

Also budget the migration time. Repointing a domain to a new server means changing the A record, and DNS propagation commonly takes a few hours and can take up to 72 hours to reach everyone. Don't schedule the cutover for Friday afternoon.

👉 [Start with the $12/month 2 vCPU plan and upgrade later](https://bit.ly/Spinservers)

## How Spin Servers sits against the usual names

The unmanaged VPS market has a few well-known reference points. Their published configurations, for context only:

| Provider | Typical unmanaged range | Support stance | Notable inclusions |
| --- | --- | --- | --- |
| Spin Servers | 2–32 vCPU, 2–32 GB RAM, 40–500 GB SSD, 4–20 TB transfer | Infrastructure only; order form marks plans Self-Managed | 1 Gbps port, 1 IPv4 + 1 IPv6, KVM, RAID-10 SSD |
| Liquid Web | 2–16 vCPU, 2–16 GB RAM, 40–200 GB SSD, 10 TB bandwidth | 24/7 support, first response quoted under a minute | InterWorx panel free, Plesk/cPanel monthly, DDoS protection, Acronis backups up to 50 GB, 100% network uptime SLA |
| Hostwinds | 1–16 vCPU, 1–96 GB RAM, 30–750 GB storage, 1–9 TB bandwidth | Explicitly no technical, management or administrative support | Nightly backups, snapshots, external firewall, load balancer, block storage, custom ISO |
| InMotion | 1–32 vCPU, 1–32 GB RAM, 30–540 GB SSD/NVMe, 2–12 TB transfer | Free online support 365/24/7 | Corero DDoS protection, dedicated IP, US or Europe |
| A2 Hosting | 1–10 cores, 1–32 GB RAM, 25–450 GB SSD/NVMe | 365/24/7 support | HackScan, KernelCare, DDoS protection, 99.9% uptime commitment |

Read that table as a map of trade-offs rather than a ranking. Spin Servers and Hostwinds compete on price per core and leave you to run the stack. Liquid Web and InMotion charge more and put humans behind a ticket queue, which matters if the phrase "no other assistance or support" would keep you up at night. A2 sits in the middle. If you need Windows rather than Linux, check availability carefully: several providers in this bracket don't offer it, and Hostwinds is one that does, with a separate unmanaged Windows line.

## FAQ

**Can I switch to managed later?**
With some providers, yes: Hostwinds lets you upgrade an unmanaged VPS to managed from its control panel with a click, after which full technical support applies. Spin Servers' plan pages describe a self-managed product only, so if a managed path matters to you, confirm it with their team before ordering rather than assuming.

**Can I add RAM without adding CPU?**
Depends on the provider. Some allow resource-level scaling with no rebuild; others only sell tier upgrades. The Spin Servers lineup is sold as fixed configurations, so plan for the tier you'll need rather than assuming you can top up one resource later.

**Does unmanaged include backups?**
Assume no. Backups are optional or absent on unmanaged plans in general, and managed plans are where daily backups usually get bundled. Check the order form and the knowledge base, not the marketing page.

**I've never run a server. Should I buy this?**
No. The sensible path is to stay on shared hosting while your site performs well there, and move to a VPS when you need resources or software that shared hosting can't provide and you're comfortable administering a server. If you want to keep an intuitive panel like cPanel and have someone else handle updates and patching, a managed VPS is the correct purchase even though it costs more.

**Do I get root?**
Yes, that's the point of unmanaged. Full root access is what you're paying for, and it's typically unavailable on managed plans.

## The decision rule

One low-traffic site, a lab box, or a VPN endpoint and you're comfortable on the command line: take the **2 vCPU / 2 GB at $12/month**. Several sites or a small shop with a database: the **6 vCPU / 8 GB at $39/month** is the one that won't need replacing in a quarter. Real application load, CI, or containers: the **16 vCPU / 16 GB at $74/month**.

If you need someone to patch the OS, answer at 3am, or hand you a cPanel login, buy managed hosting instead. The savings here are real, but they're paid for in your own time.

Before you check out, confirm three things on the order form itself: the billing cycle you want (annual saves nothing on the entry plan), the datacenter region, and whether you need port 25 opened. Those three answers decide whether the server you receive matches the one you planned for.

👉 [Compare the Spin Servers KVM VPS plans and pick your configuration](https://bit.ly/Spinservers)
