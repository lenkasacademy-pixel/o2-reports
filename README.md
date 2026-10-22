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

Frozen **22 Oct 2026, 8:15 am IST**. **September 2026 is now complete** — the
report covers **4–30 September**, every day settled, nothing held out.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month is closed, so there is no part-day.** `SNAP_DAY` is now `null` and
every day counts toward the headline; the Yesterday card becomes "Last day of
the month" and reads 30 Sep. Set `SNAP_DAY` back to a date only if this page is
ever pointed at a month still in progress.

| | 4–27 | 4–28 (last cut) | **4–30 (final)** |
|---|---|---|---|
| Cost per call placed | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹217.69 | ₹213.69 | **₹226.13** |

**The last two days were thin and Pain Management carried them badly.** The 29th
took ₹1,056.20 for 20 calls and the 30th ₹1,044.52 for 18 — only Pain Management
and Lipoma ran on either. Pain Management closed at ₹74.41 and then **₹117.46 a
call** (5 calls on ₹587.29, none reaching 20 seconds), its two worst days of the
month. That is what lifts the month's cost per call from ₹51.08 to ₹51.46 and the
20-second call from ₹203.83 to ₹214.17 — the final two days, not a re-rating of
what came before.

**Lipoma stayed cheapest to the end** — ₹35.14 and ₹35.17 a call on the last two
days, closing at **₹3,493.24 for 102 calls, ₹34.25 each**, against ₹56.70 for
every other call campaign. It is now PAUSED.

**Only Pain Management is still ACTIVE** (`LIVE = new Set([4])`). Autism,
Endoscopy, Kukatpally, Lipoma, NRI Elder Care and WhatsApp all read PAUSED.

**Final per-campaign September figures:**

| Campaign | Spend | Calls | Each | 20s | 60s |
|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | 32 |
| Lipoma Removal | ₹3,493.24 | 102 | ₹34.25 | 21 | 6 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | 4 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | 4 |
| Kukatpally | ₹502.22 | 5 | ₹100.44 | 1 | 1 |
| NRI Elder Care (web) | ₹2,686.81 | — | — | — | — |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | — | — | — | — |

**Revisions picked up this refresh.** 29 Sep was a ₹71.22 part-day in the last
cut and settled at **₹1,056.20** — a reminder of why part-days are never allowed
to set a headline. 28 Sep settled up ₹4.53 (Pain +₹0.77, Autism +₹0.74,
Lipoma +₹3.02) with no call counts moving. Everything on or before 27 Sep is
unchanged.

> ### ⚠️ October 2026 is live and is NOT on this page
>
> The account has spent **₹17,025.90 across 1–22 October** (nothing on 3–5 Oct,
> then daily delivery from the 6th; 22 Oct is a part-day at ₹14.58). This report
> is scoped to September by design, so none of it appears here — but the client
> is spending now and the page says "September 2026" throughout. **Someone should
> decide whether to add an October view**, the way `halcyon-reports` carries a
> month tab bar. Nothing here is wrong; it is just no longer the whole story.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five — and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of
that is on the page yet; the `DAILY` row format has no field for messaging depth.
These figures are unchanged from the last refresh — the campaign has not spent since.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` the last complete day, which is what the Yesterday card
reads. Both are plain constants — move them together on every refresh, or the
card will silently show a stale day.

**When the reporting month has closed, set `SNAP_DAY = null`.** There is then no
unsettled day to hold out: `render()` skips the filter, every day counts toward
the headline, and the card switches from "Yesterday" to "Last day of the month".
Leaving `SNAP_DAY` pointing at a real date in a finished month would silently
drop a complete day from every total.

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and is
  down to `{4}` (Pain Management) as of the 22 Oct refresh — Lipoma, Autism and
  Endoscopy are all PAUSED now. Keep it in step with the statuses or the "live"
  tag lies.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
