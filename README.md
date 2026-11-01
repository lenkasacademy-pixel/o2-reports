# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month is
now closed and every day in it is fully settled.

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

Frozen **1 Nov 2026, 11:00 am IST**, covering **4-30 Sep - the complete month**.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September is complete.** The previous cut stopped at the 28th with the 29th as a live
part-day. Both remaining days have since settled:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

Only **Pain Management** and **Lipoma** ran those two days. The 29th was published as
₹71.22 for 3 calls while still counting; it settled fifteen times larger, which is
exactly why the part-day is kept out of every headline.

**`SNAP_DAY` is now `null`.** With the month closed there is no unsettled day left to
exclude, so the part-day guard has nothing to drop and all 26 delivery days are in the
totals. `YDAY` is 30 Sep and the Yesterday card relabels itself "Last day of the month".
The guard itself is unchanged - set `SNAP_DAY` back to a date the moment this report is
ever extended to a live month.

**Meta revised 28 Sep up by ₹4.53 after publication** (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02), with impressions and reach nudged up to match. No
call, 20s or 60s count moved on any previously published day.

**Both headline rates rose slightly on the full month**, because the last two days were
dearer than the month's average:

| | 4-22 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30** |
|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49-₹53 -
read it as flat for the whole month. The 20-second rate is the one that moved: it drifted
from ₹181 to ₹214 as Endoscopy and Autism closed out and Pain Management took a
larger share of a budget whose calls are longer but fewer.

**Lipoma closes as the cheapest line on the account**, and it held that for every day it
ran: ₹3,493.24 for **102 calls at ₹34.25**, against ₹56.70 for everything else.
It is now PAUSED. Keep both rows in front of the client - Lipoma on its own pulls the
account rate down by over five rupees a call.

**Pain Management is the only campaign still ACTIVE** (`LIVE` is now just index 4). It
closes September at ₹12,900.47 for 222 calls, ₹58.11 each, with 61 of them (27%)
holding twenty seconds at ₹211.48.

**Endoscopy and Autism both closed out on schedule** and neither moved after pausing -
Endoscopy final at ₹3,460.95 for 66 calls (₹52.44), only 12 past twenty seconds
(₹288.41 each); Autism at ₹2,131.13 for 42 calls (₹50.74), 10 past twenty
seconds.

**18 September was a near-total stop** - the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has explained it
yet; delivery was normal either side of it.

**Outside this report's scope, but worth knowing:** the account kept running into
October (₹989.84 on 1 Oct, a three-day gap, then ₹177-₹1,814 a day through
24 Oct) and has spent **nothing since 25 October** - seven dark days as of this snapshot.
This page is September-only by design and says nothing about that. If the client wants
October, it needs its own tab or its own report; do not quietly widen this one.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each -
unchanged from the last cut, re-pulled and confirmed. Meta also reports how far each went:
27 first replies, 13 conversations past one message, 5 past three, 3 past five - and every
one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for ₹160.80
against Gulf's ₹273.88. None of that is on the page yet; the `DAILY` row format has no
field for messaging depth.

Per-call figures cover **call campaigns only**: NRI Elder Care drives website traffic and
the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit outside
every per-call figure.

**This refresh reconciled clean.** Campaign sums equal the `level: "ad_account"` daily
totals on spend *and* impressions for all 26 delivery days, to the paisa, and every one of
the seven campaigns' period totals matches Meta's own on spend, impressions, calls placed,
20s and 60s.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data (a part-day) and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.

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
  Once a month is more than ~48h closed it stops moving: the 1 Nov refresh re-derived
  every day of September and only 28-30 Sep differed from what was published.
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
