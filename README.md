# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep is the first day with delivery).
As at 23 Nov 2026 the month is **complete and fully settled** - there is no part-day in the
data any more, so `SNAP_DAY` is `""` and nothing is excluded from the headline totals.

> **The account kept running after September and this report does not cover it.**
> October 2026 took **Rs 18,476.76** on 2,83,130 impressions; November is Rs 0.00 to date.
> That October spend is outside the declared scope and is deliberately not in the page. If the
> client should see it, the month needs its own report (or this one needs month tabs like
> `halcyon-reports`) - that is a scope decision, not a refresh.

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

Frozen **23 Nov 2026, 8:25 am IST**, covering **4-30 September, every day settled**.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s (24%) - 47 lasted 60s (11%). Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds** (Rs 478.47 per minute-long call).

September closed with only **Pain Management** still ACTIVE; everything else is PAUSED, so
`LIVE` is now `new Set([4])`.

| Campaign | Days | Spend | Calls | Each | 20s | Per 20s | 60s |
|---|---|---|---|---|---|---|---|
| Pain Management | 21 | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 | 32 |
| Lipoma Removal | 9 | Rs 3,493.24 | 102 | **Rs 34.25** | 21 | **Rs 166.34** | 6 |
| Endoscopy | 5 | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 | 4 |
| Autism | 6 | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 | 4 |
| Kukatpally (one-day test) | 1 | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 | 1 |
| NRI Elder Care (website) | 4 | Rs 2,686.81 | - | - | - | - | - |
| NRI + Bengaluru WhatsApp | 11 | Rs 5,924.79 | - | - | - | - | - |

**The last two days of the month, which the previous cut never saw.** 29 Sep was a part-day at
Rs 71.22 for 3 calls when it was published; it settled at **Rs 1,056.20 for 20 calls (Rs 52.81
each)** - Pain Rs 669.68 for 9, Lipoma Rs 386.52 for 11. 30 Sep is new: **Rs 1,044.52 for 18
calls (Rs 58.03 each)** - Pain Rs 587.29 for 5 (Rs 117.46 each, its worst day) and Lipoma
Rs 457.23 for 13 (Rs 35.17). Only those two campaigns ran to the end of the month.

**28 Sep was revised up by Rs 4.53** after publication (Pain +Rs 0.77, Autism +Rs 0.74,
Lipoma +Rs 3.02); the call counts did not move. Everything from 4 to 27 Sep is unchanged from
what was published.

**Lipoma stayed the cheapest line to the end and is the reason the blended rate looks flat.**
Over the full month it took Rs 3,493.24 for **102 calls at Rs 34.25**, against Rs 56.70 for
every other call campaign, and its 20-second call is Rs 166.34 against Rs 226.13 for the rest.
It is now PAUSED.

**Autism closed cheap.** Rs 2,131.13 for 42 calls at Rs 50.74 - level with Endoscopy on placed
calls and better than Pain Management - but only 10 of those held twenty seconds. It last spent
on 28 Sep and is PAUSED.

**Pain Management is the line that lasts.** 61 of its 222 calls (27%) held twenty seconds and
32 reached a minute - 68% of the month's 60-second calls on 57% of the call budget. It is the
dearest per placed call (Rs 58.11) and the only campaign still ACTIVE.

**Endoscopy closes unchanged** at Rs 3,460.95 for 66 calls (Rs 52.44 each), only 12 of which
held twenty seconds - **Rs 288.41 per real conversation**, the dearest of the call campaigns
bar the one-day Kukatpally test.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each - unchanged
from the previous cut. Re-pulled on 23 Nov: 27 first replies, 13 conversations past one message,
5 past three, and 29 total messaging connections. The `messaging_user_depth_5` key is no longer
returned for this campaign, so the "3 past five" figure from the previous cut cannot be
re-derived; treat it as unverified rather than changed. None of this is on the page - the
`DAILY` row format has no field for messaging depth.

**NRI Elder Care still has nothing to show for Rs 2,686.81.** Its own goal, the `HEnquiry`
website event, reports no conversions at all on 39 link clicks. The page carries this as a
warning card and works it out from the data, so it needs no hand-written note.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day, 122
impressions. Still unexplained; delivery was normal either side of it.

**Read the headline carefully - Lipoma is holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 51.03 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 53.24 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 184.36 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 191.08 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every cut recorded here the per-call rate has stayed inside Rs 49-53 and finished at
Rs 51.46 - read it as flat. The 20-second rate is the one that moved: Rs 203.83 at the 28th
against **Rs 214.17** for the full month, because the last two days bought 38 calls but only
5 that held. Keep both rows in front of the client. Per-call figures cover **call campaigns
only**: NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised for
WhatsApp conversations, so both sit outside every per-call figure.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the part-day, if there is one, and `YDAY` is the day the card reads. Both are
plain constants — move them together on every refresh, or the card will silently show a stale
day. **Now that September is closed there is no part-day**, so `SNAP_DAY` is the empty string:
it matches no row, nothing is excluded from the totals, and the card's right-hand line says the
month is settled instead of naming a day that is still counting. `YDAY` is `2026-09-30` and the
card is titled **Last day**, not "Yesterday" — the report is frozen two months after the month
it covers, so "yesterday" would have been wrong on its face. If this report is ever pointed at a
live month again, set `SNAP_DAY` back to that part-day and the card re-labels itself.

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
