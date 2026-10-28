# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4–30 Sep; 4 Sep was the first day with delivery).
The month is complete — this is the closing cut, not a running one.

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **last-day card** with that day's billed amount, calls, 20s calls and cost per
  call, broken out by campaign. It reads `YDAY`, and titles itself "Yesterday"
  while the month is still running or "Last day of the month" once it is closed.

## Snapshot

Frozen **28 Oct 2026, 8:10 am IST**, covering **4–30 Sep — September is now
closed and every day in the window is settled**. There is no part-day to hold out
any more, so `SNAP_DAY` is `null` and the headline covers the full month.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month closed dearer than it read on the 28th.** The last two days took
₹2,100.72 for 38 calls but only 5 of them held twenty seconds, so cost per call
went ₹51.08 → **₹51.46** and the 20-second call ₹203.83 → **₹214.17**. That is
the whole move: the 29th and 30th were ordinary on volume and poor on duration.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

On the 29th and 30th only Pain Management and Lipoma ran; every other campaign
had already stopped.

**Meta revised 28 Sep up by ₹4.53** after publication (Autism +₹0.74, Pain +₹0.77,
Lipoma +₹3.02), with impressions and reach up a little on each and no call counts
moved. That is the last revision: nothing else in the month changed.

**Only Pain Management is still ACTIVE.** Lipoma is now PAUSED, so `LIVE` is down
to the single index `4`. Autism, Endoscopy, Kukatpally, the WhatsApp campaign and
NRI Elder Care are all PAUSED.

**Final per-campaign standings for September:**

| Campaign | spend | calls | each | days |
|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 21 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 9 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 5 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 6 |
| Kukatpally (one-day test) | ₹502.22 | 5 | ₹100.44 | 1 |
| WhatsApp (conversations) | ₹5,924.79 | 27 conv | ₹219.44 | 11 |
| NRI Elder Care (website) | ₹2,686.81 | — | — | 4 |

**Lipoma finished the cheapest line on the account by a wide margin** — ₹34.25 a
call against ₹56.70 for every other call campaign put together — and it is paused.
It is the single biggest reason the blended number looks as good as it does; keep
both rows in front of the client.

**Pain Management carried the month**: 21 of the 27 delivering days and 51% of
calls placed. It is also the line that holds callers — 61 of its 222 calls (27%)
ran past twenty seconds, ₹211.48 each.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53;
read it as flat. The 20-second rate is the one that actually drifted, and it drifted
the wrong way: ₹186.55 at the 22nd to ₹214.17 at the close. Per-call figures cover
**call campaigns only**: NRI Elder Care drives website traffic and the NRI +
Bengaluru campaign optimised for WhatsApp conversations, so both sit outside every
per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

**WhatsApp stays paused and unchanged** at ₹5,924.79 for **27 conversations**,
₹219.44 each — identical to the last refresh, since it has not spent since. Meta
still reports 27 first replies, 13 conversations past one message and 5 past three.
None of that is on the page: the `DAILY` row format has no field for messaging
depth.

> **Out of scope: the account kept running into October.** Account
> `924502380456661` spent **₹18,476.76 across 1–24 Oct** (21 delivering days) and
> has been dark since the 25th. This report is September-only by design, so none
> of that appears on the page and no October figure here has been reconciled.
> If the client wants October, it needs its own tab or its own report — say so
> rather than widening this one silently.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`YDAY` is the last day present in the data, which is what the last-day card reads.
`SNAP_DAY` is the part-day hook: while the month is still running it holds that
day's date and the page keeps it out of every total and every rate. **September is
closed, so `SNAP_DAY` is now `null`** — no row's date can equal `null`, so the
filter keeps every day, and the card re-titles itself "Last day of the month"
instead of "Yesterday". Set `SNAP_DAY` back to a date string the moment this report
covers a month that is still accruing, and move it together with `YDAY` — or the
card will silently show a stale day.

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
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer,
  and the baked-figures comment above `CAMPS`) and here — five places in all.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
