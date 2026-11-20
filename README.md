# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).
The month is closed and fully settled.

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **last-complete-day** card with that day's billed amount, calls, 20s calls and
  cost per call, broken out by campaign. It titles itself *Yesterday* while a live
  part-day exists and *Last day of the month* once the window is closed.

## Snapshot

Frozen **20 Nov 2026, 8:10 am IST**, data window **4-30 September** - the month is
**closed and fully settled**, so every day on the page is final and there is no
part-day held out of the headlines.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds** (Rs 478.47 per minute-long call).

**September is final. The account has since gone quiet.** Nothing in scope changed
materially: the previously published 4-28 Sep window moved up by just **Rs 4.53** in
total (28 Sep only - Lipoma +Rs 3.02, Pain +Rs 0.77, Autism +Rs 0.74) and **no call
count moved at all**. The two days added are what shifted the headline:

| | published 29 Sep (4-28) | now (4-30) |
|---|---|---|
| Ad spend | Rs 28,994.36 | **Rs 31,099.61** |
| Calls placed | 399 | **437** |
| Cost per call placed | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 203.83 | **Rs 214.17** |
| Lasted 20s / 60s | 100 / 46 | **105 / 47** |

**This is the clearest case yet for excluding the part-day.** 29 Sep was published as
a part-day at Rs 71.22 for 3 calls. It settled at **Rs 1,056.20 for 20 calls** - just
under fifteen times the spend. Had it been allowed into the headline it would have
read as a near-total stop. 30 Sep closed the month at Rs 1,044.52 for 18 calls.

**Final campaign standings for September (ex-GST):**

| Campaign | Spend | Calls | Per call | 20s+ | Per 20s call | Status |
|---|---|---|---|---|---|---|
| Pain Management | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 | ACTIVE |
| Lipoma Removal | Rs 3,493.24 | 102 | **Rs 34.25** | 21 | **Rs 166.34** | PAUSED |
| Endoscopy | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 | PAUSED |
| Autism | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 | PAUSED |
| Kukatpally (1 day) | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 | PAUSED |
| NRI Elder Care (web) | Rs 2,686.81 | - | - | - | - | PAUSED |
| NRI + Bengaluru (WhatsApp) | Rs 5,924.79 | - | - | - | - | PAUSED |

**Lipoma ended the month the cheapest line on both measures** - Rs 34.25 a placed call
and Rs 166.34 for one that held 20 seconds - and it is now paused. It is still holding
the average down on its own: excluding it, September sits at **Rs 56.70** a call against
the blended Rs 51.46. Keep both rows in front of the client.

**Only Pain Management is still ACTIVE at Meta**, so `LIVE` is now `new Set([4])`.
Lipoma was paused after 30 Sep. Across every refresh recorded here the per-call rate has
stayed inside Rs 49-57; read it as flat.

**The account has been dark since 25 October - 27 consecutive days with zero spend.**
This is outside the September scope and does not touch any figure on the page, but it is
the first thing to raise with the client. October ran 1-24 Oct for Rs 18,476.76 and then
stopped mid-day on the 24th (Rs 177.18); nothing has been billed since, and no campaign
has delivered. Pain Management still reads ACTIVE while serving nothing, which usually
means a billing or spend-limit problem rather than a campaign fault - check Billing ->
Payment settings on `924502380456661`. **If the client wants October onward on the page,
that is a scope change** (a second month tab, as `halcyon-reports` does); this report is
September only by design and has not been widened.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal either side of it.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each -
unchanged from the last cut, and final. Meta also reports how far each went: 27 first
replies, 29 total messaging connections, 13 conversations past one message, 5 past
three - and the deep ones are the Gulf ad set. Bengaluru buys a conversation for
Rs 160.80 against Gulf's Rs 273.88. None of that is on the page: the `DAILY` row format
has no field for messaging depth.

**The msg campaign's `results` is a trap.** On a daily pull the WhatsApp campaign
returns `results` with indicator `onsite_conversion.messaging_conversation_started_7d`,
not calls. Those 27 conversations must be written as `placed: 0` in `DAILY` or they are
summed into the account's call count and corrupt every per-call figure. Same for the
website campaign. Only `type: "calls"` campaigns carry a call count.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day, when there is one, and `YDAY` the last complete
day, which is what the Yesterday card reads. Both are plain constants — move them
together on every refresh, or the card will silently show a stale day.

**With September closed there is no part-day, so `SNAP_DAY` is now the empty string**
and `YDAY` is `2026-09-30`. Nothing is held out of the totals, no row carries the
"so far" tag, and the card titles itself *Last day of the month* instead of
*Yesterday* and says the month is final. That is driven by one derived flag,
`livePart` — set `SNAP_DAY` back to a real date the day this report covers a running
month again and the part-day behaviour returns on its own. Do not hand-write either
label.

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
