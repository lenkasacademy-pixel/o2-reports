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

Frozen **27 Sep 2026, 8:25 am IST**, covering 4–26 Sep (the 27th is a part-day
and is excluded from every headline).
Ad spend ₹25,604.11 + 18% GST ₹4,608.74 = **₹30,212.85 billed**.
326 calls placed · 81 lasted 20s · 42 lasted 60s. ₹52.12 per call placed and
**₹209.78 per call that actually held 20 seconds**.

**All four call campaigns are live again**, and 26 September was the account's
busiest day of the month — ₹3,826.35 for 58 calls. It was also an expensive one:
**₹65.97 a call against the ₹52.12 month average**, and only 9 of those 58 calls
held 20 seconds. Both headline rates moved the wrong way this refresh — cost per
call ₹49.39 → ₹52.12, and the 20-second call ₹181.34 → ₹209.78.

| 26 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Endoscopy | ₹1,324.01 | 22 | ₹60.18 | 5 |
| Pain Management | ₹1,079.30 | 13 | ₹83.02 | 1 |
| Autism | ₹875.00 | 10 | ₹87.50 | 1 |
| Lipoma | ₹548.04 | 13 | ₹42.16 | 2 |

**Endoscopy is the one to watch.** It restarted on the 25th and has taken
₹1,856.15 over three days for 32 calls. Its daily rate reads ₹45.41 → ₹55.51 →
₹57.29 → ₹60.18 → ₹36.91 across every day it has ever run: it gets dearer the
longer it stays on, then resets cheap after a break.

**Lipoma is still the best line, five days running**, but it is drifting:
₹17.95 → ₹37.85 → ₹25.88 → ₹32.15 → ₹42.16. Over the settled days it is
₹1,814.86 for **55 calls at ₹33.00**, against ₹56.01 for everything else. The
gap is still large, but it was ₹29.77 vs ₹52.64 two days ago.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five — and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of
that is on the page yet; the `DAILY` row format has no field for messaging depth.

**Read the headline carefully — the whole improvement is the new campaign:**

| | 4–21 | 4–22 | 4–23 | 4–24 | 4–26 |
|---|---|---|---|---|---|
| Cost per call placed | ₹50.88 | ₹50.37 | ₹51.03 | ₹49.39 | **₹52.12** |
| …excluding Lipoma | ₹50.88 | ₹51.55 | ₹53.24 | ₹52.64 | **₹56.01** |
| Cost per 20-second call | ₹193.14 | ₹186.55 | ₹184.36 | ₹181.34 | **₹209.78** |
| …excluding Lipoma | ₹193.14 | ₹187.72 | ₹191.08 | ₹194.87 | **₹226.53** |

The blended cost per call has gone back above ₹50 and the 20-second call is now
the dearest this account has recorded on either row. Restarting Endoscopy and
Autism added volume — 58 calls on the 26th, the best day of the month — but at
₹65.97 each, and Autism's ten calls cost ₹87.50 apiece. Lipoma is still holding
the average down; excluding it the account is at ₹56.01 a call. Keep both rows in
front of the client. Per-call figures cover **call campaigns only**:
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
