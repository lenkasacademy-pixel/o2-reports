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

Frozen **23 Sep 2026**, covering 4–22 Sep (the 23rd is a part-day and is excluded).
Ad spend ₹18,684.72 + 18% GST ₹3,363.25 = **₹22,047.97 billed**.
200 calls placed · 54 lasted 20s · 34 lasted 60s. ₹50.37 per call placed and
**₹186.55 per call that actually held 20 seconds**.

**A new call campaign appeared on 22 September and is the cheapest thing this
account has ever run.** `O2 Health Hub | Lipoma Removal | Calls` — ₹124.53 for
**7 calls at ₹17.79**, against Autism's ₹33.96 and Pain Management's ₹52.49.
It is `CAMPS[6]`, appended not inserted. **One day and seven calls is not a
result**; it is a reason to keep the budget on it and look again in a week.

**WhatsApp has been paused.** It ended at ₹5,924.18 for 26 conversations,
**₹227.85** each, and its final ₹234.87 on 22 September returned none at all.
The last three cuts read ₹322 → ₹245 → ₹228 a conversation, so it was still
improving when it stopped — whoever paused it should know that.

**The per-call lines fell for the first time in four cuts**, but read them
carefully:

| | 4–17 | 4–19 | 4–21 | 4–22 |
|---|---|---|---|---|
| Cost per call placed | ₹46.24 | ₹47.54 | ₹50.88 | **₹50.37** |
| …excluding the new Lipoma campaign | — | — | ₹50.88 | ₹51.55 |
| Cost per 20-second call | ₹180.20 | ₹187.94 | ₹193.14 | **₹186.55** |
| …excluding Lipoma | — | — | ₹193.14 | ₹187.72 |

The headline fall in cost per call is **entirely** the new campaign; the older
campaigns kept getting dearer. The 20-second improvement is real on its own.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so
both are excluded from every per-call figure.

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
