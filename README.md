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

Frozen **30 Sep 2026, 8:10 am IST**, covering 4–29 Sep (the 30th is a part-day
and is excluded from every headline).
Ad spend ₹30,049.04 + 18% GST ₹5,408.83 = **₹35,457.87 billed**.
419 calls placed · 103 lasted 20s · 46 lasted 60s. ₹51.16 per call placed and
**₹208.13 per call that actually held 20 seconds**.

**29 September was an ordinary two-campaign day.** ₹1,050.15 for 20 calls at
**₹52.51**, 3 of them over twenty seconds. Both headline rates edged back up
after two refreshes of falling: cost per call ₹51.08 → ₹51.16, the 20-second
call ₹203.83 → ₹208.13.

| 29 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | ₹668.58 | 9 | ₹74.29 | 1 |
| Lipoma | ₹381.57 | 11 | ₹34.69 | 2 |
| Autism | — | — | — | — |
| Endoscopy | — | — | — | — |

**Autism is finished.** It spent nothing on the 29th or the 30th and Meta reports
it PAUSED. It closes at ₹2,131.13 for 42 calls, **₹50.74 each** — 10 held twenty
seconds (₹213.11) and 4 held a minute (₹532.78). Its last day, the 28th, was its
cheapest at ₹41.29.

**Endoscopy is paused and unchanged** at ₹3,460.95 for 66 calls (₹52.44 each),
only 12 of them past twenty seconds — **₹288.41 per real conversation**, still the
dearest of the call campaigns bar the one-day Kukatpally test.

**Only Pain Management and Lipoma are live.** Pain Management was the dearest
line again on the 29th (₹74.29, its worst day since the 26th) and now sits at
₹12,312.08 for 217 settled calls, **₹56.74 each**. It still holds callers best in
absolute terms: 61 of its 217 (28%) reached twenty seconds at ₹201.84.

**Lipoma's seven-day run as the cheapest line was broken by a revision, not a
day.** On the 28th as published it led Autism by eleven paise; Meta then settled
Lipoma up ₹3.02 and Autism up ₹0.74, and the 28th now reads Autism ₹41.29 against
Lipoma ₹41.45 — seventeen paise the other way. It was cheapest again on the 29th
(₹34.69) and over the settled days has taken ₹3,031.06 for **89 calls at ₹34.06**,
against ₹55.78 for everything else.

**Small revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Lipoma +₹3.02,
Pain +₹0.77, Autism +₹0.74) and added impressions to all three; no call counts
moved. The 30th so far is ₹10.51 for 1 call.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unmoved for a third refresh. Meta also reports how far each went: 27 first
replies, 13 conversations past one message, 5 past three, 3 past five — and every
one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for
₹160.80 against Gulf's ₹273.88. None of that is on the page yet; the `DAILY` row
format has no field for messaging depth.

**Read the headline carefully — the whole improvement is the new campaign:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | 4–29 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.16** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹55.78** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹208.13** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹219.12** |

Both rates ticked back up. Across every refresh recorded here the per-call rate has
stayed inside ₹49–₹53; read it as flat.
Lipoma is still holding the average down on its own; excluding it the account
sits at ₹55.78 a call. Keep both rows in front of the client. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised
for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

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
