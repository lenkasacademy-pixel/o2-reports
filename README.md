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

Frozen **29 Sep 2026, 11:10 am IST**, covering 4–28 Sep (the 29th is a part-day
and is excluded from every headline).
Ad spend ₹28,994.36 + 18% GST ₹5,218.98 = **₹34,213.34 billed**.
399 calls placed · 100 lasted 20s · 46 lasted 60s. ₹51.08 per call placed and
**₹203.83 per call that actually held 20 seconds**.

**28 September was an ordinary day, and the account is down to two campaigns.**
₹1,558.97 for 32 calls at **₹48.72**, 8 of them over twenty seconds. Both
headline rates edged down again: cost per call ₹51.28 → ₹51.08, the 20-second
call ₹204.56 → ₹203.83.

| 28 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | ₹694.21 | 11 | ₹63.11 | 4 |
| Autism | ₹494.70 | 12 | ₹41.23 | 3 |
| Lipoma | ₹370.06 | 9 | ₹41.12 | 1 |
| Endoscopy | — | — | — | — |

**Autism came back as expected, cheaply — and is now paused.** On the 26th it was
the dearest line (₹87.50 a call); on the 28th it bought 12 calls at ₹41.23, level
with Lipoma. It has spent nothing on the 29th and Meta now reports it PAUSED.

**Endoscopy is paused.** It spent nothing on the 28th and its status is PAUSED.
It closes at ₹3,460.95 for 66 calls (₹52.44 each) but only 12 held twenty seconds,
**₹288.41 per real conversation** — the dearest of the call campaigns bar the
one-day Kukatpally test. Its daily rate read ₹45.41 → ₹55.51 → ₹57.29 → ₹60.82 →
₹41.58 over its last five days: noise, not a trend.

**Only Pain Management and Lipoma are live now.** Pain Management was the dearest
line on both the 27th (₹62.59) and the 28th (₹63.11), but it has the highest
share of calls that last: 60 of its 208 (29%) held twenty seconds, ₹194.05 each.

**Lipoma is still the cheapest line per call placed, seven days running** — on the
28th by eleven paise over Autism, and that was its second-dearest day. Over the
settled days it has taken ₹2,646.47 for **78 calls at ₹33.93**, against ₹55.25
for everything else.

**Small revisions this refresh.** Meta settled 27 Sep up by ₹4.51 (Endoscopy
+₹1.72, Pain +₹0.89, Lipoma +₹1.90); no call counts moved. The 29th so far is
₹71.22 for 3 calls.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five — and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of
that is on the page yet; the `DAILY` row format has no field for messaging depth.

**Read the headline carefully — the whole improvement is the new campaign:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 |
|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | **₹51.08** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | **₹55.25** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | **₹203.83** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | **₹213.69** |

Both rates fell for a second refresh but neither is back to where it was on
the 24th. Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53;
read it as flat.
Lipoma is still holding the average down on its own; excluding it the account
sits at ₹55.25 a call. Keep both rows in front of the client. Per-call figures cover **call campaigns only**:
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
