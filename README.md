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

Frozen **20 Sep 2026**, covering 4–19 Sep (the 20th is a part-day and is excluded).
Ad spend ₹14,681.28 + 18% GST ₹2,642.63 = **₹17,323.91 billed**.
170 calls placed · 43 lasted 20s · 28 lasted 60s. ₹47.54 per call placed and
**₹187.94 per call that actually held 20 seconds**. That is up from ₹180.20 on the
4–17 cut; the 20-second cost has read ₹180 → ₹188 over two days and is not on a
trend either way yet. Per-call figures cover **call campaigns only**: NRI Elder
Care drives website traffic and the NRI + Bengaluru campaign optimises for WhatsApp
conversations, so both are excluded from every per-call figure.

**18 September was a near-total stop.** The whole account spent **₹6.43** that day
— ₹0.98 on Pain Management and ₹5.45 on WhatsApp, 122 impressions between them —
with both campaigns still set to ACTIVE at Meta. That is a delivery or billing
stop, not a decision someone made, and it is the single biggest thing on this
refresh. Spend resumed normally on the 19th.

**WhatsApp is now 27% of the account** — ₹3,913.14 for **16 conversations**, about
₹245 each, down from ₹322 on the 4–17 cut. It outspent the call campaign again on
19 September (₹1,340.84 against ₹1,053.24) and returned 8 conversations at ₹167.61,
its best day yet. At that day rate it undercuts a 20-second call; across the month
it still costs about 1.3× one. The shift of budget toward it has never been an
explicit decision — worth settling.

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
- `CAMPS` order must not be reshuffled; `DAILY[0]` indexes into it.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
