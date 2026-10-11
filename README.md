# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month is now
**closed and fully settled** — 4–30 Sep, no part-day.

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

Frozen **11 Oct 2026, 8:25 am IST**, covering **4–30 September — the complete month**.
September has been closed for eleven days, so nothing in it is still settling and
**`SNAP_DAY` is `null`**: there is no part-day to hold out of the headlines, and every
day in the data counts towards them. `YDAY` is 30 Sep, the last day of the month, which
is what the Yesterday card reads.

Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**Only two campaigns ran out the month.** Pain Management and Lipoma Removal carried
29 and 30 September between them; Autism, Endoscopy, Kukatpally, NRI Elder Care and
WhatsApp were all paused before the 29th and are still PAUSED.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

**30 September was Pain Management's worst day of the month: ₹587.29 for 5 calls,
₹117.46 each**, against its ₹58.11 September average. Lipoma took ₹457.23 for 13 at
₹35.17 the same day. One day is not a trend, but it is the dearest single campaign-day
in September and it is the last thing the client sees on this page.

**Meta revised 28 September upward after the last publication**, by ₹4.53 in total
(Autism ₹494.70 → ₹495.44, Lipoma ₹370.06 → ₹373.08, Pain ₹694.21 → ₹694.98). No call
counts moved. The 29th, which the previous cut showed as a ₹71.22 part-day with 3 calls,
settled at **₹1,056.20 and 20 calls** — a reminder of how little of a part-day is real.

**Both headline rates edged up as the month closed**, because the two days added were
dearer than the average they joined:

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53; read it
as flat. Keep both rows in front of the client: **Lipoma is still holding the average
down on its own** — ₹3,493.24 for **102 calls at ₹34.25**, against ₹56.70 for everything
else. Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both
sit outside every per-call figure.

### Per campaign, 4–30 September

| Campaign | Spend | Calls | Per call | 20s | Per 20s | 60s | Days live |
|---|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 32 | 21 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | 6 | 9 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 4 | 5 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 4 | 6 |
| Kukatpally (one-day test) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 1 | 1 |

Pain Management is the dearest live line per call placed but holds callers best of the
big two: 61 of its 222 (27%) held twenty seconds. Endoscopy closes as the dearest real
conversation of the call campaigns bar the Kukatpally test — ₹288.41 per 20-second call.

**The account did not stop on 30 September.** Pain Management and Lipoma have run all
through October: **1–11 Oct is ₹8,831.20 for 170 calls** — Pain ₹5,465.27 / 77 calls
(**₹70.98 each**, well above its September ₹58.11) and Lipoma ₹3,365.93 / 93 calls
(₹36.19). None of that is on this page, because the scope is September only. If the
client wants the current picture rather than a closed month, the page needs an October
scope — that is a decision, not a refresh, so it has deliberately not been made here.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each, with no
October spend. Meta also reports how far each went: 27 first replies, 13 conversations
past one message, 5 past three, 3 past five — and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of that is
on the page yet; the `DAILY` row format has no field for messaging depth. (Re-derived on
this pull from `cost_per_action_type`; all four divisions land on whole numbers.)

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal from the 19th to the end of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still accruing**, and
`YDAY` the last complete day, which is what the Yesterday card reads. Both are plain
constants — move them together on every refresh, or the card will silently show a stale
day. **When the month is closed there is no part-day: set `SNAP_DAY = null`**, which
makes the filter a no-op so every day counts towards the headlines, suppresses the
"so far" tag in the day table, and switches the Yesterday card's sub-line to say the
month is complete. Do **not** point `SNAP_DAY` at a settled day — that silently drops a
real day out of every total.

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
