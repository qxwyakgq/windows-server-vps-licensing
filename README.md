# Windows Server 2026 VPS: Is It Still Worth Buying, Does the Price Include a License, and How Much RAM Do You Actually Need? (Plans, License Models, Price Check)

Windows Server 2022 left mainstream support in October 2026 and keeps receiving security updates until **14 October 2031**, so a 2022 VPS ordered today is a five-year machine, not a dead end. The case for it over 2025 comes down to two things: your software vendor certifies 2022, and TLS 1.3 is switched on by default at the HTTP.sys layer, so IIS serves modern cipher suites without registry edits.

What actually decides your monthly bill sits further down the page, on the license line. Two hosts can advertise the same 8 GB Windows box and land $60 apart because one bundles an activatable license and the other hands you a trial. Below: Ava Hosting's Windows plans, the license models in this market with verified numbers, current prices at four other providers, and a sizing rule you can apply in two minutes.

> **Quick pick.** Size by RAM, not by vCPU count. 1–2 GB covers a single low-traffic site, a jump box or a test machine. 4 GB is the point where IIS and SQL Server Express can share one server. 8 GB and up is for multi-user RDP, AD DS, or a database with real data in it. Ava Hosting lists managed Windows plans from **€5.00/mo** (1 vCPU, 2 GB RAM, 25 GB NVMe) to **€40.00/mo** (8 vCPU, 16 GB RAM, 160 GB NVMe). 👉 [Check the current Windows VPS tiers and prices](https://my.ava.hosting/aff.php?aff=15562)

## Ava Hosting's Windows Server 2022 VPS plans

Ava Hosting sells these as a managed Windows environment on KVM rather than a bare image you patch yourself. Their engineers handle OS configuration, patch management and Windows Firewall rules, and network-layer DDoS mitigation is included on every plan. The product page states the two ends of the range; the plan selector carries the tiers in between.

| Plan | vCPU · RAM | Storage | Price | Billing | Order |
| --- | --- | --- | --- | --- | --- |
| Entry | 1 vCPU · 2 GB | 25 GB NVMe | €5.00/mo | Monthly | [Order the entry plan](https://my.ava.hosting/aff.php?aff=15562) |
| Top | 8 vCPU · 16 GB | 160 GB NVMe | €40.00/mo | Monthly | [Order the 8 vCPU plan](https://my.ava.hosting/aff.php?aff=15562) |

Prices are the figures published on the Windows VPS product page. The selector at checkout is the source of truth, so confirm the RAM figure you want against the amount shown there before paying.

What that page commits to across the range: dedicated vCPU cores and fixed RAM allocation, so a noisy neighbour can't take your CPU time; NVMe storage on every tier; a dedicated IPv4; Docker and Windows Containers support; and the option to install Ansible, Chef, Puppet or a monitoring agent such as Windows Exporter. Everything runs out of a single data centre in Chișinău, Moldova.

One region is the honest limitation. If your users are in Singapore or California, you're buying European latency plus whatever the network does that day. Independent coverage is thin; a 2026 third-party review measured sub-200 ms TTFB and around 1.2 s full page load from its test location, and also flagged slow ticket responses. Managed patching is worth paying for, but go in expecting to do your own troubleshooting.

## The license question that changes the real monthly price

Hosts handle Windows Server licensing five different ways, and this is where a cheap plan stops being cheap.

**Vultr itemizes it.** Base price and license price are separate columns, and the license scales with the compute plan, from $16/mo on the smallest instance to $384/mo on 24 CPU / 96 GB. The arithmetic on four common sizes:

| Vultr plan | Base price | License price | You actually pay |
| --- | --- | --- | --- |
| 1 CPU · 2 GB | $10/mo | $16/mo | **$26/mo** |
| 2 CPU · 4 GB | $20/mo | $32/mo | **$52/mo** |
| 4 CPU · 8 GB | $40/mo | $64/mo | **$72/mo** |
| 8 CPU · 32 GB | $160/mo | $128/mo | **$288/mo** |

Vultr also states that existing Windows Server licenses cannot be transferred in, so a license you already own doesn't reduce the bill.

**Cloudzy ships a trial license** and offers BYOL as the alternative. You deploy immediately, then sort out activation on your own schedule.

**ColossusCloud holds a Microsoft SPLA** and includes a genuine licensed copy with every VPS; Office and SQL Server are paid add-ons.

**Xaro puts "Windows OS License" on all four plans**, from $7/mo for 2 GB up to $36/mo for 16 GB, so the headline price is the whole price.

**Contabo preinstalls Windows Server Standard** on its Windows VPS line. The page copy doesn't say whether that license is inside the plan price or billed on top, so don't assume either direction.

**Ava Hosting describes a managed Windows environment** and doesn't spell out the licensing model in the plan summary. That's the first thing to ask support, before payment rather than after.

The rule worth applying everywhere: compare advertised price plus license cost, then ask whether that license is still valid in month 13. A €5 plan carrying a 90-day trial is a €5 plan for 90 days. 👉 [Check the Ava Hosting Windows plan page for current bundle details](https://my.ava.hosting/aff.php?aff=15562)

## Is a Windows Server 2022 VPS still the right pick now that 2025 exists?

For most buyers the deciding factor is a vendor support matrix, not a version number. Check your application's supported-platform list first and the OS debate mostly resolves itself.

The timeline matters. Mainstream support for the LTSC release ended in October 2026; extended support, which means security updates without new features, runs to **14 October 2031**. Some host pages round that to "2032" in their headers, while their own FAQ pages say October 2031. Plan around 2031.

Windows Server 2025 is already on the market at Contabo and Vultr, both listing Datacenter and Standard builds plus Core variants. Contabo's comparison adds hotpatching (updates without reboots), Credential Guard, Accelerated Networking and NVMe optimization as the 2025 increments.

Three cases, three answers:

- Your vendor's support list names 2022. Buy 2022. It's still the LTSC most production stacks certify against, and an OS your app supports beats a newer one it doesn't.
- Greenfield project, new code, no vendor constraint. Price 2025 next to 2022 and take 2025 if the monthly difference is small.
- You're migrating an app you can't retest, or a vendor certifies only 2022. Stay on 2022 and put 14 October 2031 in the calendar now.

## What's inside 2022 that 2019 didn't have

These are the features that show up in day-to-day admin work, not just in a changelog:

- **TLS 1.3 on by default for HTTP.sys.** 2022 was the first Windows Server release to ship it that way, with older weak cipher suites disabled. On a live 2022 image, `Get-TlsCipherSuite` returns TLS_AES_256_GCM_SHA384 and TLS_AES_128_GCM_SHA256 as enabled, on build 10.0.20348.
- **secured-core server.** Firmware, hardware and driver attestation combined with virtualization-based security and Credential Guard. It only means something if the host gives you a virtual TPM, which is worth checking on any provider's feature list.
- **SMB encryption with AES-256-GCM and AES-256-CCM**, which covers file traffic between servers on compliance-sensitive setups.
- **DNS-over-HTTPS**, so lookups stay encrypted even on an untrusted network.
- **WSL2 with a real Linux kernel**, letting you run Linux tooling and containers beside the Windows workload instead of renting a second VPS.
- **Container and platform work**: process or Hyper-V isolation, Kubernetes integration, noticeably smaller Windows container images, and SQL Server scaling to 48 TB of memory.
- **Networking**: USO and UDP RSC cut CPU load per packet, HyStart++ and RACK reduce retransmits, and QUIC over SMB removes the VPN from remote file copies.
- **Windows Admin Center**, for browser-based monitoring, service and event log work when opening RDP is inconvenient.

## What the same money buys elsewhere

Verified figures from each provider's own pages, no links, no promo codes:

| Provider | Example plan | Advertised price | Windows license |
| --- | --- | --- | --- |
| Cloudzy | 4 GB / 2 vCPU / 120 GB NVMe / 5 TB | $14.48/mo (page shows 50% off; list $28.95) | Trial license or BYOL |
| Contabo | Cloud VPS 6: 6 vCPU / 12 GB / 200 GB SSD or 100 GB NVMe | €6.00/mo (list €7.50), first 24 months | Windows Server Standard preinstalled; billing not stated |
| Vultr | 4 CPU / 8 GB / 160 GB SSD | $40 base + $64 license = $72/mo | Itemized, non-transferable |
| Xaro | Advanced: 8 GB / 3 vCPU / 85 GB SSD | $19.00/mo (normally $29.99) | Included, labelled "Windows OS License" |

Read the caveats before you treat any of those numbers as a benchmark. Cloudzy's 50% is a running promotion, not a standing price, and it comes with a 14-day money-back window. Contabo's figure is explicitly "for the first 24 months" and the page displays two amounts; the renewal price isn't published. Xaro's strike-through prices are the provider's own and haven't been independently checked. A $14 plan with a trial license and a €40 managed plan are not the same product, and comparing them by headline price tells you nothing useful.

## Which Windows Server 2022 VPS tier fits which job

Providers map their own tiers to workloads, and the mapping is consistent enough to use as a rule.

- **1–2 GB.** A single low-traffic site, a development box, a jump host. Windows takes a real share of memory before your application starts, so don't expect SQL Server to be happy here.
- **4 GB.** IIS plus SQL Server Express on one machine, small internal tools, a staging environment that mirrors production.
- **8 GB.** A site with traffic headroom, or a lean multi-user RDP host for two or three people. Cloudzy labels this band "small site / IIS host".
- **12–16 GB.** Multi-user RDP for a small team, an AD domain controller, or SQL Server with production data. Cloudzy maps 12 GB to "production app / multi-user RDP" and 16 GB to "Active Directory / heavier loads"; ColossusCloud recommends 2022 specifically for domain controllers.
- **24 GB and up.** Several roles on one box, or a database that has outgrown a shared machine. At this point price two smaller VPS against one large one; the license cost often makes splitting cheaper.

One sizing habit saves real money: pick the RAM tier from measured usage, not from a guess about future growth. Upgrading live is usually a panel operation, and paying for 16 GB to run a 3 GB workload for a year is the most common way buyers overspend on Windows hosting.

## Before you order

Two questions to send support, whichever provider you pick. Does the price include a Windows Server license that stays activated for the life of the server, or is it a trial that expires? And what does the plan cost after any introductory period, with what refund window?

Then the decision itself:

- Vendor certifies 2022, and you need managed patching from a single European location: Ava Hosting's Windows plans run €5.00 to €40.00/mo, managed, with DDoS mitigation and dedicated IPv4 included. 👉 [Compare the Ava Hosting Windows VPS tiers](https://my.ava.hosting/aff.php?aff=15562)
- You own a license, or you're happy to activate one yourself: a BYOL-friendly host will be cheaper at the same specs.
- No vendor constraint and new code: price 2025 on Contabo or Vultr before defaulting to 2022.

Whichever way you go, the license line decides more of your bill than the vCPU count does. Get that answer in writing first.
