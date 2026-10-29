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

Frozen **29 Oct 2026, 11:10 am IST**, covering **4-30 Sep — the complete month**.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September is closed, so `SNAP_DAY` is now `null`.** There is no part-day left in
scope: every day on the page is settled and counts toward the headline. The
Yesterday card re-titles itself "Last day of the month" and reads 30 Sep. Set
`SNAP_DAY` back to a date only if this report is ever re-pointed at a live month.

**The two days the last cut could not show.** 29 Sep settled at ₹1,056.20 for
20 calls (₹52.81) and 30 Sep at ₹1,044.52 for 18 calls (₹58.03). Only Pain
Management and Lipoma were still running; everything else was already paused. Both
days were weak on duration — 3 and 2 calls over twenty seconds between them — which
is what pushed the 20-second rate up.

**Both headline rates rose on the full month**, reversing the two refreshes that
had them falling: cost per call ₹51.08 → **₹51.46**, the 20-second call
₹203.83 → **₹214.17**. The per-call move is small and still inside the
₹49-₹53 band this report has always sat in; the 20-second move is the real one,
and it is entirely the thin tail of the month.

| | spend | calls | each | 20s | per 20s | 60s |
|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 32 |
| Lipoma | ₹3,493.24 | 102 | ₹34.25 | 21 | ₹166.34 | 6 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 4 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 4 |
| Kukatpally | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 1 |

**Only Pain Management is still ACTIVE** — `LIVE` is down to `new Set([4])`.
Lipoma, which was live at the last cut, now reads PAUSED. It closes as **the
cheapest line per call placed by a wide margin**: ₹34.25 against ₹56.70 for
everything else, and the cheapest 20-second call on the account at ₹166.34. It is
still holding the blended average down single-handedly — keep both rows in front
of the client.

**Autism closes at ₹2,131.13 for 42 calls** (₹50.74). It was paused at the last
cut and never came back, so its 28 Sep day is its last.

**Small revisions this refresh.** Meta settled 28 Sep up by ₹4.59 in total
(Lipoma +₹3.02, Pain +₹0.77, Autism +₹0.74); no call counts moved. Nothing
before the 28th changed — the campaign period totals reconcile exactly against the
day rows for all seven campaigns on spend, calls, 20s **and** 60s.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged, it has not spent since 22 Sep. Meta still reports 29 total messaging
connections, 27 first replies, 13 conversations past one message and 5 past three.
The depth-past-five figure quoted in earlier cuts is **no longer returned** for this
campaign, so it has been dropped rather than carried forward unverified. None of
this is on the page: the `DAILY` row format has no field for messaging depth.

**Read the headline carefully — Lipoma is still the whole story:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49-₹53 —
read it as flat. Per-call figures cover **call campaigns only**: NRI Elder Care
drives website traffic (₹2,686.81, still **no `HEnquiry` conversions at all**) and
the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit
outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal either side of it.

## October 2026 is out of scope and the account is spending again

This report is **September only**, by design, and that is now a closed month. But
the account did not stop: it spent again from **1 Oct to 24 Oct** (roughly
₹18,000 across the month, three dark days 3-5 Oct, and nothing at all since
24 Oct). None of that is on this page.

Somebody needs to decide what this report should be:

- extend it to a **month tab bar** the way `halcyon-reports` does (one `DAILY_*`
  array and one `MONTHS` entry per month), or
- leave it frozen as the September record and start a separate October report.

Until that call is made, the page is correct but it describes a month that ended a
month ago. Do not quietly widen the scope — the headline rates are month-specific
and blending October into them would change every number the client has been shown.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data when that day is still a part-day,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently
show a stale day.

**`SNAP_DAY` is `null` while the reporting month is closed.** September has ended,
so there is no unsettled day in scope and nothing should be held out of the
headline. With `null`, the filter that drops the part-day drops nothing, the
day-by-day table stops printing a "so far" tag, and the card re-titles itself
"Last day of the month". `YDAY` is then simply the month's last day (30 Sep). The
guard still matters and must come back the moment this page points at a live
month — a part-day must never set a headline number.

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
