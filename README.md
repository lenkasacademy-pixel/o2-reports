# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
The month is complete. October spend exists and is **not** on the page - see below.

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **Last full day** card (the last complete day with delivery) with that day's billed amount,
  calls, 20s calls and cost per call, broken out by campaign.

## Snapshot

Frozen **27 Nov 2026, 8:10 am IST**, covering **4-30 September - the month is
complete and every day in it is settled**. There is no part-day in this cut, so
`SNAP_DAY` is empty and nothing is held out of the headlines.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The account has spent nothing since 24 October.** Every campaign but Pain
Management is paused, and Pain Management is `ACTIVE` with delivery `off`,
substatus **`account_spend_limit_reached`** - the ad account has hit its
**account spending limit**. It is a limit on the account, not a fault in the
campaign: raise or remove it in Billing -> Payment settings and delivery
resumes. The exact limit value cannot be read through the API tools used here;
check it in Ads Manager. This is the same failure mode `zsports` hit in
September.

**September closed cheaper per call than it looked, and dearer per real
conversation.** The last snapshot published 4-28 Sep at ₹51.08 a call and
₹203.83 per 20-second call. The two days that have settled since added
₹2,100.72 of call spend and 38 calls but only 5 more calls that held twenty
seconds, so the placed rate barely moved while the 20-second rate rose:

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside
₹49-₹53 - read it as flat. The 20-second rate is the one that drifted, and it
drifted on the last two days of the month. Lipoma is still holding the average
down on its own; excluding it the account sits at ₹56.70 a call.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations,
so both sit outside every per-call figure.

**The 29th and 30th, now settled.** At the last snapshot the 29th was a
₹71.22 part-day showing 3 calls. It settled at **₹1,056.20 for 20 calls**
(Pain ₹669.68 / 9, Lipoma ₹386.52 / 11), and the 30th closed the month at
**₹1,044.52 for 18 calls** (Pain ₹587.29 / 5, Lipoma ₹457.23 / 13) - the one
day Lipoma outsold Pain Management more than two to one. That is exactly why the
part-day is excluded: it was understating the day by a factor of fifteen.

**Meta revised 28 September up by ₹4.53 after publication** (Lipoma +₹3.02,
Pain +₹0.77, Autism +₹0.74). No call counts moved on any previously published day.

### Where September finished, per campaign

| Campaign | Spend | Calls | Each | 20s+ | Per 20s | 60s+ | Status |
|---|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 32 | ACTIVE, not delivering |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | 6 | PAUSED |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 4 | PAUSED |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 4 | PAUSED |
| Kukatpally (1 day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 1 | PAUSED |
| **Call campaigns** | **₹22,488.01** | **437** | **₹51.46** | **105** | **₹214.17** | **47** | |
| NRI Elder Care (web) | ₹2,686.81 | — | — | — | — | — | PAUSED |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | — | — | — | — | — | PAUSED |

**Lipoma finished the cheapest line per call placed by a wide margin** - ₹34.25
against ₹56.70 for everything else - and it was the cheapest on nine of the
eleven days it ran. It is also the second-cheapest per 20-second call
(₹166.34), behind nothing on this account. It is paused.

**Pain Management carried the month** (₹12,900.47, 57% of call spend, 222 of 437
calls) and holds callers best in absolute terms: 32 of the account's 47
60-second calls are its, at ₹403.14 each.

**Endoscopy closes at ₹288.41 per real conversation** - 66 calls at ₹52.44 but
only 12 held twenty seconds. The dearest of the call campaigns bar the one-day
Kukatpally test.

**18 September was a near-total stop** - the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each -
unchanged from the last cut. Meta also reports how far each went: 27 first
replies, 13 conversations past one message, 5 past three. (The `depth_5` key is
no longer returned for this campaign; the previous cut recorded 3.) Every one of
the deep ones is the Gulf ad set. Bengaluru buys a conversation for ₹160.80
against Gulf's ₹273.88. None of that is on the page - the `DAILY` row format has
no field for messaging depth.

## October 2026 is not on this page

The page is scoped to September, so **₹18,476.76 of October spend is not shown
anywhere in it.** The account ran 1-24 October on two campaigns and then stopped:

| Campaign | 1-24 Oct spend | Calls | Each |
|---|---|---|---|
| Pain Management | ₹14,020.41 | 162 | ₹86.55 |
| Lipoma Removal | ₹4,456.35 | 111 | ₹40.15 |
| **Total** | **₹18,476.76** | **273** | **₹67.68** |

**October ran 31% dearer per call than September** (₹67.68 against ₹51.46), and
the whole of that is Pain Management: ₹86.55 a call in October against ₹58.11 in
September, on roughly the same impressions (139,236 vs 138,210). Lipoma held its
line (₹40.15 against ₹34.25).

**This needs a decision, not a refresh.** Extending the page to October means
either widening the scope constant or adding a month tab bar like
`halcyon-reports` has; both are structural changes rather than a data refresh,
so they are deliberately not made here. Until one is made, the live page stops
at 30 September and the client sees nothing of October.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data (a part-day) and `YDAY` the last
complete day, which is what the Last full day card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.

## Refreshing

`DAILY` rows are
`[campIdx, "YYYY-MM-DD", spend, placed, calls20s, calls60s, tapped, impressions, reach, linkClicks]`.

Pull with Meta MCP `ads_get_ad_entities`, `level: "campaign"`, `time_increment: "1"`.

- **Calls placed** come from `results` where the indicator is
  `actions:click_to_call_native_call_placed`. There is no queryable `calls` field.
- **20s and 60s counts are not directly queryable either.** They are derived from
  `cost_per_action_type`: `spend ÷ cost_per_action_type:click_to_call_native_20s_call_connect`
  (and `_60s_`). Each division lands on a whole number — if one does not, something
  is wrong, so assert that. Cross-check by running the same query without
  `time_increment` and confirming the per-campaign period totals match the sum of days.
- `cost_per_action_type:click_to_call_call_confirm` gives taps-to-call (`tapped`).
  It is attributed on its own schedule, so per-day it can exceed or trail calls
  placed; only the period total is comparable. The page does not display it.
- A day with spend but no `click_to_call_native_*` entry genuinely had none. A day
  with **zero spend** (delayed attribution, e.g. 6 Sep) yields no derivable
  durations — record 0 and treat it as unknown, not as a real zero.
- The account returns a row for every campaign × every day, almost all empty; keep
  only rows with spend, calls or impressions. `filtering` on `amount_spent > 0` is
  silently ignored alongside `time_increment` — filter locally.
- Recent days keep settling for ~48h; re-pull the whole month rather than appending.
- `CAMPS` order must not be reshuffled; `DAILY[0]` indexes into it. **Append new
  campaigns to the end** — Lipoma Removal was added as index 6 on 23 Sep for
  exactly this reason.
- `LIVE` is a `Set` of campaign indexes still ACTIVE at Meta, not a single index.
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused. Keep it
  in step with the statuses or the "live" tag lies.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
