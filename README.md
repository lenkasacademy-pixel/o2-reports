# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
The month is complete and settled. The account kept spending after September -
see the scope warning under *Snapshot*.

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

Frozen **16 Nov 2026, 8:15 am IST**, covering **4-30 September - the complete
month, long since settled.** There is no part-day any more, so `SNAP_DAY` is `""`
and every day in `DAILY` counts towards the headlines (see *Closing a month* below).
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

> ### The report now covers less than two-thirds of the account
>
> Scope is still September only, but the account did not stop in September.
> **1 Oct - 16 Nov: ₹18,476.76 and 273 more calls placed** - Pain Management
> ₹14,020.41 / 162 calls (still ACTIVE) and Lipoma ₹4,456.35 / 111 calls
> (ran on into October, now PAUSED). None of that is on the page.
> September is ₹31,099.61 of a ₹49,576.37 lifetime, so the page now
> describes **63% of what the account has spent**. Either widen the scope or
> tell the client plainly that this is a September-only report - a reader who
> assumes it is current is reading a figure seven weeks stale.

**The 29th is the clearest part-day lesson in this repo.** Published as a
part-day it read ₹71.22 for 3 calls. Settled, it is **₹1,056.20 for 20
calls** - 14.8x the spend. Anything built on that part-day would have been
wrong by an order of magnitude, which is exactly what `SNAP_DAY` exists to stop.

**The two new days closed the month quietly.** 29 Sep ₹1,056.20 for 20 calls
(₹52.81 each, 3 over twenty seconds); 30 Sep ₹1,044.52 for 18 calls
(₹58.03 each, 2 over twenty seconds). Only Pain Management and Lipoma were
still running by then.

**Meta also revised 28 Sep up by ₹4.53** after publication (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02); no call counts moved.

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30 final** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| ...excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| ...excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

**Read the per-call rate as flat and the 20-second rate as drifting up.** Across
every refresh recorded here the per-call rate has stayed inside ₹49-53 and it
closed at ₹51.46. The 20-second rate is the one that moved: ₹181 at its best
on the 24th, ₹214.17 at close, because the last week bought calls at the usual
price but fewer of them held. 24% of September's calls lasted twenty seconds,
against 25% at the 4-28 cut.
Lipoma is still holding the average down on its own; excluding it the month sits
at ₹56.70 a call. Keep both rows in front of the client. Per-call figures cover
**call campaigns only**: NRI Elder Care drives website traffic and the NRI +
Bengaluru campaign optimised for WhatsApp conversations, so both sit outside every
per-call figure.

### Where each campaign closed

| Campaign | Spend | Calls | Each | 20s+ | Per 20s | Status |
|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | **ACTIVE** |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | **₹166.34** | PAUSED |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | PAUSED |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | PAUSED |
| Kukatpally (1-day test) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | PAUSED |
| NRI Elder Care (website) | ₹2,686.81 | - | - | - | - | PAUSED |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | - | - | - | - | PAUSED |

**Lipoma finished cheapest on both measures** - ₹34.25 a placed call and
₹166.34 a twenty-second call, the best in the account - and it is paused.
Pain Management, the only line still running, is the dearest of the four real
call campaigns at ₹58.11, though 27% of its calls hold twenty seconds and 32
reached a full minute, more than every other campaign combined.

**`LIVE` is now `{4}`** - Pain Management alone. Lipoma, Autism and Endoscopy all
read PAUSED at Meta.

**18 September was a near-total stop** - the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five - and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None
of that is on the page; the `DAILY` row format has no field for messaging depth.

## Closing a month

September is over, so the part-day machinery is parked rather than removed:

- `SNAP_DAY = ""` matches no row, so nothing is held out of the headlines.
- `YDAY = "2026-09-30"` and the card retitles itself *Last day of the month*.
- `render()` computes `hasPart` (`DAILY` contains `SNAP_DAY`) and uses it to pick
  between the two wordings. **Set `SNAP_DAY` back to a real date the moment a live
  part-day enters `DAILY`** and the original behaviour returns by itself.

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
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer,
  and the comment above `CAMPS`) and here - four places in the file.
- `LIVE` is `{4}` as of 16 Nov 2026: Pain Management only.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
