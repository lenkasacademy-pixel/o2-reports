# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).
The month is now complete: the data runs 4-30 Sep.

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

Frozen **1 Oct 2026, 8:15 am IST**, covering **4-30 Sep - September is now a
complete month**. The 1 Oct part-day (₹11.73) is outside the September scope
and is not in the data at all; `SNAP_DAY` points at it so the Yesterday card
still explains why the report stops where it does.
Ad spend ₹31,093.55 + 18% GST ₹5,596.84 = **₹36,690.39 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. ₹51.45 per call placed and
**₹214.11 per call that actually held 20 seconds**.

**The month closes with two campaigns live and both headline rates up.** Cost
per call ₹51.08 -> ₹51.45, the 20-second call ₹203.83 -> ₹214.11. Two
refreshes of improvement were given back; the per-call rate is still inside the
₹49-53 band it has held all month, so read it as flat, but the 20-second rate
is now the worst reading of the month.

**29 September settled nearly fifteen times its part-day value.** It was
published at ₹71.22 for 3 calls because the snapshot caught it at 11:10 am; it
closed at **₹1,056.20 for 20 calls (₹52.81)**. This is exactly why the
part-day never sets a headline.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| **29 Sep** Pain Management | ₹669.68 | 9 | ₹74.41 | 1 |
| **29 Sep** Lipoma | ₹386.52 | 11 | ₹35.14 | 2 |
| **30 Sep** Pain Management | ₹586.16 | 5 | ₹117.23 | **0** |
| **30 Sep** Lipoma | ₹452.30 | 13 | ₹34.79 | 2 |

**Pain Management is the problem and 30 Sep is the warning.** It took ₹586.16
for 5 calls - **₹117.23 each, by far its dearest day of the month** - and not
one of those calls held twenty seconds. Its 29th was already poor at ₹74.41.
Across September it is ₹12,899.34 for 222 calls (₹58.11), with 61 of them
(27.5%) past twenty seconds at ₹211.46 each. Two bad days do not make a trend,
but this is the live campaign carrying most of the budget, so watch the 1st and
2nd before spending further.

**Lipoma is still the cheapest line per call placed, and it is now nine days
running.** It closes September at ₹3,488.31 for **102 calls at ₹34.20**,
against ₹56.70 for everything else. On the 30th it was ₹34.79 while Pain
Management was ₹117.23 - a 3.4x gap on the same day.

**Autism is finished for the month at ₹2,131.13 for 42 calls (₹50.74)**,
10 of them past twenty seconds. It spent nothing after the 28th and is PAUSED.
**Endoscopy is unchanged** at ₹3,460.95 for 66 calls (₹52.44), only 12 past
twenty seconds - ₹288.41 per real conversation.

**Revisions this refresh.** Meta moved Lipoma up ₹0.09 (and 2 impressions) on
30 Sep *between two calls minutes apart* during this very refresh; the campaign
and account pulls were re-taken until they agreed. No other day moved and no
call count changed. 29 and 30 Sep are both still inside Meta's ~48h revision
window, so expect them to drift by a rupee or two.

**Read the headline carefully - the whole improvement is still Lipoma:**

| | 4-22 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.45** |
| ...excluding Lipoma | ₹51.55 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.11** |
| ...excluding Lipoma | ₹187.72 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.11** |

Excluding Lipoma the account pays ₹56.70 a call - its dearest reading yet.
Keep both rows in front of the client. Per-call figures cover **call campaigns
only**: NRI Elder Care drives website traffic and the NRI + Bengaluru campaign
optimised for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent ₹6.43 that
day, 122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44
each - unchanged this refresh. Meta also reports how far each went: 27 first
replies, 13 conversations past one message, 5 past three, 3 past five - and
every one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for
₹160.80 against Gulf's ₹273.88. None of that is on the page yet; the `DAILY`
row format has no field for messaging depth.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data (a part-day) and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
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
