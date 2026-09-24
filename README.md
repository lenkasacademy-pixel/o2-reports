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

Frozen **24 Sep 2026**, covering 4–23 Sep (the 24th is a part-day and is excluded).
Ad spend ₹20,041.53 + 18% GST ₹3,607.48 = **₹23,649.01 billed**.
224 calls placed · 62 lasted 20s · 36 lasted 60s. ₹51.03 per call placed and
**₹184.36 per call that actually held 20 seconds**.

**Lipoma Removal is holding up.** Two days in: `O2 Health Hub | Lipoma Removal |
Calls` has taken ₹729.79 for **23 calls at ₹31.73** — against Pain Management's
₹54.62 on the same account, and cheaper than Autism's ₹33.96, the best this
account had managed before. Day two alone was 16 calls at ₹37.83. It is
`CAMPS[6]`, appended not inserted. Two days is still two days, but it has now
survived one.

**WhatsApp stays paused** at ₹5,924.18 for 26 conversations, ₹227.85 each. It was
still improving when it stopped (₹322 → ₹245 → ₹228 across three cuts).

**Read the headline carefully — the whole improvement is the new campaign:**

| | 4–17 | 4–19 | 4–21 | 4–22 | 4–23 |
|---|---|---|---|---|---|
| Cost per call placed | ₹46.24 | ₹47.54 | ₹50.88 | ₹50.37 | **₹51.03** |
| …excluding Lipoma | — | — | ₹50.88 | ₹51.55 | **₹53.24** |
| Cost per 20-second call | ₹180.20 | ₹187.94 | ₹193.14 | ₹186.55 | **₹184.36** |
| …excluding Lipoma | — | — | ₹193.14 | ₹187.72 | **₹191.08** |

Both blended lines look flat or better. Both lines **excluding Lipoma keep
getting dearer** — ₹50.88 → ₹51.55 → ₹53.24 a call, ₹193.14 → ₹187.72 → ₹191.08
a 20-second call. The older campaigns have not turned around; one small new
campaign is carrying the average. Per-call figures cover **call campaigns only**:
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
