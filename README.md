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

Frozen **19 Nov 2026, 8:15 am IST**. September 2026 is now a **complete, fully
settled month**, so the window is **4-30 Sep** and there is no part-day in scope:
`SNAP_DAY` is `null` and all 27 delivery days count toward every headline.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The account has spent nothing since 24 October.** September is closed and this
report's scope ends there, but October did run (Rs 18,476.76, 1-24 Oct) and the
account has been dark for 26 days since. Pain Management is the only campaign Meta
still reports ACTIVE; everything else is PAUSED or ARCHIVED. Extending this report
past September is a scope decision, not a refresh - it is not done here.

**Two days were added and three were revised.** The 29th was a part-day at
publication (Rs 71.22, 3 calls) and settled to **Rs 1,056.20 for 20 calls**; the
30th is new at **Rs 1,044.52 for 18 calls**. Meta also revised 28 Sep up by
Rs 4.53 in total (Pain +Rs 0.77, Lipoma +Rs 3.02, Autism +Rs 0.74) with no call
counts moving. That is the whole difference between the old 4-28 cut and this one.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Lipoma | Rs 457.23 | 13 | Rs 35.17 | 2 |
| Pain Management | Rs 587.29 | 5 | Rs 117.46 | 0 |

**Pain Management ended the month badly.** Its last two days ran Rs 74.41 and
**Rs 117.46** a call against its own Rs 58.11 month average - the dearest pair of
days it had. It is still the account's largest line by far (Rs 12,900.47, 222 calls)
and still holds callers best in absolute terms (61 of 222 reached 20 seconds), but
the price was moving the wrong way when delivery stopped. Worth a look before it
restarts, since it is the one campaign still set ACTIVE.

**Lipoma closes as the cheapest line, and it is not close.** Rs 3,493.24 for
**102 calls at Rs 34.25**, against Rs 56.70 for every other call campaign combined.
It kept that rate right to the end (Rs 35.14 and Rs 35.17 on its final two days).
It is now PAUSED.

**Endoscopy and Autism are unchanged** - both stopped before the 29th and neither
moved this refresh. Endoscopy closes at Rs 3,460.95 for 66 calls (Rs 52.44 each),
only 12 of which held twenty seconds, **Rs 288.41 per real conversation**. Autism
closes at Rs 2,131.13 for 42 calls (Rs 50.74), 10 past twenty seconds.

**Read the headline carefully - Lipoma is still holding the average down:**

| | 4-22 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30** |
|---|---|---|---|---|---|---|
| Cost per call placed | Rs 50.37 | Rs 49.39 | Rs 52.12 | Rs 51.28 | Rs 51.08 | **Rs 51.46** |
| ...excluding Lipoma | Rs 51.55 | Rs 52.64 | Rs 56.01 | Rs 55.52 | Rs 55.25 | **Rs 56.70** |
| Cost per 20-second call | Rs 186.55 | Rs 181.34 | Rs 209.78 | Rs 204.56 | Rs 203.83 | **Rs 214.17** |
| ...excluding Lipoma | Rs 187.72 | Rs 194.87 | Rs 226.53 | Rs 217.69 | Rs 213.69 | **Rs 226.13** |

Both rates rose on the full month, reversing the two-refresh fall. The per-call rate
has still never left the Rs 49-53 band across every cut recorded here; read it as
flat. The 20-second rate is the one that has genuinely drifted - Rs 186.55 to
Rs 214.17 since the 22nd, +15%. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised
for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal from the 19th until the account stopped.

**WhatsApp stays paused** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each -
unchanged to the paisa. Meta still reports 27 first replies, 13 conversations past
one message and 5 past three, and 29 total messaging connections; the Gulf ad set
holds every deep one. **The `messaging_user_depth_5_message_send` key is no longer
returned at all** (it read 3 at publication) - treat the "past five messages" figure
as withdrawn rather than zero. None of this is on the page; the `DAILY` row format
has no field for messaging depth.

**NRI Elder Care still reports nothing.** Rs 2,686.81 spent, 39 link clicks, and its
`HEnquiry` website event has **no conversions at all**. The page carries this as a
warning card. Unchanged since publication, and still unexplained.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` the last complete day, which is what the Yesterday card
reads. Both are plain constants — move them together on every refresh, or the card
will silently show a stale day. **When the month in scope has closed, set
`SNAP_DAY = null`**: nothing is then excluded, the "so far" tag never renders, and
the card relabels itself "Last day of the month". Set it back to a real date if this
report is ever re-pointed at a month still in progress.

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
  in step with the statuses or the "live" tag lies. As of 19 Nov it is `{4}` -
  Pain Management alone; Lipoma was paused after 30 Sep.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
