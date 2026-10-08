# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month is
now complete, so the page covers 4–30 Sep with every day settled.

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

Frozen **8 Oct 2026, 8:20 am IST**, covering **4–30 September — the whole month, every
day settled**. September is closed, so for the first time there is no part-day on the page
and `SNAP_DAY` is `null`.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month closed slightly dearer than the 4–28 cut read.** Cost per call went
₹51.08 → ₹51.46 and the 20-second call ₹203.83 → ₹214.17, because the last two days
were the two thinnest of the month for calls: the 29th took ₹1,056.20 for 20 calls
(₹52.81) and the 30th ₹1,044.52 for 18 (₹58.03), against ₹44.19 on the 27th. Pain
Management is the whole of that — on the 30th it bought just 5 calls for ₹587.29,
**₹117.46 each**, its worst day in the month by a wide margin, while Lipoma held at
₹35.17. Two days is not a trend, but it is the thing to watch in October.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |
| Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |
| Autism | — | — | — | — |
| Endoscopy | — | — | — | — |

**Only Pain Management and Lipoma are still live** (`LIVE` stays `{4, 6}`). Autism closed at
₹2,131.13 for 42 calls (₹50.74 each, 10 past twenty seconds at ₹213.11) and has not spent
since 28 Sep. Endoscopy closed at ₹3,460.95 for 66 calls (₹52.44) with only 12 holding
twenty seconds, **₹288.41 per real conversation** — still the dearest of the call campaigns
bar the one-day Kukatpally test.

**Lipoma finished the month as the cheapest line by a distance:** ₹3,493.24 for **102 calls
at ₹34.25**, against ₹56.70 for everything else, and its 20-second calls are the cheapest
too at ₹166.34. Pain Management is the biggest line at ₹12,900.47 for 222 calls (₹58.11)
and still holds callers best in absolute terms — 61 of its 222 (27%) lasted twenty seconds.

**Revisions this refresh.** The 29th was a part-day at ₹71.22 in the last cut and settled at
₹1,056.20; the 30th is new at ₹1,044.52. Meta also settled 28 Sep up by ₹4.53 in total
(Autism +₹0.74, Pain +₹0.77, Lipoma +₹3.02); no call counts moved. Everything on or
before 27 Sep came back unchanged.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each — unchanged,
and the depth figures re-pulled identical: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five.

### October is running, and it is not on this page

The report is September-only by design, but the account did not stop. Settled October spend
to the 7th is **₹4,411.07** (₹989.84 on the 1st, ₹537.66 on the 2nd, nothing at all on the
3rd, 4th or 5th, then ₹1,073.28 and ₹1,810.29 on the 6th and 7th), with ₹123.35 so far on
the 8th. **The three dark days in the middle are worth asking about.** If the client wants
October, the cleanest route is month tabs as in `halcyon-reports` rather than widening this
page's scope.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | 4–30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53; read it as
flat. Keep both rows in front of the client. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic (₹2,686.81 for the month) and the NRI + Bengaluru
campaign optimised for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still counting**, and
`YDAY` the last complete day, which is what the Yesterday card reads. Both are plain
constants — move them together on every refresh, or the card will silently show a stale day.

**Set `SNAP_DAY` to `null` once the month has closed** and no day in the data is unsettled,
as it is now. That makes the part-day filter a no-op, drops the "so far" tag from the day
table, and switches the card heading from "Yesterday" to "Last day" and its note to a line
saying the month is settled — all three are driven off the constant, so there is no prose to
hand-edit. Never point `SNAP_DAY` at a settled day: that would silently drop a real day out
of every headline total.

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
