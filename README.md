# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **Yesterday** card (the last complete day; titled *Last day of the month* once the month is closed) with that day's billed amount,
  calls, 20s calls and cost per call, broken out by campaign.

## Snapshot

Frozen **7 Nov 2026, 8:10 am IST**, covering **4-30 Sep** - the whole month, now
closed. Every day on the page is fully settled, so for the first time there is no
part-day held out of the headline.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**September closed with two more days than the last cut showed.** The 29th and
30th were the last two days of delivery in the month, and both were Pain
Management plus Lipoma only:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | Rs 1,056.20 | 20 | Rs 52.81 | 3 |
| 30 Sep | Rs 1,044.52 | 18 | Rs 58.03 | 2 |

**The part-day guard earned its keep again.** 29 Sep was published as a part-day
at Rs 71.22 for 3 calls. Settled, it is Rs 1,056.20 for 20 calls - fifteen times
the spend. Meta also revised 28 Sep up by Rs 4.53 after publication (Autism
+Rs 0.74, Pain +Rs 0.77, Lipoma +Rs 3.02); no call counts moved.

**Both headline rates moved up, and the last two days are why.** Cost per call
placed Rs 51.08 -> **Rs 51.46**; the 20-second call Rs 203.83 -> **Rs 214.17**.
The 38 calls added on the 29th and 30th were cheap enough per call, but only 5 of
them held twenty seconds (13%, against 24% for the month), so the duration rate
took the strain.

**Only Pain Management is still ACTIVE at Meta.** Lipoma is now PAUSED as well,
joining Autism and Endoscopy. Its final September figures are its best:
Rs 3,493.24 for **102 calls at Rs 34.25**, against Rs 56.70 for every other call
campaign. It held the account average down on its own for the whole second half
of the month.

**Autism closes at Rs 2,131.13 for 42 calls, Rs 50.74 each** - 10 of them over
twenty seconds. Its last delivery was 28 Sep (Rs 495.44, 12 calls at Rs 41.29).
**Endoscopy** closes unchanged at Rs 3,460.95 for 66 calls (Rs 52.44 each), 12
over twenty seconds, **Rs 288.41 per real conversation**; its last day was the
27th.

**OUT OF SCOPE, BUT THE CLIENT WILL ASK: the account ran through October.**
It spent **Rs 18,476.76 across 1-24 October** (21 days with delivery; nothing on
3-5 Oct) and has spent **nothing since 24 October** - fourteen straight days dark
as of this snapshot, including every day of November. This page is September-only
by design and shows none of it. If October is wanted, it needs a month tab like
`halcyon-reports` has, or a second page.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44
each, unchanged since 24 Sep. Meta still reports 27 first replies, 13
conversations past one message and 5 past three. None of that is on the page; the
`DAILY` row format has no field for messaging depth.

**Read the headline carefully - Lipoma is still doing the work:**

| | 4-22 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Across every refresh recorded here the per-call rate has stayed inside Rs 49-53;
read it as flat. The 20-second rate is the one that has genuinely drifted, from
Rs 181 at its best to Rs 214 at the close. Keep both rows in front of the client.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so
both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day, held out of every total on the page, and `YDAY`
the last complete day, which the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.
**With September closed there is no part-day left in scope, so `SNAP_DAY` is
`null`** and all 26 days count toward the headline. The page handles `null`: the
"so far" tag never fires, the card titles itself *Last day of the month* instead
of *Yesterday*, and the line under it says September is final. If this report ever
grows a live month, set `SNAP_DAY` back to that month's part-day.

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
