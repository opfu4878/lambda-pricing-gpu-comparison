# Lambda Labs Alternatives: Real Pricing Compared, the 8-GPU SXM Catch Explained, and How to Choose by Workload

Four things are driving teams to search for Lambda Labs alternatives right now: H100 on-demand pricing that climbed 33% in under 18 months, spot instances vanishing from the lineup entirely, single-GPU access to the SXM variant being removed — the card now ships only in 8-GPU nodes — and "first-come" availability that turns popular configurations into a waiting game. Meanwhile the rest of the market moved the other way: H100 spot rates fell 64% from their 2024 peak, and by one count more than 300 GPU cloud providers launched in 2025 alone.

The alternatives split into three camps: spot marketplaces where you bid on other people's hardware, developer-focused GPU clouds with per-second billing and serverless endpoints, and full-stack clouds that sell the same NVIDIA silicon with the rest of a cloud platform attached. Depending on which camp fits your workload, switching typically cuts 20–50% off the headline H100 rate — or adds billing granularity Lambda doesn't offer at any price.

One warning before the comparisons: a lot of the listicles still ranking for this topic quote Lambda prices that no longer exist. Figures like $2.49–$2.86 for an H100 were accurate in early 2026. As of late 2026, Lambda's published on-demand rates are $3.29 (PCIe) and $3.99 (SXM). If an article's math is built on the old numbers, its recommendation is built on sand.

