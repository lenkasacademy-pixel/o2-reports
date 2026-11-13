# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4–30 Sep; 4 Sep was the first day with delivery).
The month is **complete** — there is no part-day left in the data. See
*October is not in this report* below.

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

Frozen **13 Nov 2026, 8:20 am IST**, covering the complete month **4–30 September**.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September is closed.** The last two days settled and the 30th was added:

| | 4–28 (as published) | 4–30 (now) |
|---|---|---|
| Ad spend | ₹28,994.36 | **₹31,099.61** |
| Calls placed | 399 | **437** |
| Cost per call placed | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹213.69 | **₹226.13** |

The per-call rate barely moved, but **the 20-second rate jumped ₹10.34**, because the
last two days bought volume without duration: 29–30 Sep together took ₹2,100.72 for
38 calls (₹55.28 each, in line) but only **5** of them held twenty seconds — a marginal
₹420 per real conversation against the month's ₹214.17. Two days is not a trend, but it
is the whole of the move, and it is worth saying rather than letting the headline drift.

| Campaign (September) | Spend | Placed | Each | 20s+ | Per 20s |
|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | **₹166.34** |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 |
| Kukatpally (one day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |
| NRI Elder Care (web) | ₹2,686.81 | — | — | — | — |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | — | — | — | — |

**Lipoma Removal finished cheapest on both measures and is now PAUSED.** Over its nine
days it took ₹3,493.24 for 102 calls at **₹34.25**, against ₹56.70 for every other call
campaign, and ₹166.34 per 20-second call against ₹226.13. It is the line worth restarting.
`LIVE` is now `new Set([4])` — **Pain Management is the only campaign still ACTIVE at
Meta**, and even it has not spent since 24 October.

**Revisions this refresh.** Meta settled 28 Sep up by ₹4.53 in total (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02); no call counts moved. The 29th, a part-day at ₹71.22 when
last published, closed at **₹1,056.20** for 20 calls, and the 30th came in at ₹1,044.52
for 18.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each, unchanged.
Re-pulled this refresh: 27 first replies, 13 conversations past one message, 5 past three.
(The `messaging_user_depth_5_message_send` key did not come back on this pull; the
earlier reading of 3 past five is left as recorded.) None of that is on the page — the
`DAILY` row format has no field for messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet.

## October is not in this report

The scope of this page is September, and that is unchanged — but the account did not
stop at the end of September, so a reader should know what is missing:

- **1–2 Oct** spent ₹1,527.50, **6–24 Oct** spent ₹18,949.28. Nothing on 3–5 Oct.
- **The account has spent ₹0.00 every day since 25 October** — 20 consecutive days to
  13 Nov. `Pain Management` is still ACTIVE but has not delivered since the 24th.
- Lifetime, `Pain Management` is at ₹26,920.88 / 384 calls and `Lipoma Removal` at
  ₹7,949.59 / 213 calls — roughly double what September alone shows for each.

**Adding October would be a design change, not a refresh**: unlike `halcyon-reports`
this page has no month tab bar, so a second month means either widening the window
(and with it every headline, the Yesterday card and the chart's calendar) or building
tabs. That is a call for a human. **The dark run since 25 Oct is the thing worth
raising with the client first.**

## A multi-campaign daily pull can silently return zeros

**This bit the report on 13 Nov 2026.** One `ads_get_ad_entities` call with
`level: "campaign"`, `time_increment: "1"` and all **seven** campaign ids returned the
full 7 × 30 = 210 rows — and every one of `Lipoma Removal`'s 30 rows came back
`amount_spent: 0`, `impressions: 0`, `results: "Not available"`. The same window
requested for that **one** campaign returned its real days (₹125.63 on the 22nd through
₹457.23 on the 30th).

Nothing in the response flagged it: no error, no missing id, no short page. **The
account reconciliation is what caught it** — campaign sums were short of the account's
own daily total on every day from 22 Sep (Lipoma's first day) onward, by exactly
Lipoma's spend. That check is not optional; without it this refresh would have
published ₹3,493.24 and 102 calls as zero and quietly restated the whole month.

If a day fails to reconcile, **re-pull the suspect campaign on its own** before
believing a zero.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is a part-day**, and
`YDAY` the last complete day, which is what the Yesterday card reads. Both are plain
constants — move them together on every refresh, or the card will silently show a
stale day.

**With the month closed, `SNAP_DAY` is `""`.** Nothing is then excluded from the
totals, no day carries the *so far* tag, and the card titles itself *Last day of the
month* and says September is closed instead of naming a day that is still counting.
The page works this out from `PART = !!SNAP_DAY && DAILY has that day`, so if a future
refresh re-opens a live window it only has to set `SNAP_DAY` again.

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and dropped
  back to `{4}` on 13 Nov when Lipoma was paused. Keep it in step with the statuses
  or the "live" tag lies.
- Update the snapshot date in `index.html` — **four places**: the title comment on
  line 8, the masthead stamp, the footer line, and the comment above the baked
  figures — and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
