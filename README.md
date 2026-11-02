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

Frozen **2 Nov 2026, 8:20 am IST**. **September is now closed and fully settled** —
the page covers **4–30 Sep**, every day of it, and nothing is excluded. The 29th and
30th have landed; `SNAP_DAY` is empty for the first time (see *GST and dates*).
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The two days that were missing turned out to be ordinary days, not the collapse the
part-day suggested.** The 29th was published as a Rs 71.22 part-day with 3 calls; it
settled at **Rs 1,056.20 for 20 calls (Rs 52.81)**. The 30th is new at **Rs 1,044.52 for
18 calls (Rs 58.03)**. Meta also revised the 28th up by Rs 4.53 (Autism +Rs 0.74,
Pain +Rs 0.77, Lipoma +Rs 3.02) with call counts unchanged.

| last four days | spend | calls | each | 20s |
|---|---|---|---|---|
| 27 Sep | Rs 1,811.95 | 41 | Rs 44.19 | 11 |
| 28 Sep | Rs 1,563.50 | 32 | Rs 48.86 | 8 |
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

**The month closed thinning out.** Only Pain Management and Lipoma ran on the 29th and
30th, and the daily call rate drifted from Rs 44.19 to Rs 58.03 across the last four days.
Read that as the mix changing, not a price move: Autism and Endoscopy — both cheaper lines
— had already stopped, so the average fell back towards Pain Management's own rate.

**Only Pain Management is still ACTIVE at Meta** (`LIVE = new Set([4])`). **Lipoma is now
PAUSED**, having closed as the cheapest line on the account: **Rs 3,493.24 for 102 calls,
Rs 34.25 each**, against Rs 56.70 for everything else. Autism closed at Rs 2,131.13 for
42 calls (Rs 50.74) and Endoscopy at Rs 3,460.95 for 66 calls (Rs 52.44) — the latter
unchanged from the previous cut, since it never spent again.

**Pain Management carried the month**: Rs 12,900.47 over 21 days, 222 calls at Rs 58.11,
the dearest of the call lines — but 61 of them held twenty seconds (27%) at Rs 211.48, and
32 held a minute. It is the only line still running.

| | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|
| Cost per call placed | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| …excluding Lipoma | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| …excluding Lipoma | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

The final month lands inside the Rs 49–53 band the per-call rate held across every
refresh — **read it as flat**. The 20-second rate finished Rs 10.34 above the 4–28 cut
because the last two days bought 38 calls but only 5 that held twenty seconds. Keep both
rows in front of the client. Per-call figures cover **call campaigns only**: NRI Elder
Care drives website traffic (Rs 2,686.81) and the NRI + Bengaluru campaign optimised for
WhatsApp conversations (Rs 5,924.79), so both sit outside every per-call figure.

**WhatsApp stays paused and unchanged** at Rs 5,924.79 for **27 conversations**,
Rs 219.44 each — identical to the previous cut, so the messaging-depth figures below were
not re-pulled. Meta reported 27 first replies, 13 conversations past one message, 5 past
three, 3 past five, and every one of the deep ones is the Gulf ad set. Bengaluru buys a
conversation for Rs 160.80 against Gulf's Rs 273.88. None of that is on the page: the
`DAILY` row format has no field for messaging depth.

**18 September was a near-total stop** — the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has explained it
yet; delivery was normal for the rest of the month.

## October 2026 is out of scope, and it is not empty

This account spent **Rs 18,476.76 on 283,130 impressions in October 2026**, none of which
appears on this page. **Scope is September only** by design — both this README and the
refresh brief say so — so October was deliberately not pulled or published. If the client
expects an October view, that is a **new month tab or a new page**, not an edit to this
one. `halcyon-reports` is the worked example of how to add a month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still accruing**, and
`YDAY` the last complete day, which is what the Yesterday card reads. Both are plain
constants — move them together on every refresh, or the card will silently show a stale day.

**September has closed, so `SNAP_DAY` is now the empty string and `YDAY` is `2026-09-30`.**
Every day 4–30 Sep is settled, so quarantining one of them would have dropped a real day out
of the headline — the opposite of what the guard is for. The page handles an empty `SNAP_DAY`
on its own: no row is excluded, no "so far" tag is printed, the card titles itself *Last day
of the month*, and it says September is closed instead of claiming a day is still counting.
**Set `SNAP_DAY` back to the live date the moment this page covers a month in progress.**

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and is back
  to one member (`{4}`, Pain Management) now that Lipoma is paused too. Keep it in step
  with the statuses or the "live" tag lies.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer,
  and the baked-figures comment above `CAMPS` — four places) and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
