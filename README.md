# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month
is now **complete** — 4–30 Sep, every day settled, nothing held back as a part-day.

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

Frozen **12 Nov 2026, 8:20 am IST**, covering **4–30 September — the complete month**.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. **₹51.46 per call placed** and
**₹214.17 per call that held 20 seconds** (₹478.47 per 60-second call).

### THE ACCOUNT HAS BEEN DARK SINCE 24 OCTOBER

**Read this before sending the report to the client.** September is closed and this
page is final for that month, but the account did not stop there:

| Period | Spend |
|---|---|
| Sep (4–30) | ₹31,099.61 |
| Oct (1–2, 6–24) | ₹18,476.76 over 21 delivering days |
| 25 Oct – 12 Nov | **₹0.00 — 19 consecutive days, nothing at all** |

`O2 Health Hub | Pain Management | Calls | Sep 2026` still reads **ACTIVE** at Meta
and is the only campaign in `LIVE`, but it has not spent since 24 Oct. **The "live"
tag on this page means "not paused at Meta", not "delivering."** Nobody has
explained the stop; there is no October report in this repo to carry it. Either
raise it with the client or add an October tab — a September-only page increasingly
describes a smaller share of what the account has done.

### What moved in this refresh

The previous cut was frozen 29 Sep at 11:10 am, mid-day, and covered 4–28 Sep.

- **29 Sep settled, and it was mostly unbilled at the old snapshot.** Pain Management
  ₹43.37 → **₹669.68** (1 call → 9), Lipoma ₹27.85 → **₹386.52** (2 calls → 11). The
  day closes at ₹1,056.20 for 20 calls. This is exactly why a part-day never sets a
  headline number.
- **30 Sep is new**: ₹1,044.52, 18 calls, ₹58.03 each — Pain Management ₹587.29 for 5,
  Lipoma ₹457.23 for 13 (2 over 20s). It is the "Final day" card.
- **28 Sep revised up ₹4.53** (Autism +₹0.74, Pain +₹0.77, Lipoma +₹3.02). No call
  counts moved.
- **Both headline rates rose** once the two settled days were in: cost per call
  ₹51.08 → **₹51.46**, the 20-second call ₹203.83 → **₹214.17**. Still inside the
  ₹49–₹53 band the per-call rate has held across every refresh.
- **Lipoma is now PAUSED** (it was live at the last cut), so `LIVE` went from
  `{4, 6}` to `{4}`.

### Final September, by campaign

| Campaign | Spend | Calls | Per call | 20s | 60s |
|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | 32 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | 6 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | 4 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | 4 |
| Kukatpally (one-day test) | ₹502.22 | 5 | ₹100.44 | 1 | 1 |

**Lipoma finished the month as the cheapest line per call placed**, ₹34.25 against
₹55.25 for everything else — it held the account average down on its own all month.
Pain Management was the dearest of the continuing lines at ₹58.11 but keeps callers
longest: 61 of its 222 calls (27%) held twenty seconds.

Per-call figures cover **call campaigns only** (₹22,488.01 of the ₹31,099.61).
`O2 Guardian | NRI Elder Care` drives website traffic (₹2,686.81) and the NRI +
Bengaluru campaign optimised for WhatsApp conversations (₹5,924.79), so both sit
outside every per-call figure.

**WhatsApp, final September** — ₹5,924.79 for **27 conversations**, ₹219.44 each.
Depth: 29 total messaging connections, 27 first replies, 13 conversations past one
message, 5 past three. Meta no longer returns a
`messaging_user_depth_5_message_send` cost for this campaign, so the "3 past five"
figure from the previous cut cannot be reproduced and is dropped rather than carried
forward. None of this is on the page: the `DAILY` row format has no field for
messaging depth.

**18 September was still a near-total stop** — ₹6.43 across the whole account, 122
impressions. Nobody has explained it; delivery was normal either side.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` names the day that is **still accruing**, and `YDAY` the last complete
day, which is what the card reads. Both are plain constants — move them together on
every refresh, or the card will silently show a stale day.

**September is closed, so `SNAP_DAY` is now `null`** and no day is held out of the
totals; `YDAY` is `2026-09-30`. With `SNAP_DAY` null the card titles itself "Final
day" and says the month is complete instead of claiming a day is still counting.
Set `SNAP_DAY` back to a date only if a live day is ever in scope again.

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
- Update the snapshot date in `index.html` — **four places**: the title comment,
  the masthead stamp, the footer line and the `baked figures` comment — and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