> **In a hurry? The short version:**
>
> - **Cheapest H100:** Vast.ai, from $1.49/hr on the spot market — no SLA, expect interruptions.
> - **Best for spiky workloads:** RunPod — per-second billing and serverless endpoints with scale-to-zero; H100 PCIe from $2.89/hr on Secure Cloud.
> - **Best full-stack pick:** Vultr — H100 at $2.99/hr, H200 at $3.99/hr, hourly billing across 32 data center locations, Kubernetes and storage in the same account, plus $250 in new-account credit. 👉 [Check Vultr's Cloud GPU lineup](https://www.vultr.com/products/cloud-gpu/?ref=7268283)
> - **Staying on Lambda is still reasonable** if you need full 8-GPU SXM nodes or multi-week clusters and like the preconfigured environment.

## Why teams are switching away from Lambda Labs

None of the four reasons below are about product quality — Lambda's onboarding (PyTorch and CUDA preinstalled, SSH access within minutes) is still one of the nicer experiences in the category. They're about price structure and product shape.

1. **Prices went up while the market went down.** H100 SXM on-demand rose from $2.99/hr in mid-2025 to $3.99/hr by August 2026, a move tied to the capacity deal with Microsoft announced in November 2025. The PCIe variant rose from about $2.49 to $3.29 over the same stretch. Across the wider market, spot H100 rates fell 64% from their 2024 peak during that window.

2. **The 8-GPU SXM minimum.** Single-GPU H100 access on Lambda is PCIe only, at $3.29/hr. The SXM card — the one with 900 GB/s NVLink — is sold exclusively as a full 8-GPU HGX node. If your distributed-training job needs SXM bandwidth but only two or four GPUs, you pay for eight. Every major competitor on this page sells single-GPU SXM.

3. **No spot, no serverless.** Every Lambda instance is a persistent VM at the full on-demand rate. There's no preemptible tier for checkpoint-tolerant training and no scale-to-zero inference product, so idle GPU-hours bill the same as busy ones.

4. **First-come availability.** Lambda describes its instances as self-serve, first-come access. During peak demand cycles the popular configurations disappear, and finding an H100 can mean checking inventory several times a day.

To be fair where fairness is due: Lambda includes free egress, which genuinely matters if you shuttle multi-terabyte datasets between clouds, and its support has a solid reputation with research teams.

## What Lambda actually charges right now

As of late 2026, Lambda's published on-demand lineup covers five GPU models:

| Lambda instance | VRAM | On-demand rate |
| --- | --- | --- |
| B200 SXM | 180 GB | $6.69/GPU/hr |
| H100 SXM | 80 GB | $3.99/GPU/hr |
| H100 PCIe | 80 GB | $3.29/GPU/hr |
| A100 SXM | 80 GB | $2.79/GPU/hr |
| A100 SXM | 40 GB | $1.99/GPU/hr |
| V100 | 16 GB | $0.79/GPU/hr |

Two things worth noticing. There's no mid-tier: no L40S, no A6000, no consumer cards — the budget option is the aging V100. And the 1-Click Clusters product starts at 16 GPUs on a two-week minimum, arranged through their team rather than self-serve, running $9.86/GPU/hr at 16 GPUs down to $8.87 at 256 or more.

## The main Lambda Labs alternatives, side by side

Ten providers cover the realistic option space. Rates below are on-demand, checked against pricing pages and published catalogs between August and October 2026.

| Provider | H100 on-demand | Billing | Spot / serverless | Best for |
| --- | --- | --- | --- | --- |
| RunPod | $2.89 (PCIe, Secure Cloud) | Per-second | Both | Spiky jobs, serverless inference, 3-minute onboarding |
| Vast.ai | From $1.49 (marketplace) | Per-second | Spot + reserved | Lowest rates if you tolerate interruptions |
| Spheron | $1.33 (SXM) | Per-minute | Neither | Cheap SXM via aggregated supply |
| Modal | $1.50 | Per-second | Serverless-native | Python-first inference, scale-to-zero |
| TensorDock | $1.80 | Per-minute | Neither | Broad hardware at near-marketplace prices |
| Hyperstack | $1.95–$2.40 | Per-minute | Neither | Straightforward EU rates |
| Thunder Compute | $2.19 | Per-minute | Neither | Budget A100s at $1.09 |
| DigitalOcean | $1.99 | Hourly | Neither | Managed ML environments, Kubernetes |
| Nebius | From $2.15 | Hourly | Neither | Large European capacity |
| CoreWeave | ~$6.16 (SXM, 8-GPU min) | Hourly | Neither | 70B+ training, 99.5% SLA |

Uptime guarantees vary more than prices do: Lambda contracts 99%, RunPod 95%, CoreWeave 99.5%, and Vast.ai offers no SLA at all — reliability depends on which independent host you rent from. FluidStack ($3.20/hr for H100) is worth a look for latency-sensitive inference, and if you specifically want AMD's MI300X, CoreWeave is the provider with public single-GPU pricing at $3.50/hr.

The billing column matters more than it looks. A per-second provider bills a 47-minute job for 47 minutes; an hourly provider bills 60. Across dozens of short jobs a day, that gap dwarfs a $0.10 difference in headline rate.

It compounds annually, too. One published comparison put a single H100 running at 40% utilization — roughly 3,500 GPU-hours a year — at $10,010 annually on Lambda versus $6,965 on RunPod, back when Lambda still charged $2.86/hr. At the current $3.99 SXM rate, those same 3,500 hours come to **$13,965**. The GPU didn't get faster between those two invoices.

## Vultr: the full-stack alternative most comparisons skip

Vultr rents dedicated NVIDIA datacenter GPUs by the hour, and its H100 lists at $2.99/hr — about 9% below the $3.29 Lambda charges for its only single-GPU H100 option. It rarely appears in these roundups because they center on pure-play GPU clouds; for anyone whose project needs more than a bare GPU box, that's exactly the gap it fills.

### Vultr's Cloud GPU lineup and pricing

Four datacenter GPUs, billed hourly, no contract:

| GPU instance | VRAM | Best for | On-demand rate | Deploy |
| --- | --- | --- | --- | --- |
| NVIDIA H100 | 80 GB | LLM fine-tuning, 13B–70B training | $2.99/GPU/hr | [Deploy H100](https://www.vultr.com/products/cloud-gpu/?ref=7268283) |
| NVIDIA H200 | 141 GB | Long-context, memory-heavy inference | $3.99/GPU/hr | [Deploy H200](https://www.vultr.com/products/cloud-gpu/?ref=7268283) |
| NVIDIA A100 | 80 GB | Widely supported mid-size training | $1.89/GPU/hr | [Deploy A100](https://www.vultr.com/products/cloud-gpu/?ref=7268283) |
| NVIDIA L40S | 48 GB | Inference, image and video workloads | $1.29/GPU/hr | [Deploy L40S](https://www.vultr.com/products/cloud-gpu/?ref=7268283) |

Cheaper pro cards (the RTX 4000 Ada and the four-GPU A16) round out the lineup for budget inference workloads. 👉 [See Vultr's current per-hour pricing](https://www.vultr.com/pricing/?ref=7268283) for live rates on those and on all GPU configurations.

Set against Lambda directly, the numbers get interesting. On the A100, Vultr charges $1.89 for the 80GB card — less than the $1.99 Lambda wants for the 40GB version, with double the VRAM. Against Lambda's B200 at $6.69, Vultr's H200 at $3.99 covers the big-VRAM inference niche at 40% below that rate, though the B200 remains the faster chip for training runs. Vultr added H200 capacity in 2025, so the lineup is current rather than legacy. When rates are this close across providers, also check which variant (PCIe vs SXM) each H100 actually is — interconnect bandwidth changes the picture for multi-GPU training.

A few structural details that affect the bill and the workflow:

- Hourly billing with no minimum term and no reserved-pricing lock-ins to evaluate
- 32 cloud data center locations worldwide
- Bare metal GPU servers when you want the entire node to yourself
- Kubernetes with GPU node pools, plus object storage, load balancers, and managed databases in the same account
- CUDA-capable images and one-click app deployments
- New accounts can claim $250 in credit (valid for the first 30 days at the time of writing — confirm the current offer at signup)

### Where Vultr wins

Against Lambda, it's the single-GPU rates plus a GPU tier Lambda doesn't have — the L40S at $1.29 for inference, the H200 for memory-bound serving. Against the marketplaces, it's predictability: consistent hardware in Vultr-operated datacenters instead of bidding on individual hosts with unknown network quality. There's no per-host reliability lottery, and 32 regions means inference can sit close to your users rather than in one or two zones.

The other practical difference shows up at month three, when your project needs a Kubernetes cluster or a database and you realize the GPU-only accounts don't sell those. With Vultr it's one login and one bill. If that mix matches your project, 👉 [open a Vultr account and put the new-user credit to work](https://bit.ly/VulTR) — a multi-day H100 trial fits comfortably inside the credit.

### Where Vultr is not the answer

A few situations where another camp fits better:

- **Spiky inference with idle periods.** Vultr has no spot tier and no serverless GPU product. RunPod and Modal were built for exactly this, with scale-to-zero and no idle billing.
- **Absolute cheapest rate.** Marketplaces beat $2.99 comfortably — Vast.ai spot listings start at $1.49. If your training survives interruptions, that's the floor.
- **Sub-dollar consumer GPUs.** There's no 4090-class budget tier here; the entry options are pro cards. Vast.ai lists 68+ GPU types including consumer cards, which matters when a model fits in 24GB.
- **Per-second metering.** Vultr bills hourly, so a 47-minute job costs the same as it would on Lambda's clock — the lower rate softens that, but doesn't remove it.

And the one place Lambda clearly wins: egress. Lambda's transfer is free; Vultr includes bandwidth allowances per instance rather than unlimited free transfer. If your month involves moving tens of terabytes between clouds, price that difference before switching.

## How to choose: match the provider to the workload

Rankings like "best overall" hide the actual decision, which comes down to three variables: how fault-tolerant the job is, how spiky usage is, and how much of your stack needs to live in the same account.

- **Eviction-tolerant training, rock-bottom rate** → spot marketplaces: Vast.ai or RunPod's Community Cloud at $1.49–$2.69 for H100. Checkpoint to object storage every 30 minutes — one comparison put expected evictions for a five-day spot run at roughly one, with 10-minute notice.
- **Spiky inference or bursty batch jobs** → RunPod Serverless or Modal: per-second billing, scale-to-zero, no idle charges. Lambda has no equivalent at any price.
- **Single-GPU H100 or A100, no contract** → Vultr ($2.99 / $1.89) or TensorDock ($1.80). Lambda's single-GPU H100 is PCIe-only at $3.29.
- **Full 8-GPU SXM node or a multi-week cluster** → this is where staying on Lambda makes sense: 1-Click Clusters from 16 GPUs at $8.87–$9.86/GPU/hr depending on size, or CoreWeave if a 99.5% SLA is the priority.
- **GPU plus the rest of a cloud** → Vultr: one account covering Kubernetes, storage, and GPUs across 32 regions.

## FAQ

**Is Lambda Labs still worth using in 2026?**
Yes — if your workload is full 8-GPU SXM nodes, multi-week clusters, or you rely on Lambda Stack's preconfigured environment. The common complaints bite hardest at the single-GPU and spiky-workload end, which Lambda's product shape was never built around.

**Which Lambda alternatives bill per second?**
RunPod and Vast.ai bill per second on instances; Modal is per-second and serverless-native. Spheron, TensorDock, Hyperstack, and Thunder Compute bill per minute. Lambda rounds shorter jobs up rather than metering to the second.

**Do any alternatives offer spot H100s?**
Vast.ai and RunPod's Community Cloud list spot H100s around $1.49–$2.69/hr. Budget for evictions: keep checkpoints in object storage and treat spot as interruptible capacity, not a home for a fragile five-day run.

**Why do different articles quote such different Lambda prices?**
Because the prices changed twice. H100 SXM was $2.99/hr in mid-2025 and $3.99/hr by August 2026; the PCIe variant moved from about $2.49 to $3.29. Anything citing $2.49–$2.86 is pre-hike data.

**How do egress and bandwidth fees compare?**
Lambda is the generous one here — free egress. Vultr includes bandwidth allowances with each instance rather than unlimited free transfer, and marketplace hosts vary. Multi-terabyte monthly transfers between clouds can cost real money elsewhere, which is part of Lambda's value for research teams.

## Before you commit

Three checks that take five minutes and prevent the expensive mistakes:

1. Confirm which H100 variant you actually need. SXM's NVLink matters for multi-GPU training; for single-GPU fine-tuning and most inference, PCIe does the job — and it's the cheaper card everywhere it's sold.
2. Estimate annual GPU-hours, multiply by the rate, then check the billing unit. At 40% utilization, the gap between a per-second provider and an hourly one can exceed the gap between headline prices.
3. Burn the free credit before spending cash. Vultr's new-account credit is enough for a serious multi-day H100 trial, and most of the GPU startups on this page offer smaller test credits too.

If your decision landed on "Lambda's simplicity with a lower single-GPU rate and a real cloud around it," that's Vultr's lane: 👉 [compare Vultr's Cloud GPU plans and current rates](https://www.vultr.com/products/cloud-gpu/?ref=7268283). If it landed on per-second billing and scale-to-zero, the serverless specialists do that better than anyone here — and if it's cheapest-H100-with-interruptions, the spot marketplaces remain unbeaten.
