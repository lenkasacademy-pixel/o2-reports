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

Frozen **15 Oct 2026, 8:05 am IST**, covering **4-30 September - the month is now
closed**. Every day in the window has settled, so for the first time nothing is held
back: `SNAP_DAY` is `null` and the page says so instead of naming a part-day.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**September ended on two campaigns and then one.** Pain Management and Lipoma were
the only lines still spending on the 29th and 30th; Lipoma has since been paused too,
so `LIVE` is down to a single index (4, Pain Management).

| day | spend | calls | each | 20s |
|---|---|---|---|---|
| 28 Sep | Rs 1,563.50 | 32 | Rs 48.86 | 8 |
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

**Both headline rates turned back up over the last two days** after falling for two
refreshes: cost per call Rs 51.08 -> Rs 51.46, the 20-second call Rs 203.83 ->
Rs 214.17. The cause is visible in one line - **Pain Management's last two days were
its dearest**, Rs 74.41 a call on the 29th and Rs 117.46 on the 30th (5 calls on
Rs 587.29, and not one of them held twenty seconds). Lipoma was flat and cheap
either side of it, Rs 35.14 then Rs 35.17.

**Lipoma closes as the cheapest line on the account, by a distance.**
Rs 3,493.24 for **102 calls at Rs 34.25**, against Rs 56.70 for everything else;
21 of its calls held twenty seconds (Rs 166.34 each), the best 20-second rate of
any campaign. It is now PAUSED.

**Autism closed on 28 Sep** at Rs 2,131.13 for 42 calls (Rs 50.74 each), 10 of them
over twenty seconds. **Endoscopy** closes at Rs 3,460.95 for 66 calls (Rs 52.44) but
only 12 held twenty seconds, **Rs 288.41 per real conversation** - still the dearest
of the call campaigns bar the one-day Kukatpally test.

**Pain Management is the whole account now**, and it is the dearest of the four call
lines at Rs 58.11 a call - but it holds callers best: 61 of its 222 calls (27%) got
past twenty seconds and 32 past a minute, Rs 211.48 and Rs 403.14 each.

**Revisions this refresh.** Meta settled 28 Sep up by Rs 4.53 (Autism +Rs 0.74,
Pain +Rs 0.77, Lipoma +Rs 3.02) and +91 impressions; no call counts moved. Campaign
sums equal the account's own daily spend and impressions on all 26 delivery days, and
each campaign's day rows sum to its own period total on spend, calls, 20s, 60s,
impressions and link clicks.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five - and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for Rs 160.80 against Gulf's Rs 273.88. None of
that is on the page yet; the `DAILY` row format has no field for messaging depth.

**Read the headline carefully - Lipoma is still holding the average down:**

| | 4-22 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49-53;
read it as flat. Excluding Lipoma the account closes at Rs 56.70 a call. Keep both
rows in front of the client. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised
for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal afterwards for the rest of the month.

## The report stops at 30 September, but the account did not

**Scope is September only, so this is deliberately off the page** - but somebody
should decide whether it stays that way. Between 1 and 15 October the account has
already spent **Rs 12,560.41 for 218 calls** (Pain Management Rs 8,104.06 / 107
calls, Lipoma Rs 4,456.35 / 111 calls before it was paused). That is 40% of what
September cost, and the client cannot see any of it. Either widen the scope to a
month tab bar like `halcyon-reports`, or say plainly on the page that it covers
September alone.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day and `YDAY` the last complete day, which is what the
Yesterday card reads. Both are plain constants — move them together on every refresh,
or the card will silently show a stale day.

**Set `SNAP_DAY` to `null` once the month has closed** and every day in it has settled,
as it is now. A settled day must not be dropped from the headline totals just because
it is last, so `null` means nothing is held back; the card then titles itself
“Last day of the month” instead of “Yesterday” and says the month has closed.
`YDAY` becomes the last day with delivery (30 Sep). While a month is still running,
`SNAP_DAY` is the part-day again and the old behaviour returns — both paths are in
the page, so this does not need re-editing each way.

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
