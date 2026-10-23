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
- A **Final day** card (the last day in the data) with that day's billed amount,
  calls, 20s calls and cost per call, broken out by campaign. While a month is
  still running it is headed *Yesterday* and names the part-day it excludes;
  with September closed it is headed *Final day* and says the month is settled.

## Snapshot

Frozen **23 Oct 2026, 11:10 am IST**, covering **4-30 September — the month is
now closed**. Every day in the report is settled; there is no part-day left to
exclude, so `SNAP_DAY` is empty and all 26 delivering days count toward the
headline.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**September is over and only Pain Management is still running.** Lipoma Removal
spent its last rupee on 30 Sep and now reads PAUSED, so `LIVE` is down to a
single campaign. Autism, Endoscopy, Kukatpally, NRI Elder Care and the WhatsApp
campaign are all PAUSED.

**The two days the last cut could not see.** 29 Sep was published as a part-day
at Rs 71.22; it settled at **Rs 1,056.20 for 20 calls (Rs 52.81 each)**. 30 Sep
closed the month at **Rs 1,044.52 for 18 calls (Rs 58.03 each)**. Both days were
Pain Management and Lipoma only.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep - Pain Management | Rs 669.68 | 9 | Rs 74.41 | 1 |
| 29 Sep - Lipoma | Rs 386.52 | 11 | Rs 35.14 | 2 |
| 30 Sep - Pain Management | Rs 587.29 | 5 | Rs 117.46 | 0 |
| 30 Sep - Lipoma | Rs 457.23 | 13 | Rs 35.17 | 2 |

**Pain Management ran dear into month-end and Lipoma did not.** Pain's daily
rate went Rs 63.18 (28th) -> Rs 74.41 (29th) -> **Rs 117.46 (30th)**, its worst
day of the month, on falling volume (11 -> 9 -> 5 calls). Lipoma held at
Rs 35.14 and Rs 35.17 over the same two days. The month-end divergence is the
thing to look at before Pain Management is topped up again.

**Lipoma finished cheapest by a wide margin.** Rs 3,493.24 for **102 calls at
Rs 34.25**, against Rs 56.70 for every other call campaign put together. It ran
nine days, 22-30 Sep.

**Final per-campaign standings (call campaigns, ex-GST):**

| Campaign | spend | calls | per call | 20s | per 20s |
|---|---|---|---|---|---|
| Pain Management | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 |
| Lipoma Removal | Rs 3,493.24 | 102 | **Rs 34.25** | 21 | Rs 166.34 |
| Endoscopy | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 |
| Autism | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 |
| Kukatpally (one day) | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 |

**Small revisions this refresh.** Meta settled 28 Sep up by Rs 4.53 in total
(Pain +Rs 0.77, Lipoma +Rs 3.02, Autism +Rs 0.74); no call counts moved. Autism's
28 Sep impressions also moved 10,180 -> 10,206 and its reach 9,051 -> 9,070.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44
each — unchanged since 22 Sep. Meta also reports how far each went: 27 first
replies, 13 conversations past one message, 5 past three, 3 past five — and
every one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for
Rs 160.80 against Gulf's Rs 273.88. None of that is on the page; the `DAILY` row
format has no field for messaging depth.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 51.03 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 53.24 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 184.36 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 191.08 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

The per-call rate closed at Rs 51.46, inside the Rs 49-53 band it held all
month — read it as flat. The 20-second rate is the one that moved: the last two
days bought 38 calls but only 3 of them held twenty seconds, which pushed the
month's figure from Rs 203.83 to Rs 214.17. Excluding Lipoma the account closes
at Rs 56.70 a call. Keep both rows in front of the client. Per-call figures
cover **call campaigns only**: NRI Elder Care drives website traffic and the NRI
+ Bengaluru campaign optimised for WhatsApp conversations, so both sit outside
every per-call figure.

**18 September was a near-total stop** — the whole account spent Rs 6.43 that
day, 122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it; delivery was normal after it.

**Reconciliation.** Campaign rows equal the account's own daily spend *and*
impressions on all 26 delivering days, to the paisa, and every campaign's daily
sums equal its September period total. Every 20s/60s division landed on a whole
number.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day to keep out of every total and `YDAY` the last
complete day, which is what the day card reads. Both are plain constants — move
them together on every refresh, or the card will silently show a stale day.

**September is closed, so `SNAP_DAY` is now `""`.** With no part-day inside the
scope there is nothing to exclude: the empty string matches no row, so every day
counts and the "so far" tag never renders. `YDAY` is `2026-09-30`. If this report
ever reopens on a running month, put the part-day back in `SNAP_DAY` and the card
reverts to its *Yesterday* wording on its own.

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
- Recent days keep settling for ~48h; re-pull the whole month rather than
  appending. The 4-30 Sep pull on 23 Oct still moved 28 Sep by Rs 4.53 against
  the 29 Sep cut, so re-pull even a month that looks long finished.
- `CAMPS` order must not be reshuffled; `DAILY[0]` indexes into it. **Append new
  campaigns to the end** — Lipoma Removal was added as index 6 on 23 Sep for
  exactly this reason.
- `LIVE` is a `Set` of campaign indexes still ACTIVE at Meta, not a single index.
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused. Keep it
  in step with the statuses or the "live" tag lies.
- Update the snapshot date in `index.html` — it appears **four times**: the title
  comment on line 8, the masthead stamp, the footer line and the baked-figures
  comment above `CAMPS` — and once here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
