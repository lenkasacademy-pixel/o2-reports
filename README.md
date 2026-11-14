# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
September is **closed and fully settled** - there is no part-day left in the data,
so `SNAP_DAY` is `null` and nothing is excluded from the headline figures.

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

Frozen **14 Nov 2026, 8:10 am IST**, covering the **complete month, 4-30 Sep**.
Every day is settled; the part-day guard is dormant (`SNAP_DAY = null`).
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**September is final.** The previous cut stopped at the 28th with the 29th as a
Rs 71.22 part-day. Both of the last two days came in as ordinary days and the
month closed on them:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

Only Pain Management and Lipoma were still running by then. The 30th was Pain
Management's dearest day of the month (Rs 587.29 for 5 calls, **Rs 117.46 each**)
against Lipoma's Rs 35.17 - a one-day gap that wide on 5 calls is small-sample
noise, not a finding.

**Revisions since the last cut.** Meta settled 28 Sep up by Rs 4.53 (Autism
+Rs 0.74, Pain +Rs 0.77, Lipoma +Rs 3.02); no call counts moved. The 29th grew
from the Rs 71.22 part-day to Rs 1,056.20 / 20 calls, which is exactly the
behaviour the part-day guard exists to hide from the headline.

**Both headline rates finished slightly worse than the 4-28 cut**, because the
closing days were dearer than the month's average: cost per call Rs 51.08 ->
**Rs 51.46**, the 20-second call Rs 203.83 -> **Rs 214.17**. The 20-second number
moved more than the per-call number because only 5 of the last 38 calls held
twenty seconds.

**The account is down to one ACTIVE campaign.** Pain Management is the only one
Meta still reports ACTIVE; Lipoma was paused after the month ended, and Autism,
Endoscopy, Kukatpally, NRI Elder Care and WhatsApp are all PAUSED. `LIVE` is now
`{4}`.

### Final per-campaign figures (4-30 Sep)

| Campaign | days | spend | calls | per call | 20s | per 20s call |
|---|---|---|---|---|---|---|
| Pain Management | 21 | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 |
| Lipoma Removal | 9 | Rs 3,493.24 | 102 | **Rs 34.25** | 21 | **Rs 166.34** |
| Endoscopy | 5 | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 |
| Autism | 6 | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 |
| Kukatpally (1-day test) | 1 | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 |
| NRI Elder Care (website) | 4 | Rs 2,686.81 | - | - | - | - |
| NRI + Bengaluru (WhatsApp) | 11 | Rs 5,924.79 | - | - | - | - |

**Lipoma closed as the cheapest line by a wide margin** - Rs 34.25 a call against
Rs 56.70 for every other call campaign put together, and it was the cheapest line
on eight of the nine days it ran (on 28 Sep Autism beat it by sixteen paise).
Pain Management still has the best hold rate: 61 of its 222 calls (27%) reached
twenty seconds.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each -
unchanged from the last cut, so the depth figures in the paragraph below were not
re-pulled. Meta also reports how far each went: 27 first replies, 13 conversations
past one message, 5 past three, 3 past five - and every one of the deep ones is the
Gulf ad set. Bengaluru buys a conversation for Rs 160.80 against Gulf's Rs 273.88.
None of that is on the page yet; the `DAILY` row format has no field for messaging
depth.

**Read the headline carefully - Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 51.03 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 53.24 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 184.36 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 191.08 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every cut recorded here the per-call rate has stayed inside Rs 49-53: read
it as flat. Keep both rows in front of the client. Per-call figures cover **call
campaigns only**: NRI Elder Care drives website traffic and the NRI + Bengaluru
campaign optimised for WhatsApp conversations, so both sit outside every per-call
figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal on either side of it.

## Out of scope: October delivery is not on this page

The report is scoped to September, but the account **kept spending into October**:
**Rs 18,476.76 across 21 delivery days, 1-24 Oct**, and then nothing at all -
the account has spent Rs 0.00 every day from **25 Oct to 14 Nov**. None of that is
in `DAILY`, because the page is a September report and the scope was not changed
on this refresh.

Two things follow, and both are decisions for a human, not for the refresh:

- If the client wants October, it needs its own scope (or month tabs, the way
  `halcyon-reports` does it). Do not quietly widen `DAILY` past 30 Sep - the
  masthead, the title and the footer all say September.
- **The three-week silence since 24 Oct is worth a question.** Pain Management is
  still ACTIVE at Meta yet has served nothing, which usually means billing, a
  spend cap or a payment method rather than a campaign problem. Nothing on this
  page shows it, because the page stops at 30 Sep.

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
  and the comment above `CAMPS`) and here - four places in the page, one here.
- `SNAP_DAY` may be `null`. It names the part-day to keep out of the headline
  figures; once a reported window has closed and settled there is no such day, and
  `null` is the honest value. The Yesterday card relabels itself to "Last day of
  the month" when it is null - that wording is derived, do not hand-write it.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
