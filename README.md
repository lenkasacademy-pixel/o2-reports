# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery, through 30 Sep — the month is complete).

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

Frozen **27 Oct 2026, 8:11 am IST**, covering the **complete month, 4-30 September**.
September has been closed for four weeks, so every day on the page is fully settled
and `SNAP_DAY` is `null` - nothing is held out of the headline (see *GST and dates*).
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The month closed with two campaigns and finished quietly.** The 29th and 30th
were the last two days of delivery:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

**The 29th is the clearest part-day lesson yet.** The previous cut published it as
a Rs 71.22 part-day with 3 calls; it settled at **Rs 1,056.20 with 20 calls** - just
under fifteen times the spend. The 28th also moved up Rs 4.53 after publication
(Autism +Rs 0.74, Pain +Rs 0.77, Lipoma +Rs 3.02; call counts unchanged). Nothing
on this page is a part-day any more, which is why the totals can finally cover
the whole month.

**Lipoma is now PAUSED, so only Pain Management is live.** `LIVE` is down to
`{4}`. Lipoma closes as **the cheapest line on the account by a wide margin**:
Rs 3,493.24 for **102 calls at Rs 34.25**, against Rs 56.70 for everything else.
It held its lead every single day it ran.

Final per-campaign closes (ex-GST, call campaigns):

| Campaign | spend | calls | each | 20s | per 20s | status |
|---|---|---|---|---|---|---|
| Pain Management | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 | ACTIVE |
| Lipoma Removal | Rs 3,493.24 | 102 | Rs 34.25 | 21 | Rs 166.34 | PAUSED |
| Endoscopy | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 | PAUSED |
| Autism | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 | PAUSED |
| Kukatpally (one-day test) | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 | PAUSED |

**Autism stopped on the 28th** at Rs 2,131.13 for 42 calls (Rs 50.74). Its last day
was its second-cheapest. **Endoscopy stopped on the 27th** at Rs 3,460.95 for 66
calls, only 12 of which held twenty seconds - **Rs 288.41 per real conversation**,
the dearest of the call campaigns bar the one-day Kukatpally test.

**Pain Management ran the whole month and is the only line still on.** It took 60%
of the call budget and has the highest share of calls that last: 61 of its 222
(27%) held twenty seconds at Rs 211.48 each, and 32 held a minute.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each -
unchanged from the previous cut, so the messaging-depth figures below still stand.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five - and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for Rs 160.80 against Gulf's Rs 273.88. None
of that is on the page yet; the `DAILY` row format has no field for messaging depth.

**Read the headline carefully - Lipoma is still the whole improvement:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 51.03 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 53.24 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 184.36 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 191.08 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49-53;
read it as flat, and the final month figure of Rs 51.46 sits mid-range. **The
20-second rate is the one that moved**: Rs 203.83 to Rs 214.17 in two days, because
the last two days bought Rs 2,100 of calls but only 5 more that held twenty
seconds. Keep both rows in front of the client. Per-call figures cover **call
campaigns only**: NRI Elder Care drives website traffic and the NRI + Bengaluru
campaign optimised for WhatsApp conversations, so both sit outside every per-call
figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

**October is out of scope and is not on the page.** The account has spent
**Rs 18,476.76 across 1-27 October** (283,130 impressions) on Pain Management,
which is still ACTIVE. This report is September-only by design, so none of that
appears here. If the client wants October, it needs a second month - and since
this page has no month tab bar (unlike `halcyon-reports`), that is a page change,
not a refresh. **Flag it rather than silently widening the scope.**

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` the last complete day, which is what the Yesterday card
reads. Both are plain constants — move them together on every refresh, or the
card will silently show a stale day.

**Set `SNAP_DAY = null` once the month has closed and every day is settled**, as
it is now. The page filters on `r[1] !== SNAP_DAY`, so a non-null value silently
drops that day from every headline — correct for an unsettled day, wrong for a
settled one. With `null` nothing is excluded and the totals cover the whole
month; the Yesterday card says so instead of naming a day that is still counting.

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
