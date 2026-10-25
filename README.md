# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).
September is now **closed and fully settled** — there is no part-day on the page, so
`SNAP_DAY` is `null` and every day counts toward the headline numbers. The account has
gone on spending into October (₹18,476.76 and 273 calls over 1–24 Oct, Pain Management
and Lipoma only); that is **outside this report's scope** and is not shown. Extending it
would need a month-tab mechanism like `halcyon-reports` has — a design change, not a refresh.

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

Frozen **25 Oct 2026, 8:15 am IST**, covering the whole of **4–30 Sep** — the month is
closed, every day is settled, and nothing on the page is still moving.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The final two days of September are what moved the numbers — and they moved them the
wrong way.** 29 and 30 Sep together took ₹2,100.72 of call spend for 38 calls
(₹55.28 each, in line with the month) but only **5 of those 38 held twenty seconds**,
against 24% for the month as a whole. So the headline cost per placed call barely budged
(₹51.08 → ₹51.46) while the cost of a real conversation jumped:

| | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|
| Cost per call placed | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53; read it as
flat for the month. The 20-second rate is the one that ended worse than it started.
Keep both rows in front of the client. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised
for WhatsApp conversations, so both sit outside every per-call figure.

| 29–30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | ₹1,256.97 | 14 | ₹89.78 | 1 |
| Lipoma | ₹843.75 | 24 | ₹35.16 | 4 |

**Only Pain Management is live now.** It closes September as the dearest call line
(₹58.11) but still the one whose calls last: 61 of its 222 (27%) held twenty seconds at
₹211.48 each, and 32 reached a minute — more minute-long calls than every other campaign
on the account put together.

**Lipoma was paused after 30 Sep** and finishes as the cheapest line per call placed by a
wide margin: ₹3,493.24 for **102 calls at ₹34.25**, against ₹56.70 for everything else. Its
calls are short, though — only 21 held twenty seconds (₹166.34, still the account's best)
and just 6 reached a minute.

**Autism, Endoscopy and Kukatpally all closed out unchanged** from the last refresh, with
no late-attributed calls at all: Autism ₹2,131.13 / 42 calls / ₹50.74; Endoscopy
₹3,460.95 / 66 calls / ₹52.44 but only 12 past twenty seconds (**₹288.41 per real
conversation**, the dearest of the call campaigns bar the one-day Kukatpally test);
Kukatpally ₹502.22 / 5 calls / ₹100.44.

**Revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Lipoma +₹3.02, Pain +₹0.77,
Autism +₹0.74); no call counts moved. The 29th, a ₹71.22 part-day when last published,
settled at **₹1,056.20 for 20 calls**. Everything on or before 27 Sep is byte-identical to
the previous snapshot.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each — unchanged
to the paisa. Meta still reports 27 first replies, 13 conversations past one message and
5 past three, and every one of the deep ones is the Gulf ad set. Bengaluru buys a
conversation for ₹160.80 against Gulf's ₹273.88. None of that is on the page: the `DAILY`
row format has no field for messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` is the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently show a
stale day. Now that September is closed there is no part-day to hold back, so `SNAP_DAY`
is `null`: nothing is excluded from the totals, the "so far" tag never renders, and the
card relabels itself "Last day with delivery". Set it back to a date the moment the
report's window includes a live day again.

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and is back
  down to `{4}` (Pain Management) now that Lipoma is paused. Keep it in step with the
  statuses or the "live" tag lies — it is a present-tense claim, so it tracks Meta
  today, not what was ACTIVE during the reporting window.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
