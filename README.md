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

Pulled **9 Nov 2026, 8:15 am IST**. **September 2026 is now a complete, closed
month**: the window is **4–30 September**, every day of it settled, and there is no
part-day to exclude. `SNAP_DAY` is therefore `null` and `YDAY` is `2026-09-30`; the
card that used to read "the 29th is still counting" now says the month is complete.
Nothing in the data is excluded from any headline.

Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
**437 calls placed · 105 lasted 20s · 47 lasted 60s.** ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The 29th was the part-day last time, and it moved a lot.** It was published at
₹71.22 for 3 calls; settled, it is **₹1,056.20 for 20 calls**. That single day is the
clearest argument for the part-day rule this report has produced — had it been left
in the headline it would have read as a collapse that never happened. The 30th
settled at ₹1,044.52 for 18 calls.

**Adding the 29th and the 30th barely moved the headline.** Cost per call placed went
₹51.08 (4–28) → **₹51.46** (4–30); the 20-second call ₹203.83 → **₹214.17**. The
20-second figure moved more because those two days placed 38 calls but only 3 of them
held twenty seconds.

**Only two campaigns ran to the end of the month**, Pain Management and Lipoma, and
they are the whole of the 29th and 30th. Autism, Endoscopy and Kukatpally all closed
earlier in the month and are unchanged from the last cut.

**Pain Management closes as the account's biggest line**: ₹12,900.47 for 222 calls
(₹58.11 each), 61 of them past twenty seconds — 27%, the best durable-call share of
any campaign — at ₹211.48 per 20-second call.

**Lipoma stays the cheapest line per call placed**: ₹3,493.24 for **102 calls at
₹34.25**, against ₹56.70 for every other call campaign put together. Excluding it, the
account sits at ₹56.70 a call and ₹226.13 per 20-second call. Keep both rows in front
of the client.

**Status now (read as of 9 Nov, outside the report's scope):** only **Pain Management
is still ACTIVE** at Meta. Lipoma has since been paused, so `LIVE` is now
`new Set([4])` — a single index again.

**18 September remains a near-total stop** — the whole account spent ₹6.43 that day on
122 impressions with both campaigns ACTIVE. Nobody has explained it; delivery was
normal before and after.

**WhatsApp is unchanged** at ₹5,924.79 for **27 conversations**, ₹219.44 each — 27
first replies, 13 conversations past one message, 5 past three, 3 past five, and every
deep one on the Gulf ad set. None of that is on the page; the `DAILY` row format has no
field for messaging depth, so it lives in this README alone.

**Read the headline carefully — Lipoma is still holding the average down on its own:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | 4–30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every cut recorded here the per-call rate has stayed inside ₹49–₹53. Read it
as flat, and read the month as closed. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised for
WhatsApp conversations, so both sit outside every per-call figure.

**Reconciliation.** Campaign sums equal the account's own daily spend **and**
impressions on all 26 delivery days, and every 20s/60s division lands on a whole
number.

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
- **The month is closed, so there is no part-day.** `SNAP_DAY` is `null` and the
  "still counting" line and the "so far" tag both switch themselves off when no
  `DAILY` row matches `SNAP_DAY`. Do not point `SNAP_DAY` at a real September day to
  satisfy the old shape — that would drop a settled day out of every headline.
- `LIVE` is read from Meta *now*, not from the report window: at the 9 Nov pull only
  Pain Management was still ACTIVE.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
