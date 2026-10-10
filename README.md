# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery, through
30 Sep). The month is complete. The account has resumed spending in October and
that is deliberately *not* on this page — see the snapshot note below.

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

Frozen **10 Oct 2026, 8:05 am IST**, covering **4-30 Sep — September is now a
closed month**, so there is no part-day and every day on the page is settled.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The account is spending again in October, and that is outside this report.**
1-9 Oct took ₹7,404.51 for 142 calls (Pain Management ₹4,548.58 / 62, Lipoma
₹2,855.94 / 80), with 3-5 Oct dark. The page is scoped to September by design,
so none of that appears on it. If the client wants October, this report needs a
month tab the way `halcyon-reports` has one — don't quietly widen the September
scope, because every headline on the page is a September figure.

**September closed with two campaigns and two ordinary days.** The 29th took
₹1,056.20 for 20 calls (₹52.81) and the 30th ₹1,044.52 for 18 calls (₹58.03) —
both inside the ₹49-₹59 band the account has held all month.

| last two days | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep — Pain Management | ₹669.68 | 9 | ₹74.41 | 1 |
| 29 Sep — Lipoma | ₹386.52 | 11 | ₹35.14 | 2 |
| 30 Sep — Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |
| 30 Sep — Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |

**Both headline rates rose on the full month**, because the two days added were
dearer than the month's average: cost per call ₹51.08 → **₹51.46**, the
20-second call ₹203.83 → **₹214.17**. Pain Management is what moved them — its
30 Sep was its dearest day of the month at ₹117.46 a call, on 5 calls.

**Pain Management closes September at ₹58.11 a call** (₹12,900.47, 222 calls over
21 days), still the dearest live line, and still the one whose calls last: 61 of
222 (27%) held twenty seconds, ₹211.48 each.

**Lipoma closes cheapest by a wide margin, every day it ran** — ₹3,493.24 for
**102 calls at ₹34.25**, against ₹56.70 for everything else. 21 of its calls
held twenty seconds (₹166.34 each), the best 20-second rate on the account.

**Autism and Endoscopy are both finished and both PAUSED.** Autism closes at
₹2,131.13 for 42 calls (₹50.74), 10 over twenty seconds at ₹213.11. Endoscopy
closes at ₹3,460.95 for 66 calls (₹52.44) but only 12 held twenty seconds,
**₹288.41 per real conversation** — the dearest of the call campaigns bar the
one-day Kukatpally test.

**Revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02); no call counts moved. The 29th, published as a
₹71.22 part-day, settled at ₹1,056.20 — which is exactly why the part-day is
kept out of the headlines.

**WhatsApp stays paused and unchanged** at ₹5,924.79 for **27 conversations**,
₹219.44 each. Meta also reports how far each went: 27 first replies, 13
conversations past one message, 5 past three, 3 past five — and every one of the
deep ones is the Gulf ad set. Bengaluru buys a conversation for ₹160.80 against
Gulf's ₹273.88. None of that is on the page yet; the `DAILY` row format has no
field for messaging depth.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4-22 | 4-24 | 4-26 | 4-28 | 4-30 |
|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹49.39 | ₹52.12 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹52.64 | ₹56.01 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹181.34 | ₹209.78 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹194.87 | ₹226.53 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside
₹49-₹53 — read it as flat for the month. Excluding Lipoma the account sits at
₹56.70 a call. Keep both rows in front of the client. Per-call figures cover
**call campaigns only**: NRI Elder Care drives website traffic and the NRI +
Bengaluru campaign optimised for WhatsApp conversations, so both sit outside
every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day and `YDAY` the last complete day, which is what
the Yesterday card reads. Both are plain constants — move them together on every
refresh, or the card will silently show a stale day.

**When the reported month has closed, set `SNAP_DAY = null`** and point `YDAY` at
the last day of the month. There is then no unsettled day to hold out, so every
day counts towards the headlines, the day table stops tagging anything *so far*,
and the card retitles itself "Last day of the month". The card reads both
constants, so don't hand-write either label.

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
