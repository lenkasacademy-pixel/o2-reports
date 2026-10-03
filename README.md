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

Frozen **3 Oct 2026, 8:10 am IST**, covering **4-30 Sep - September is now
complete**, so for the first time there is no part-day to exclude and every day
in the month counts toward the headline.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month closed on two campaigns and a dear last day.** 30 September took
₹1,044.52 for 18 calls at **₹58.03**, only 2 of them over twenty seconds. Pain
Management is the reason: ₹587.29 for 5 calls, **₹117.46 each**, its worst day of
the month by a wide margin, and Meta returns **no
`click_to_call_native_20s_call_connect` key at all** for it - 5 calls, not one
held twenty seconds. That is a genuine zero, not a missing field. Lipoma ran
normally at ₹35.17 a call.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |
| Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |

**29 September settled far above its part-day.** It was published as ₹71.22 for
3 calls; complete it is **₹1,056.20 for 20 calls** (Pain 9, Lipoma 11) at ₹52.81.
That is the part-day guard earning its keep - had the 29th set a headline it
would have read ₹23.74 a call.

**Meta also revised 28 September up by ₹4.53** after publication (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02); impressions and reach moved with it, call counts
did not. Days 1-27 came back byte-identical.

**Autism and Endoscopy are closed out.** Both stayed paused and spent nothing
after the 28th. Autism finishes at ₹2,131.13 for 42 calls (₹50.74 each), 10 over
twenty seconds at ₹213.11. Endoscopy finishes at ₹3,460.95 for 66 calls
(₹52.44 each) but only 12 held twenty seconds, **₹288.41 per real
conversation** - the dearest of the call campaigns bar the one-day Kukatpally
test.

**Only Pain Management and Lipoma are live.** Pain closes September at
₹12,900.47 for 222 calls, ₹58.11 each, with the highest share of calls that
last: 61 of 222 (27%) held twenty seconds, ₹211.48 each. Lipoma is the cheapest
line per call placed all month - ₹3,493.24 for **102 calls at ₹34.25**, with 21
over twenty seconds at ₹166.34, the best 20-second rate on the account.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each -
re-pulled this refresh and unchanged. Meta also reports how far each went: 27
first replies, 13 conversations past one message, 5 past three, 3 past five -
and every one of the deep ones is the Gulf ad set. Bengaluru buys a conversation
for ₹160.80 against Gulf's ₹273.88. None of that is on the page yet; the `DAILY`
row format has no field for messaging depth.

**Read the headline carefully - Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Both rates ticked up on the final two days, driven by Pain Management's 29th and
30th. Across every refresh recorded here the per-call rate has stayed inside
₹49-₹53; read it as flat. Excluding Lipoma the account sits at ₹56.70 a call.
Keep both rows in front of the client. Per-call figures cover **call campaigns
only**: NRI Elder Care drives website traffic and the NRI + Bengaluru campaign
optimised for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** - the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

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
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
