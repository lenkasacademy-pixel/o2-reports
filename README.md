# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month
is now **closed and fully settled**, so no day is held back as a part-day any more.
See *October is not on this page* below.

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **Yesterday** card (the last complete day) with that day's billed amount,
  calls, 20s calls and cost per call, broken out by campaign.

## Snapshot

Frozen **5 Nov 2026, 8:11 am IST**, covering **4–30 Sep — the complete month**.
September is closed and every day on it has settled, so nothing is held back any
more: `SNAP_DAY` is empty and the last-day card reads the 30th.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month closed two days longer than the last cut showed.** 29 September had
been published as a part-day worth ₹71.22 and 3 calls; it settled at
**₹1,056.20 for 20 calls**. 30 September is new: **₹1,044.52 for 18 calls**.
Between them the two days added ₹2,100.72 and 38 calls — but only 5 of those held
twenty seconds and 1 held sixty.

| closing days | spend | calls | each | 20s | 60s |
|---|---|---|---|---|---|
| 29 Sep · Pain Management | ₹669.68 | 9 | ₹74.41 | 1 | — |
| 29 Sep · Lipoma | ₹386.52 | 11 | ₹35.14 | 2 | — |
| 30 Sep · Pain Management | ₹587.29 | 5 | ₹117.46 | — | — |
| 30 Sep · Lipoma | ₹457.23 | 13 | ₹35.17 | 2 | 1 |

**Both headline rates rose, and the 20-second rate rose much more.** Cost per call
₹51.08 → **₹51.46**; cost per 20-second call ₹203.83 → **₹214.17**. That is the two
closing days: 38 calls at ₹55.28 each is close to the running average, but 5
twenty-second calls out of 38 (13%) is roughly half the month's 24% rate. Read the
20s move as those two days' duration mix, not as a trend.

**Meta revised 28 September up by ₹4.53** after it was published (Lipoma +₹3.02,
Pain +₹0.77, Autism +₹0.74). No call, 20s or 60s count moved on any previously
published day.

**Only Pain Management and Lipoma ran to the end of the month, and Lipoma is now
paused too.** Pain Management is the single campaign still ACTIVE at Meta, so
`LIVE` is down to one index. Final per-campaign standings:

| campaign | days | spend | calls | each | 20s | per 20s |
|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | ₹58.11 | 61 (27%) | ₹211.48 |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | **₹34.25** | 21 (21%) | ₹166.34 |
| Endoscopy | 5 | ₹3,460.95 | 66 | ₹52.44 | 12 (18%) | ₹288.41 |
| Autism | 5 | ₹2,131.13 | 42 | ₹50.74 | 10 (24%) | ₹213.11 |
| Kukatpally (one-day test) | 1 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |

**Lipoma finished the cheapest line on the account by a wide margin** — ₹34.25 a
call against ₹56.70 for everything else — and it held that position every day it
ran. It is also the only campaign whose cost per 20-second call (₹166.34) beat Pain
Management's.

**Pain Management has the most durable calls in absolute terms**: 61 of its 222
calls held twenty seconds and 32 held sixty, ₹403.14 for a minute-long call — the
only campaign on the account where a minute costs under ₹500.

**WhatsApp closed at ₹5,924.79 for 27 conversations**, ₹219.44 each — unchanged
from the last cut, since it stopped spending on 24 Sep. Meta's depth figures are
unchanged too: 27 first replies, 13 conversations past one message, 5 past three,
3 past five, and every deep one is the Gulf ad set. Bengaluru buys a conversation
for ₹160.80 against Gulf's ₹273.88. None of that is on the page; the `DAILY` row
format has no field for messaging depth.

**Read the headline carefully — Lipoma is doing the work:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

The last column is the closed month. Across every cut recorded here the per-call
rate stayed inside ₹49–₹53, so read September itself as flat. **October breaks that
band — see the October section below.** Lipoma held the average down on its own all
month; excluding it September sits at ₹56.70 a call. Keep both rows in front of the
client. Per-call figures cover **call campaigns only**: NRI Elder Care drives
website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal from the 19th to the end of the month.

## October is not on this page — and October spent money

**The account did not stop on 30 September.** It ran through October and billed
**₹18,476.76** on the same two campaigns before going quiet; it has spent ₹0.00 so
far in November. This page is scoped to September only, so none of it shows:

| October (1–31) | spend | impressions | calls | each |
|---|---|---|---|---|
| Pain Management | ₹14,020.41 | 139,236 | 162 | **₹86.55** |
| Lipoma Removal | ₹4,456.35 | 143,894 | 111 | ₹40.15 |
| **Total** | **₹18,476.76** | 283,130 | **273** | **₹67.68** |

(Campaign spend sums exactly to the account's own October total — no campaign is
missing from that table.)

**That is a 32% rise in cost per call, and it is almost all Pain Management** —
₹58.11 in September to ₹86.55 in October, on slightly *more* impressions for 60
*fewer* calls. Lipoma got dearer too (₹34.25 → ₹40.15) but stayed the cheap line.

**A September-only page shows the client a ₹51.46 call that is no longer what a
call costs.** Extending the report to October is a scope decision, not a refresh:
this page has no month tab bar (unlike `halcyon-reports`), so a second month means
new structure. Raise it rather than silently widening the range.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` the last complete day, which is what the card above the
funnel reads. Both are plain constants — move them together on every refresh, or
the card will silently show a stale day.

**When the window is closed, set `SNAP_DAY = ""`.** September is finished and every
day on it has settled, so there is no part-day to hold back: an empty `SNAP_DAY`
filters nothing out of the headline totals, drops the "so far" tag from the day
table, and switches the card's own two labels from "Yesterday / … is still
counting" to "Last day / September is closed". Those two labels are conditional on
`SNAP_DAY` in the template — do not hand-write either one. Leaving
`SNAP_DAY = "2026-09-30"` would have silently cut the last settled day out of every
headline on the page.

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
