# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).
September is now **complete and fully settled**, so there is no part-day inside the scope:
`SNAP_DAY` is `null` and nothing is excluded from the headlines. The account has started
spending again in October (1 Oct Rs 989.84, 2 Oct Rs 537.66, 6 Oct Rs 1,062.44; nothing on
3-5 Oct) -- that is **out of scope** and not on the page. Widening the report to October is a
decision for a human, not this refresh.

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

Frozen **7 Oct 2026, 8:05 am IST**, covering **4-30 Sep -- the complete month**.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The month closed with only Pain Management and Lipoma running.** Nothing else
spent after 28 September. The last two days were ordinary in spend and poor in
duration:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

**Those 38 closing calls brought only 5 that held twenty seconds**, and that is the
whole story of this refresh: the per-call rate barely moved (Rs 51.08 -> Rs 51.46)
while **the 20-second call got dearer by Rs 10.34, Rs 203.83 -> Rs 214.17**. The 20s
share of placed calls fell from 25.1% to 24.0%. Watch whether October repairs it.

**Pain Management ended expensive.** Rs 74.41 a call on the 29th and **Rs 117.46 on
the 30th** (5 calls on Rs 587.29), against its Rs 58.11 month average. Two days is
not a trend, but it is the dearest it has been and it is one of only two live lines.

**Lipoma is still the cheapest line per call placed, and it closed the month that
way** -- Rs 35.14 on the 29th and Rs 35.17 on the 30th, against Rs 34.25 for the
month. Over September it took Rs 3,493.24 for **102 calls at Rs 34.25**, against
Rs 56.70 for everything else. It is also the cheapest 20-second call on the account
at Rs 166.34.

**Closed-out campaigns.** Autism finishes at Rs 2,131.13 for 42 calls (Rs 50.74),
10 over twenty seconds at Rs 213.11 -- it last spent on the 28th. Endoscopy finishes
at Rs 3,460.95 for 66 calls (Rs 52.44) but only 12 held twenty seconds,
**Rs 288.41 per real conversation** -- the dearest of the call campaigns bar the
one-day Kukatpally test (Rs 502.22 for 5 calls, Rs 100.44 each).

**Small revisions this refresh.** Meta settled 28 Sep up by Rs 4.53 (Autism +Rs 0.74,
Pain +Rs 0.77, Lipoma +Rs 3.02); no call counts moved. The 29th had been published as
a part-day at Rs 71.22 for 3 calls and settled at Rs 1,056.20 for 20.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each --
re-pulled this refresh and unchanged. Meta also reports how far each went: 27 first
replies, 13 conversations past one message, 5 past three, 3 past five. None of that
is on the page yet; the `DAILY` row format has no field for messaging depth.

**Read the headline carefully -- Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 51.03 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 53.24 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 184.36 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 191.08 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49-53;
read it as flat. The 20-second rate has not: it is now the highest it has been.
Excluding Lipoma the account sits at Rs 56.70 a call. Keep both rows in front of the
client. Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both
sit outside every per-call figure.

**18 September was a near-total stop** -- the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the part-day at the end of the data and `YDAY` the last complete day,
which is what the Yesterday card reads. Both are plain constants — move them together
on every refresh, or the card will silently show a stale day. **When the scope month is
closed there is no part-day: set `SNAP_DAY = null`** and `YDAY` to the last day of the
month. The card and the day table both test for a part-day actually being present, so
with `null` nothing is excluded and the card re-titles itself "Last day of the month".

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
