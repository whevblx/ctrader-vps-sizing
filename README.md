# cTrader VPS: How Much RAM Do Your cBots Need, Which City Should the Server Sit In, and What Does AVA Hosting Charge? (Full Plan Table)

AVA Hosting's cheapest plan with real headroom for cTrader Desktop is **VPS Basic at €10.00 per month**: 2 vCPU, 4 GB RAM, 50 GB NVMe. If you run several cBots and kick off a backtest in the same session, take **VPS Power at €20.00 per month** for 8 GB. The €5 VPS One will launch cTrader, but 2 GB gets thin once Windows and one instance are loaded.

Below is the sizing rule that decides your plan, the broker server locations that decide your city, what AVA includes for the money, and what four other providers charge for the same job.

> **Quick pick**
> - One instance, one or two cBots, no backtesting → VPS Basic, €10.00/mo
> - Several cBots plus backtests → VPS Power, €20.00/mo
> - Two cTrader IDs, prop-firm evaluations, constant optimisation → VPS Extra, €30.00/mo
>
> 👉 [See AVA Hosting's current VPS plans and prices](https://my.ava.hosting/aff.php?aff=15562)

## Every AVA Hosting plan, side by side

| Plan | vCPU / RAM / NVMe | Price | What it realistically runs in cTrader | Order |
| --- | --- | --- | --- | --- |
| VPS Nano | 1 / 512 MB / 20 GB | €11.00 per year | Nothing useful here; 512 MB cannot hold Windows plus a cTrader instance. Listed as 0 available | [Check availability](https://my.ava.hosting/aff.php?aff=15562) |
| VPS One | 1 / 2 GB / 25 GB | €5.00/mo | One instance, one or two cBots, no backtests. Workable, not comfortable | [Order VPS One](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Basic | 2 / 4 GB / 50 GB | €10.00/mo | One instance with a few cBots and room left for Windows | [Order VPS Basic](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Lucky | 2 / 6 GB / 70 GB | €15.00/mo | Same as Basic with more space for chart-heavy workspaces | [Order VPS Lucky](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Power | 4 / 8 GB / 90 GB | €20.00/mo | One instance, several cBots, a backtest running alongside | [Order VPS Power](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Extra | 6 / 12 GB / 120 GB | €30.00/mo | Two instances, or long optimisation runs on one | [Order VPS Extra](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Ultra | 8 / 16 GB / 160 GB | €40.00/mo | Multiple cTrader IDs, several accounts, heavy backtesting | [Order VPS Ultra](https://my.ava.hosting/aff.php?aff=15562) |

Every plan on that list ships with Intel Xeon E5 cores, NVMe storage, a 1 Gbps port (100 Mbps on the Nano), unlimited traffic, DDoS protection, full root access, a control panel, 24/7 support and a **99.9% uptime SLA**. The plan cards also list weekly backups as included. The Nano card notes that port 25 is closed, which matters for mail and not for trading.

Two things to know before you compare these numbers with anyone else's. The figures are published as "starting from" prices in EUR on monthly billing, and the price ladder by RAM is €5 for 2 GB, €10 for 4 GB, €15 for 6 GB, €20 for 8 GB, €30 for 12 GB, €40 for 16 GB. AVA also runs a separate "Self-hosted Start" order flow with an entry tier at **€2.00/mo for 1 vCPU and 1 GB**, and slightly different NVMe sizes at the top of the range (100 GB instead of 90 GB at €20, for example). If you land on that page, match by RAM rather than by storage.

## Why your cBot stops when your laptop sleeps

cBots execute inside cTrader Desktop. Close the application, drop the connection, or let Windows install updates and reboot, and every bot stops until you reopen it and sign back in. cTrader Web and the mobile apps are for monitoring; neither one executes a cBot. That single fact removes "I'll just leave the laptop open" from the list of options.

The build you install is your broker's branded cTrader, taken from the broker's own download page, signed in with your own cTrader ID. On a Windows Server it behaves exactly as it does on Windows 10 or 11, charts and indicators included. On AVA's side you get root access, which on Windows means Administrator, so you install the platform yourself over RDP in a few minutes.

One installation goes further than most people expect. A single cTrader Desktop instance signed in with one cTrader ID can hold accounts at several brokers, and each cBot instance is bound to one account and one symbol. Live account, demo and a prop-firm evaluation can run side by side from the same box. You only need a second installation when the accounts belong to different cTrader IDs or you want them isolated.

## Sizing: 1 to 2 GB per cTrader instance, plus Windows

Plan on **1 to 2 GB of RAM per cTrader instance on top of what Windows itself uses**, and more while a backtest or optimisation is running in Automate. cTrader is heavier than MetaTrader 4, which is where most "2 GB was enough for MT4" advice goes wrong.

That gives a straightforward mapping:

- **2 GB** leaves almost nothing after Windows. One instance at the low end of its footprint, one or two bots, no optimisation runs.
- **4 GB** is the first tier where Windows plus one instance plus a handful of cBots fits with headroom.
- **8 GB** is the comfortable place to be: one instance, several cBots, and a backtest without starving the live bots.
- **12 GB and up** covers a second instance or an overnight optimisation that would otherwise eat the machine.

Cores matter for backtests more than for live trading. A live cBot on a 15-minute chart barely touches a modern vCPU. Modelling years of tick data does, which is why the four cores on VPS Power at €20 make more sense than the two cores on VPS Basic if you iterate on strategies.

👉 [Pick the AVA Hosting plan that matches your cBot count](https://my.ava.hosting/aff.php?aff=15562)

## Choosing the city: where your broker's cTrader servers actually sit

Brokers publish their server locations, and the picture as of October 2026 looks like this. IC Markets' cTrader servers name **Equinix LD5** and FxPro's name **LD4**, both in the Slough campus outside London. FP Markets, Axi and Global Prime name **NY4** in New York. Admirals, Darwinex and BlackBull name LD4 or LD5. FXTM names **Frankfurt**. Exness sits in **Amsterdam**.

The latency gap between "same campus" and "same country" is large. Providers publishing measurements put a server in the same campus as the broker at **under 1 ms**, and a server in the same metro but a different building at roughly **0–10 ms**. A server in Moldova or Germany talking to LD4 is a different order of magnitude again, which is why the city question comes before the RAM question for anyone running a fast strategy.

Two cautions that the marketing pages skip. Brokers move servers, and the same broker can run different platforms or different legal entities in different cities, so check the server name shown in the cTrader login screen and measure the ping from a trial server before you commit. And low latency is a network measurement, not a promise about fills: slippage still depends on the broker, the venue, the order type and the market at that moment.

AVA's plan cards don't name a data centre or offer a city picker, and the brand's trading-VPS page has described its servers as hosted in **Chișinău, Moldova**. For a bot trading bar closes on M15 or slower, that's noise. For anything scalping around the London or New York open with a tight target, ask support where the box will physically sit and what ping they see to your broker's server before you pay. If the answer doesn't work for your strategy, that's a reason to walk away, not a detail to discover later.

## The two-year cost, and what AVA doesn't publish

At the published monthly rates, VPS Basic runs **€120 a year** and VPS Power **€240 a year**. Nothing on the plan cards suggests a renewal premium, and billing is monthly in EUR, so the cost of choosing wrong is one month rather than one year. That's a genuine advantage over providers who discount the first term and raise the price on renewal.

What isn't published is a money-back window. AVA's pages don't state a refund period, and the cards don't say whether VAT is included in the displayed price or added at checkout. Both are worth a support ticket before payment, because the providers in the next section publish 14 or 15 days and you should know what you're giving up.

The other item to confirm is Windows. AVA's trading-VPS pages list Linux or Windows as a choice at order time, but the plan cards don't name a Windows Server version or say whether the licence is bundled. Ask for the exact build (2019, 2022 or 2025) and whether it's included in the €10 or €20. A cheap VPS with an unbudgeted licence is not a cheap VPS.

👉 [Start on monthly billing and test the setup for one month](https://my.ava.hosting/aff.php?aff=15562)

## How the alternatives price the same job

Prices below come from each provider's own pages on the dates shown. They're in different currencies with different inclusions, so read them as anchors, not as an average.

| Provider | Published entry price | Locations named | Uptime claim | Refund window |
| --- | --- | --- | --- | --- |
| QuantVPS | $199.99/mo seen on one page, plan not labelled | New York, London; dedicated tiers on the NY4 campus | 99.999% with a published credit table | 14 days |
| MassiveGRID | from $2.87/mo (page dated 25 Oct 2026) | London, New York, Frankfurt, Singapore | 100%, no credit terms published | 15 days |
| ForexVPS | from $28.80/mo | 21 locations | 100% guarantee | 14 days |
| Inservers | from ₹880/mo plus 18% GST (checked 2 Nov 2026) | Greater Noida, Delhi NCR | 99.9% | not stated |

The uptime column deserves a note. QuantVPS is the only one of the four that publishes measurement rules, exclusions and a credit schedule, which makes its 99.999% checkable. The 100% figures are marketing commitments without terms attached, and should be read that way.

On latency, the same split applies. QuantVPS publishes 0–10 ms from New York to FX brokers and under 1 ms from its NY4-campus dedicated tiers. MassiveGRID publishes under 10 ms within London and under 1 ms to brokers hosted in the same city. ForexVPS advertises "as fast as 1 millisecond". Different routes, different measurements, no common yardstick.

Where the cheap end of the market costs you: a 2 GB plan for under $3 a month is fine for a demo bot and cramped for real work, exactly as 2 GB is on AVA. Several brokers also hand out a free VPS once you deposit or hit a volume threshold. Those are usually small shared instances in a city the broker picks, sized for one bot on one account. If you want to choose the city or run more than one instance, you're buying your own.

## Who should not buy a cTrader VPS

You don't need one if you place trades by hand and close the platform when you're done. Nothing is running while you're away, so a server has nothing to keep alive.

You don't need one if you already have a Windows machine that genuinely stays on, on a wired connection with a UPS, and you're running a single slow bot. That's a real setup, and €120 a year buys a lot of patience.

# or FIX on Linux. That route skips the desktop entirely, and AVA's **€5 VPS One** with 2 GB is enough for it. Paying €20 for 8 GB of Windows to run a process that never draws a chart is waste.

And you shouldn't buy from AVA specifically if your strategy lives or dies on single-digit milliseconds to LD4 or NY4 and support can't confirm a nearby location. That's a legitimate reason to look elsewhere, and it's better to find out from a support reply than from a month of puzzling fills.

## Three questions before you order

Work through these in order, because the first one usually settles the plan.

1. **How many cBots, and do you backtest on the same box?** One or two bots with no optimisation: VPS Basic at €10. Several bots plus backtests: VPS Power at €20. Overnight optimisation or a second instance: VPS Extra at €30.
2. **How many cTrader IDs?** One ID with accounts at several brokers fits a single installation, including a live account, a demo and a prop-firm evaluation. Two IDs means two installations, which pushes you up a tier for RAM.
3. **Where is your broker's cTrader server?** Check the server name in the login screen, then ask AVA what latency they measure to it from their location. If the number is unacceptable for your strategy, stop here.

Before paying, confirm four things in writing: the data centre city, the Windows Server version and whether the licence is included, the backup schedule, and whether VAT applies on top of the displayed price. Get the refund question answered too, since AVA doesn't publish a window and monthly billing is your only stated protection.

Ready to size it properly? 👉 [Compare AVA Hosting's VPS plans and order the tier you need](https://my.ava.hosting/aff.php?aff=15562)
