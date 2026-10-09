# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
September is now **closed and fully settled**, so this cut has no part-day in it.
`SNAP_DAY` is set to the snapshot day (`2026-10-09`), which is deliberately *not*
a date in `DAILY` - with nothing to exclude, every headline covers the whole month.
The Yesterday card detects that for itself (`hasPart`) and relabels to "Last day in
this report" rather than claiming a day is still counting.

> **The account is still spending, in October, and this report no longer covers it.**
> Pain Management and Lipoma Removal are both still ACTIVE. A direct 1-9 Oct pull gives
> Pain Management **Rs 3,777.67 for 55 calls** (Rs 68.68) and Lipoma
> **Rs 2,290.76 for 72 calls** (Rs 31.82) - Rs 6,068.43 and 127 calls between them, at
> a blended Rs 47.78. Every other campaign on the account reports Rs 0 and "Not
> available" for October. Note 9 Oct is a live part-day in that figure, so treat it as
> indicative. Whether to add an October view is a scope decision for a human: this page
> has no month tab bar, so adding one is not the one-array change it is in
> `halcyon-reports`.

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

Frozen **9 Oct 2026, 8:30 am IST**, covering **4-30 Sep - the complete month**.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**September closes on two campaigns and two numbers that both edged up.** Cost per
call placed went Rs 51.08 (4-28) -> **Rs 51.46** (4-30); the 20-second call went
Rs 203.83 -> **Rs 214.17**. The last two days are why: 29 and 30 Sep placed 38 calls
between them but only **3** of those held twenty seconds, against the ~25% the month
had been running at. On the per-call number the month still reads flat - every refresh
recorded here has stayed inside Rs 49-53.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

**30 September was Pain Management's dearest day of the month.** Rs 587.29 for 5 calls,
**Rs 117.46 each**, against Lipoma's Rs 35.17 on the same day. On the 29th it was
Rs 74.41 against Lipoma's Rs 35.14. Two days is not a trend, but both are well outside
the Rs 48-65 band Pain Management held all month, and it is the campaign still carrying
the budget - worth a look.

**Lipoma Removal closes the month as the cheapest line per call placed, and it never
lost that position.** Rs 3,493.24 for **102 calls at Rs 34.25**, against Rs 56.70 for
every other call campaign put together. It is also the only line that stayed level
across the last two days (Rs 35.14, then Rs 35.17).

**Pain Management** closes at Rs 12,900.47 for 222 calls (Rs 58.11) and still has the
highest share of calls that last: 61 of 222 (**27%**) held twenty seconds, Rs 211.48
each - better than Lipoma's 21 of 102 (21%).

**Autism and Endoscopy are both paused and final.** Autism closes at Rs 2,131.13 for
42 calls (Rs 50.74), 10 of them over twenty seconds. Endoscopy closes at Rs 3,460.95
for 66 calls (Rs 52.44) with only 12 over twenty seconds, **Rs 288.41 per real
conversation** - the dearest of the call campaigns bar the one-day Kukatpally test.

**Revisions this refresh.** Meta settled **28 Sep up by Rs 4.53** (Autism +Rs 0.74,
Pain +Rs 0.77, Lipoma +Rs 3.02; no call counts moved), taking that day from
Rs 1,558.97 to Rs 1,563.50. The 29th, published as a Rs 71.22 part-day, settled at
**Rs 1,056.20**. One all-zero WhatsApp row for 24 Sep was dropped: Meta reported a
late-attributed conversation with no spend, no impressions and no calls, and `DAILY`
has no field for messaging conversations.

**WhatsApp stays paused and unchanged** at Rs 5,924.79 for **27 conversations**,
Rs 219.44 each - re-pulled this refresh and identical to the last cut. Meta also
reports how far each went: 27 first replies, 13 conversations past one message, 5 past
three, 3 past five - and every one of the deep ones is the Gulf ad set. Bengaluru buys
a conversation for Rs 160.80 against Gulf's Rs 273.88. None of that is on the page yet;
the `DAILY` row format has no field for messaging depth.

**Read the headline carefully - Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 51.03 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 53.24 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 184.36 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 191.08 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49-53; read it
as flat. The 20-second rate has not: it has climbed in every cut since the 24th and is
now 18% above where it started. Keep both Lipoma rows in front of the client. Per-call
figures cover **call campaigns only**: NRI Elder Care drives website traffic and the
NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit outside every
per-call figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has explained it
yet; delivery was normal for the rest of the month.

## Reconciliation on this refresh

All three checks the refresh recipe asks for passed, on the full month:

- Campaign day rows equal the `level: "ad_account"` daily totals on **spend,
  impressions and link clicks** on all 26 days with delivery.
- Each campaign's period total (one pull without `time_increment`) equals the sum of
  its own day rows on spend, impressions, link clicks and calls placed - to the paisa,
  all seven campaigns.
- Every 20s and 60s derivation (`spend / cost_per_action_type:..._connect`) lands on a
  whole number, at day level and at period level, and the day-level counts sum to the
  period-level ones exactly for all five call campaigns.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the part-day, when there is one, and `YDAY` the last complete day,
which is what the Yesterday card reads. Both are plain constants — move them together
on every refresh, or the card will silently show a stale day. **When the scope month is
closed** (as now), point `SNAP_DAY` at the snapshot day instead, so it matches no row
in `DAILY` and nothing is excluded from the headlines; the card checks for itself
whether a part-day row exists before claiming one is still counting.

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
