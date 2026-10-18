# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 1-3 and 7 Sep had no delivery at all).

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

Frozen **18 Oct 2026, 8:45 am IST**, covering **4-30 September** - the month is now
complete, so for the first time there is **no part-day in the data**. `SNAP_DAY` is
therefore the empty string (nothing is excluded) and `YDAY` is 30 Sep.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s, 47 lasted 60s. **Rs 51.46 per call placed** and
**Rs 214.17 per call that actually held 20 seconds**.

**September closed with two campaigns and finished on its dearest call of the month.**
The 29th settled at Rs 1,056.20 for 20 calls (Rs 52.81) and the 30th at Rs 1,044.52 for
18 calls (Rs 58.03). On the 30th **Pain Management produced no 20-second call at all** -
Rs 587.29 for 5 calls, Rs 117.46 each, its worst day in the month by a wide margin -
while Lipoma took Rs 457.23 for 13 calls at Rs 35.17. One bad day on one campaign; not a
trend, but it is what moved the headline.

**Only Pain Management is still ACTIVE.** Lipoma Removal now reads PAUSED, so `LIVE` is
down to the single index 4. Final per-campaign September figures:

| Campaign | Days | Spend | Calls | Each | 20s+ | 60s+ |
|---|---|---|---|---|---|---|
| Pain Management | 21 | Rs 12,900.47 | 222 | Rs 58.11 | 61 | 32 |
| WhatsApp (msg) | 11 | Rs 5,924.79 | - | - | - | - |
| Lipoma Removal | 9 | Rs 3,493.24 | 102 | **Rs 34.25** | 21 | 6 |
| Endoscopy | 5 | Rs 3,460.95 | 66 | Rs 52.44 | 12 | 4 |
| NRI Elder Care (web) | 4 | Rs 2,686.81 | - | - | - | - |
| Autism | 6 | Rs 2,131.13 | 42 | Rs 50.74 | 10 | 4 |
| Kukatpally | 1 | Rs 502.22 | 5 | Rs 100.44 | 1 | 1 |

**Lipoma stayed the cheapest line to the end** - Rs 34.25 a call against Rs 56.70 for
everything else - and it is now paused. That is the single biggest thing to put to the
client: the account's cheapest source of calls has been switched off.

**Revisions since the 29 Sep cut.** Meta settled 28 Sep up by Rs 4.53 (Autism +0.74,
Pain +0.77, Lipoma +3.02; no call counts moved), and the 29th went from a Rs 71.22
part-day to Rs 1,056.20 settled - a reminder of why the part-day never sets a headline.

| | 4-26 | 4-27 | 4-28 | **4-30 (final)** |
|---|---|---|---|---|
| Cost per call placed | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |

Across every refresh the per-call rate has stayed inside Rs 49-53; read it as flat. The
20-second rate finished Rs 10 worse than the 4-28 cut because the last two days added
Rs 2,100 of spend and only 5 qualifying calls. Keep both rows in front of the client.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website traffic and
the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit outside
every per-call figure.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each. Meta
also reports how far each went: 27 first replies, 13 conversations past one message, 5
past three, 3 past five - and every one of the deep ones is the Gulf ad set. Bengaluru
buys a conversation for Rs 160.80 against Gulf's Rs 273.88.

> **Trap, new on this refresh: the WhatsApp campaign now returns per-day counts in
> `results`.** Earlier pulls gave "Not available" per day; it now reports 1, 2, 1, 4, 8,
> 5, 5 conversations on 13-21 Sep. Those are **messaging conversations, not phone calls**,
> and `DAILY`'s `placed` column is phone calls only. Writing them in would have added 26
> phantom calls and dropped the headline from Rs 51.46 to about Rs 48 a call. The builder
> now forces `placed`/`20s`/`60s`/`tapped` to 0 for any campaign whose `type` is `web` or
> `msg`, and asserts it. Conversation counts stay in this README alone.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions. Kept here because nobody has explained it yet.

## October 2026 is outside this report

**The account restarted and has spent Rs 14,396.18 between 1 and 17 October** - almost
half of September's total - on days 1-2 and 6-17 (3-5 Oct were dark). None of it is in
this report, because the scope is September only. **Someone needs to decide whether this
report gains an October tab or a second file**; until then the live page describes a month
that ended three weeks ago. Deliberately not added in this refresh: changing the scope is
not a data refresh.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**, and
`YDAY` the last complete day, which is what the Yesterday card reads. Both are plain
constants — move them together on every refresh, or the card will silently show a stale
day. Now that September is closed there is no part-day, so `SNAP_DAY` is `""`: the totals
filter then excludes nothing, no row gets the "so far" tag, and the Yesterday card says
September is settled instead of naming a day that is still counting.

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
