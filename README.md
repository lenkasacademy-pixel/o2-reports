# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).

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

Frozen **24 Nov 2026, 8:15 am IST**. September is now a **closed month**: the data
window is the complete **4-30 Sep**, every day settled, and there is no part-day.
`SNAP_DAY` is therefore `null` and all 27 delivery days count toward the headlines.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month closed with two more ordinary days.** The 29th took ₹1,056.20 for 20
calls (₹52.81) and the 30th ₹1,044.52 for 18 calls (₹58.03) — only Pain Management
and Lipoma were still delivering, which the account totals confirm to the paisa on
both days. Those two days moved the headline per-call rate ₹51.08 → **₹51.46**,
still inside the ₹49-53 band every refresh has produced. Read it as flat.

**The 20-second rate is the one that moved.** ₹203.83 → **₹214.17**, because the
last two days bought 38 calls but only 5 that held twenty seconds. The 60-second
call closes the month at ₹478.47.

| | 4-22 | 4-24 | 4-26 | 4-28 | **4-30 (final)** |
|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹49.39 | ₹52.12 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹52.64 | ₹56.01 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹181.34 | ₹209.78 | ₹203.83 | **₹214.17** |

**Final per-campaign totals (September, ex-GST).** Pain Management is the only
campaign Meta still reports ACTIVE; every other one is PAUSED or ARCHIVED.

| Campaign | Spent | Calls | Each | 20s+ | per 20s | 60s+ |
|---|---|---|---|---|---|---|
| Pain Management · Sep 2026 | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 32 |
| Lipoma Removal · Calls | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | 6 |
| Endoscopy · 6 km radius | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 4 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 4 |
| Kukatpally Calls · Clean v2 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 1 |

**Lipoma finished the cheapest line per call placed, and by a long way** — ₹34.25
across 102 calls against ₹56.70 for every other call campaign. It is still holding
the account average down on its own: excluding it, September reads ₹56.70 a call.
Keep both rows in front of the client.

**Pain Management ends as the dearest line per call (₹58.11) but the one that
holds callers.** 61 of its 222 calls (27%) ran past twenty seconds and 32 past a
minute — 68% of the month's 60-second calls on 57% of the call budget.

**Revisions after the last publication.** Meta settled 28 Sep up by ₹4.53 in total
(Autism +₹0.74, Pain +₹0.77, Lipoma +₹3.02) with ₹0.74 of impressions-only drift;
no call counts moved on any settled day. Both 29 and 30 Sep were full days that the
29 Sep snapshot had only seen a few hours of (₹71.22 then, ₹2,100.72 in the end).

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three — and every one of the deep ones is the Gulf ad set.
Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of that is
on the page; the `DAILY` row format has no field for messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal on either side of it.

## Out of scope: October, and a month of silence

This report is September only, and that is now a historical window rather than a
live one. For whoever picks it up next:

- The account **ran again from 1-24 October** and took **₹18,476.76** in that
  window (nothing on 3-5 Oct). None of it is on this page.
- The account has spent **₹0 since 25 October** — **31 consecutive days dark** as
  of this snapshot — while `Pain Management · Sep 2026` still reads ACTIVE at Meta.
  An ACTIVE campaign on a silent account is the same signature `zsports` had when
  it hit its account spending limit, so check Billing → Payment settings and the
  prepaid balance before concluding the campaigns are at fault.
- Extending this report to October would mean a month tab bar, the way
  `halcyon-reports` does it. That is a product decision, not a refresh, so it was
  left alone.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data (a part-day) and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.

**For a closed month, set `SNAP_DAY = null`.** September settled long ago, so there
is no unsettled day to hold back and excluding one would throw away a real day. The
page handles `null` on its own: the `r[1] !== SNAP_DAY` filter then keeps every row,
no "so far" tag is drawn, and the Yesterday card retitles itself *Final day* and
says the month is complete instead of naming a day that is still counting. `YDAY`
becomes the last day with delivery (30 Sep). Do **not** point `SNAP_DAY` at the last
settled day to "keep the shape" — that silently deletes that day from every total.

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
