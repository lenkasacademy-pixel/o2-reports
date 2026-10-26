# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery, to 30 Sep).
The month is closed; October delivery exists and is deliberately out of scope - see below.

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

Frozen **26 Oct 2026, 8:20 am IST**, covering **4-30 September**. September has
closed, so **every day on this page is settled** - there is no part-day to exclude
and `SNAP_DAY` is `null`.

Ad spend INR 31,099.61 + 18% GST INR 5,597.93 = **INR 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. INR 51.46 per call placed and
**INR 214.17 per call that actually held 20 seconds**.

### What the last two days of the month did to the headline

The previous cut stopped at the 28th. Adding the 29th and 30th moved the
20-second number materially and the per-call number barely at all:

| | 4-28 Sep (as published) | 4-30 Sep (now) |
|---|---|---|
| Spent | INR 28,994.36 | **INR 31,099.61** |
| Calls placed | 399 | **437** |
| Cost per call placed | INR 51.08 | **INR 51.46** |
| Cost per 20-second call | INR 203.83 | **INR 214.17** |
| Lasted 20s | 100 (25%) | **105 (24%)** |
| Lasted 60s | 46 | **47** |

**The two closing days bought calls at a normal price but almost none of them
lasted.** 29-30 Sep took INR 2,100.72 for 38 calls - INR 55.28 each, in the usual
band - but only **5** held twenty seconds and only **1** held sixty. That is
INR 420.14 per 20-second call across those two days against INR 203.87 for the 4-28
window, and it is the whole reason the headline 20-second cost rose INR 10.34.
Call volume is not the problem; call quality on those two days is.

**Meta revised the earlier days up by INR 4.53** after the last publication
(4-28 Sep now reads INR 28,998.89 against the published INR 28,994.36). No call
count moved, and the published 4-28 rates reproduce to the paisa: INR 51.10 per
call and INR 203.87 per 20-second call.

### Per-campaign, 4-30 September

| Campaign | Spent | Calls | Per call | 20s | Per 20s | Days live |
|---|---|---|---|---|---|---|
| Pain Management | INR 12,900.47 | 222 | INR 58.11 | 61 | INR 211.48 | 21 |
| Lipoma Removal | INR 3,493.24 | 102 | **INR 34.25** | 21 | **INR 166.34** | 9 |
| Endoscopy 6 km | INR 3,460.95 | 66 | INR 52.44 | 12 | INR 288.41 | 5 |
| Autism | INR 2,131.13 | 42 | INR 50.74 | 10 | INR 213.11 | 6 |
| Kukatpally Clean v2 | INR 502.22 | 5 | INR 100.44 | 1 | INR 502.22 | 1 |
| NRI Elder Care (website) | INR 2,686.81 | - | - | - | - | 4 |
| NRI + Bengaluru (WhatsApp) | INR 5,924.79 | - | - | - | - | 11 |

**Only Pain Management is still ACTIVE at Meta** - `LIVE` is now `new Set([4])`.
Lipoma Removal was ACTIVE at the last snapshot and is now PAUSED, so the "live"
tag has moved off it. Everything else on the account is paused.

**Lipoma Removal closes as the cheapest line on both measures** - INR 34.25 a call
and INR 166.34 per 20-second call, against INR 56.70 and INR 226.13 for the call
campaigns excluding it. It is still holding the account average down on its own:
keep both rows in front of the client.

Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so
both sit outside every per-call figure. Call-campaign spend for the month is
INR 22,488.01 of the INR 31,099.61 total.

**WhatsApp stays paused and has not moved** at INR 5,924.79 for **27
conversations**, INR 219.44 each (re-pulled this refresh: `results` indicator
`onsite_conversion.messaging_conversation_started_7d` = 27; 27 first replies, 13
conversations past one message, 5 past three). None of that is on the page - the
`DAILY` row format has no field for messaging depth.

**18 September was a near-total stop** - the whole account spent INR 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal afterwards.

## October 2026 delivery exists and is deliberately NOT on this page

The account did not stop at the end of September. It was dark 3-5 Oct, then ran
**6-24 October** and has spent nothing on the 25th or 26th. This report's scope is
September only, so none of that is included and no October figure appears anywhere
on the page.

**This is a scope decision, not a data gap, and it needs a human call.** If the
client wants October, the clean way is a month tab bar like `halcyon-reports` has,
not an extension of the September arrays - the page has no tab mechanism today and
every headline on it is labelled "September 2026".

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` is the last complete day, which is what the Yesterday card
reads. Both are plain constants — move them together on every refresh, or the card
will silently show a stale day.

**When the reported month has closed, set `SNAP_DAY = null`.** It is only ever a
filter (`R.filter(r => r[1] !== SNAP_DAY)`) and a tag, so `null` correctly filters
nothing and tags nothing, and every day counts toward the headline. Leaving it
pointing at the last real day would drop a fully settled day out of every total;
pointing it at a date outside the data would leave the card claiming a day that is
not there is "still counting". With `SNAP_DAY` null the card retitles itself
"Last day of the month" and says September is complete.

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
  On this refresh that caught INR 4.53 of upward revision across 4-28 Sep.
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
