# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month
is now **complete and fully settled** - 4-30 Sep, no part-day.

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

Frozen **19 Oct 2026, 8:15 am IST**, covering **4-30 Sep - the complete month**.
September has closed, so unlike every previous cut there is **no part-day in this
window**: `SNAP_DAY` is `null` and every day here is settled.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The month closed on two quiet, Pain-and-Lipoma-only days.** The 29th took
Rs 1,056.20 for 20 calls and the 30th Rs 1,044.52 for 18 - both well under the
month's Rs 1,152 daily average, and between them they produced only **5 calls that
held twenty seconds out of 38**. That is what moved the headline: cost per call
drifted up gently (Rs 51.08 -> Rs 51.46) but **cost per 20-second call jumped
Rs 203.83 -> Rs 214.17**, the largest single-refresh move in that number recorded
here. Two thin days are not a trend, but this is the number to watch next month.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | Rs 587.29 | 5 | Rs 117.46 | 0 |
| Lipoma | Rs 457.23 | 13 | Rs 35.17 | 2 |

**Only Pain Management is still ACTIVE.** Lipoma Removal has since been paused at
Meta (it was live at the last cut), so `LIVE` is down to the single index `{4}`.
Lipoma closes September as **by far the cheapest line - Rs 3,493.24 for 102 calls at
Rs 34.25**, against Rs 56.70 for every other call campaign combined, and it holds
that lead on duration too (Rs 166.34 per 20-second call, the best on the account).

**Pain Management is the account.** Rs 12,900.47 of the Rs 22,488.01 call budget,
222 of the 437 calls, at Rs 58.11 each - dearer than average per call placed but
strong on depth: 61 of its calls held twenty seconds (27%) at Rs 211.48, and 32
held a full minute at Rs 403.14, the best 60-second rate of any campaign.

**Meta revised 4-28 Sep up by Rs 4.53 after the last publication** (Rs 28,994.36 ->
Rs 28,998.89); no call counts moved. The 4-28 cut still reproduces exactly 399 calls,
100 at 20s and 46 at 60s, which is the check that this refresh is continuous with
the published one.

**Per-campaign close for the month:**

| Campaign | spend | calls | per call | 20s | per 20s |
|---|---|---|---|---|---|
| Pain Management | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 |
| Lipoma Removal | Rs 3,493.24 | 102 | Rs 34.25 | 21 | Rs 166.34 |
| Endoscopy | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 |
| Autism | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 |
| Kukatpally (one-day test) | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 |

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each -
unchanged, it has not spent since 22 Sep. Meta also reports how far each went: 27
first replies, 13 conversations past one message, 5 past three, 3 past five - and
every one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for
Rs 160.80 against Gulf's Rs 273.88. None of that is on the page yet; the `DAILY` row
format has no field for messaging depth.

**Read the headline carefully - the whole improvement is Lipoma:**

| | 4-22 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49-53 and
it still does at Rs 51.46 - read it as flat. Lipoma is holding the average down on
its own; excluding it the account sits at Rs 56.70 a call. Keep both rows in front
of the client. Per-call figures cover **call campaigns only**: NRI Elder Care drives
website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day and `YDAY` the last complete day, which is what the
Yesterday card reads. Both are plain constants - move them together on every
refresh, or the card will silently show a stale day. **`SNAP_DAY` is `null` when the
window contains no part-day**, as it does now that September has closed: setting it
to 30 Sep instead would wrongly strike a fully settled day out of every headline and
label it "so far". The Yesterday card adapts its sub-line to whichever case applies.

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
