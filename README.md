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

Frozen **18 Nov 2026, 11:00 am IST**, covering **4–30 Sep — the whole month, now
closed and fully settled**. There is no part-day left to exclude, so `SNAP_DAY` is
`null` and all 26 delivery days count towards every headline.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The month closed on two campaigns and a mild drift upward.** The previous cut
(4–28 Sep, published 29 Sep) read Rs 28,994.36 for 399 calls at Rs 51.08. Adding the
two settled days the old snapshot could not see — 29 Sep (Rs 1,056.20, 20 calls) and
30 Sep (Rs 1,044.52, 18 calls) — plus Meta's own revisions to 28 Sep, takes the month
to Rs 31,099.61 and 437 calls. Cost per call moved Rs 51.08 -> **Rs 51.46**; the
20-second call Rs 203.83 -> **Rs 214.17**, its dearest reading of any cut.

| | 4–22 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| …excluding Lipoma | Rs 51.55 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| …excluding Lipoma | Rs 187.72 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49–53 —
read it as flat. Keep both rows in front of the client: Lipoma is still holding the
average down on its own, and excluding it the account sits at Rs 56.70 a call.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website traffic
and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit
outside every per-call figure.

**Lipoma finished as the cheapest line on the account, by a wide margin.**
Rs 3,493.24 for **102 calls at Rs 34.25**, against Rs 56.70 for every other call
campaign. It ran its last nine days 22–30 Sep and is now PAUSED. Only 21 of its 102
calls held twenty seconds (21%), below Autism (24%) and Pain Management (27%) though
above Endoscopy (18%), so it buys cheap calls rather than notably long ones — but at
Rs 166.35 per 20-second call it is still the best rate on the account.

**Pain Management is the only campaign Meta still reports ACTIVE**, and it closed
September at Rs 12,900.47 for 222 calls (Rs 58.11), 61 of them over twenty seconds
(27%) at Rs 211.48 each — the highest share of calls that last, as it was at the
previous cut.

**Autism, Endoscopy and Kukatpally all closed paused.** Autism Rs 2,131.13 / 42 calls
/ Rs 50.74. Endoscopy Rs 3,460.95 / 66 calls / Rs 52.44, but only 12 held twenty
seconds — **Rs 288.41 per real conversation**, the dearest of the call campaigns bar
the one-day Kukatpally test (Rs 100.44 a call on a single day).

**18 September was a near-total stop** — the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has explained
it; delivery was normal on either side of it.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each —
unchanged from the previous cut, so the depth figures below still stand. Meta also
reports how far each went: 27 first replies, 13 conversations past one message, 5 past
three, 3 past five — and every one of the deep ones is the Gulf ad set. Bengaluru buys
a conversation for Rs 160.80 against Gulf's Rs 273.88. None of that is on the page
yet; the `DAILY` row format has no field for messaging depth.

> ### The account kept running after September, and this page does not show it
>
> **Scope is still September only, so October is entirely absent from the report.**
> For the record, the account spent a further **Rs 18,476.76 across 1–24 October**
> (21 days with delivery) and has then been **completely dark from 25 October to
> 18 November — 25 days, Rs 0.00, no impressions**. Pain Management still reads
> ACTIVE while spending nothing, which is the same shape as a billing or
> spend-limit stop rather than a paused campaign.
>
> Extending the report to October needs a page change, not just a data refresh —
> this file has no month tabs, unlike `halcyon-reports`. That is a call for a human:
> either add tabs, or tell the client plainly that the September report is a closed
> historical cut.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` is the day the Yesterday card reads. Both are plain constants — move them
together on every refresh, or the card will silently show a stale day.

**When the month is closed, set `SNAP_DAY = null`.** Nothing is then excluded and every
settled day counts, which is right: the exclusion exists only because Meta revises the
last ~48h, and a month seven weeks old has no unsettled day in it. Leaving the last day
in `SNAP_DAY` would silently drop a real day from every headline. The Yesterday card
switches its sub-line to say the month is complete when `SNAP_DAY` is null.

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
- **Fetch by `object_ids`, not by listing campaigns — and always reconcile.** On the
  18 Nov pull, a plain `level: "campaign"` listing for the month returned all 7
  campaigns x 30 days = **exactly 210 rows, over the 200-row cap**, and silently
  returned **zeros for every Lipoma day** while still emitting the rows. Nothing
  errored. The campaign sums came out Rs 3,493.24 short of the account's own daily
  totals, and the per-day gaps matched the published Lipoma figures exactly. Re-fetching
  that one id with `object_ids` returned the real numbers. Split the ids so each call
  stays well under 200 campaign-days, and check every id came back with plausible
  figures — a campaign present with zeros is the failure mode, not a campaign missing.
- **Always reconcile before publishing.** Pull `level: "ad_account"` with
  `time_increment: "1"` for the same range and assert the campaign sums equal the
  account's own daily spend *and* impressions on every day. On the 18 Nov pull both
  matched to the paisa on all 26 delivery days once Lipoma was refetched — that check is
  the only reason the zeroed campaign was caught.
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
