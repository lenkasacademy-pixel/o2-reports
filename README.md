# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).
The month is now **complete and fully settled**: 4-30 Sep, 27 days, no part-day.

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

Frozen **28 Nov 2026, 8:25 am IST**, covering **4-30 September - the whole month,
every day settled**. Nothing on this page is still moving, so for the first time
there is no part-day to hold out of the headlines.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The two days the last cut could not see cost more and converted less.** The 29th
settled at ₹1,056.20 for 20 calls (₹52.81) and the 30th at ₹1,044.52 for 18
calls (₹58.03) - and between them they bought only **5** twenty-second calls on
₹2,100.72 of call spend. That is what moved the duration headline:

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| ...excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| ...excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Read it the way the earlier cuts were read: **the per-call rate is flat** - every
refresh recorded here sits inside ₹49-53, and the closed month lands at ₹51.46,
mid-range. **The 20-second rate is not flat.** It has gone from ₹181.34 at its
best (4-24) to ₹214.17 for the full month, an 18% rise, and the last two days are
the sharpest part of it. The calls kept coming at the same price; fewer of them
held.

**Revisions since the 29 Sep cut.** The 28th was published at ₹1,558.97 and
settled at ₹1,563.50 (+₹4.53, call counts unchanged). The 29th was published as
a part-day at ₹71.22 for 3 calls and settled at **₹1,056.20 for 20 calls** -
fifteen times the spend. This is exactly why the part-day is held out of the
headlines, and it is the clearest example of it in this report's history.

| Campaign | Days | Spend | Placed | Each | 20s | Per 20s | 60s | Status |
|---|---|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 32 | **ACTIVE** |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | **₹34.25** | 21 | **₹166.34** | 6 | PAUSED |
| Endoscopy | 5 | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 4 | PAUSED |
| Autism | 6 | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 4 | PAUSED |
| Kukatpally (one-day test) | 1 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 1 | PAUSED |
| NRI Elder Care (website) | 4 | ₹2,686.81 | - | - | - | - | - | PAUSED |
| NRI + Bengaluru (WhatsApp) | 11 | ₹5,924.79 | - | - | - | - | - | PAUSED |

**Pain Management is the only campaign still ACTIVE at Meta**, and it carried the
month on its own from the 23rd: 21 days, ₹12,900.47, 222 calls. But it is the
dearest call line bar the one-day Kukatpally test (₹58.11) and its duration rate
slipped with the month - 60 of 208 calls held twenty seconds at the 28 Sep cut
(₹194.05), now **61 of 222 at ₹211.48**. It added 14 calls over the last two
days and just one of them lasted.

**Lipoma closes as the cheapest line on the account by a wide margin** - 102 calls
at **₹34.25** against ₹56.70 for everything else, and the cheapest twenty-second
call too at ₹166.34. It is now PAUSED. It is still holding the account average
down single-handedly: keep both rows of the table above in front of the client.

**Autism closes at ₹2,131.13 for 42 calls, ₹50.74 each** - respectable, and
cheaper per placed call than Pain Management. It spent nothing after the 28th.

**Endoscopy is unchanged from the last cut** at ₹3,460.95 for 66 calls, 12 of
which held twenty seconds - **₹288.41 per real conversation**, the dearest of the
call campaigns bar Kukatpally. It stopped on the 27th and the figures never moved
again, which is the clearest sign a campaign is genuinely finished.

Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so
both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal on either side of it and for the rest of
the month.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each -
re-pulled on this refresh and **unchanged to the paisa**, which is expected since
the campaign stopped on 22 Sep. By ad set: Bengaluru buys a conversation for
**₹160.80** (13 on ₹2,090.41) against Gulf's **₹273.88** (14 on ₹3,834.38).
Meta also now reports 29 total messaging connections against those 27 conversations.
The messaging-depth breakdown quoted in earlier cuts (27 first replies, 13 past one
message, 5 past three, 3 past five, all the deep ones on the Gulf ad set)
**could not be re-pulled**: `messaging_first_reply` and the
`messaging_user_depth_*` fields are no longer offered by the connector at campaign
or ad-set level. Those figures are from the 29 Sep pull; treat them as of that date.
None of it is on the page - the `DAILY` row format has no field for messaging depth.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still counting**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently
show a stale day.

**September is closed, so `SNAP_DAY` is now the empty string** and nothing is
excluded from the totals: all 27 days are settled. The filter and the `CLOSED` flag
beside it stay in the code, so the part-day guard starts working again the moment a
live day is added. With `CLOSED` set the card titles itself *Last day of the month*
rather than *Yesterday* — a September report read in November cannot call the 30th
"yesterday" — and `YDAY` is `2026-09-30`.

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
  in step with the statuses or the "live" tag lies. It is now `{4}` alone — Lipoma
  was paused after the month ended, so it dropped out. Note these statuses are read
  **at refresh time**, not as at 30 September: in a closed-month report the tag says
  "still running today", which is the useful reading of it.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
