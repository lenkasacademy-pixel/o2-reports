# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
The month is complete, so there is no part-day and `SNAP_DAY` is `null`.

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

Frozen **4 Nov 2026, 8:11 am IST**, covering **4-30 Sep — September is now
complete**, so for the first time nothing is held back as a part-day.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The two days that were missing are the whole story.** The previous cut stopped at
the 28th because the 29th was then a live part-day showing only ₹71.22. Settled, the
29th was ₹1,056.20 and the 30th added ₹1,044.52 — ₹2,105.25 of spend and 38 calls
that the published page never showed.

| | published 4-28 | now 4-30 | move |
|---|---|---|---|
| Ad spend | ₹28,994.36 | **₹31,099.61** | +₹2,105.25 |
| Calls placed | 399 | **437** | +38 |
| Cost per call placed | ₹51.08 | **₹51.46** | +₹0.38 |
| …excluding Lipoma | ₹55.25 | **₹56.70** | +₹1.45 |
| Lasted 20s+ | 100 | **105** | +5 |
| Cost per 20-second call | ₹203.83 | **₹214.17** | +₹10.34 |
| Lasted 60s+ | 46 | **47** | +1 |

**Why the 20-second call got ₹10 dearer.** The last two days bought 38 calls but only
5 of them held twenty seconds — ₹2,105 of spend against a ₹204 running rate. Cost per
call *placed* barely moved (₹51.08 → ₹51.46); it is the duration rate that absorbed it.
Across every refresh recorded here the per-call rate has stayed inside ₹49-₹53: read it
as flat.

**Meta also revised the 28th up by ₹4.53** after publication (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02; Autism's impressions 10,180 → 10,206). No call counts moved.
That is the ~48h settling the page is built to absorb.

**Autism and Lipoma both closed in September; only Pain Management is still ACTIVE.**

| campaign | spend | placed | each | 20s | per 20s | status |
|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | ACTIVE |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | PAUSED |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | PAUSED |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | PAUSED |
| Kukatpally (1 day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | PAUSED |

**Lipoma finished as the cheapest line on the account, and by a long way** —
₹34.25 a call against ₹56.70 for everything else, and the cheapest 20-second call
too (₹166.34). It ran nine days and was paused after the 30th. It is still holding
the account average down on its own: keep both rows in front of the client.

**Pain Management is the dearest placed call (₹58.11) and the best at holding one.**
61 of its 222 calls (27%) reached twenty seconds and 32 reached a minute — ₹403.14 per
minute-long call, far better than Lipoma's ₹582.21 or Endoscopy's none-of-note.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal on either side of it.

**WhatsApp is unchanged.** Still ₹5,924.79 for **27 conversations**, ₹219.44 each —
identical to the figure published on 29 Sep, because the campaign has been paused
throughout. Meta still reports 27 first replies, 13 conversations past one message
and 5 past three; the Bengaluru/Gulf ad-set split published earlier (₹160.80 against
₹273.88) was not re-pulled this refresh and stands as published. None of it is on
the page — the `DAILY` row format has no field for messaging depth.

Per-call figures cover **call campaigns only**: NRI Elder Care drives website traffic
(₹2,686.81, four days, all 4-10 Sep) and the NRI + Bengaluru campaign optimised for
WhatsApp conversations, so both sit outside every per-call figure.

## ⚠ October is out of scope, and the account has stopped

This page is **September only**, and that is now a month and a bit behind the account.
Two things a human needs to decide on:

1. **October delivered ₹18,476.76 across 21 days (1-24 Oct) and is not on this page.**
   Adding it means a month tab bar, which `o2-reports` does not have — that is the
   `halcyon-reports` pattern (one `DAILY_*` array + one `MONTHS` entry + one tab
   button), not an array patch. Deliberately **not** done here: it changes the shape
   of the report, which is the client's call, not a refresh's.
2. **The account has spent nothing for eleven straight days** — ₹0.00 every day from
   25 Oct through 4 Nov — while **Pain Management still reads ACTIVE at Meta**. An
   ACTIVE campaign serving nothing usually means billing or an account spend limit,
   not a campaign fault. Worth checking in Ads Manager before the next refresh.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently show
a stale day.

**When the reported month closes, set `SNAP_DAY = null`.** Every day in the data is
then fully settled and nothing should be held out of the headlines; the filter
(`r[1] !== SNAP_DAY`) keeps every row, the day table stops printing a "so far" tag,
and the Yesterday card's subtitle switches to saying the month is complete instead of
naming a part-day that no longer exists. Leaving `SNAP_DAY` pointing at a settled day
would silently drop it from every total — that is the mistake this guard prevents.

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
  in step with the statuses or the "live" tag lies. On 4 Nov it narrowed to
  `{4}`: Lipoma was paused after 30 Sep, leaving Pain Management the only ACTIVE
  campaign.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
