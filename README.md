# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** - 4-30 Sep, the month's full run of delivery,
now complete and fully settled.

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

Frozen **26 Nov 2026, 8:15 am IST**. **September is closed.** The window is the
month's full run of delivery, **4-30 Sep**, and every day in it is settled - there
is no part-day in this cut, so `SNAP_DAY` is empty and nothing is excluded.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**This refresh closes the month.** The previous cut stopped at the 28th because the
29th was a live part-day showing only ₹71.22. Both remaining days have settled:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

Only Pain Management and Lipoma ran on those two days. **They were weak on duration** -
38 calls but only 5 held twenty seconds - which is why closing the month moved the
headline the way it did: cost per call placed ₹51.08 -> **₹51.46**, but the
20-second call ₹203.83 -> **₹214.17** and the minute-long one ₹443.10 -> **₹478.47**.
The month got slightly dearer per call and noticeably dearer per real conversation.

**Meta revised the already-published 4-28 window up by ₹4.53** (Autism's 28 Sep
+₹0.74 to ₹495.44, the rest spread thinner). **No call count moved** - 399 placed,
100 at 20s and 46 at 60s for 4-28 are exactly as published.

**Final per-campaign standings (4-30 Sep, ex-GST):**

| Campaign | days | spend | calls | 20s | 60s | per call | per 20s |
|---|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | 61 | 32 | ₹58.11 | ₹211.48 |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | 21 | 6 | **₹34.25** | **₹166.34** |
| Endoscopy | 5 | ₹3,460.95 | 66 | 12 | 4 | ₹52.44 | ₹288.41 |
| Autism | 6 | ₹2,131.13 | 42 | 10 | 4 | ₹50.74 | ₹213.11 |
| Kukatpally (one-day test) | 1 | ₹502.22 | 5 | 1 | 1 | ₹100.44 | ₹502.22 |
| NRI Elder Care (website) | 4 | ₹2,686.81 | — | — | — | — | — |
| NRI + Bengaluru (WhatsApp) | 12 | ₹5,924.79 | — | — | — | — | — |

**Lipoma finished as the cheapest line in the account and by a wide margin** -
₹34.25 a call against ₹56.70 for every other call campaign put together, and
₹166.34 per 20-second call against ₹226.13. It ran only nine days. If the account
comes back, this is the line to come back with.

**Only Pain Management is still ACTIVE at Meta;** every other campaign reads PAUSED,
Lipoma included (it was still live at the last cut, so `LIVE` is now just `{4}`).

**The account stopped spending on 24 October and has not spent since.** October took
₹18,476.76 across 21 days with delivery, then nothing: zero spend and zero
impressions every day from 25 Oct through 26 Nov. That is outside this report's
September scope and no September figure depends on it, but the client should not be
told "the campaigns are running" - they are not. If October onward should be
reported, this page needs a month tab bar the way `halcyon-reports` has one.

**WhatsApp closed at ₹5,924.79 for 27 conversations, ₹219.44 each** - unchanged, and
the depth split still reproduces exactly: 27 first replies, 13 past one message,
5 past three. Every deep one is the Gulf ad set. Still not on the page; the `DAILY`
row format has no field for messaging depth.

**18 September remains unexplained** - the whole account spent ₹6.43 that day on
122 impressions with both campaigns ACTIVE. Kept on the record because nobody has
accounted for it.

Per-call figures cover **call campaigns only**: NRI Elder Care drives website traffic
and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit
outside every per-call figure.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day, excluded from every headline, and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.
**When the month is closed there is no part-day: set `SNAP_DAY` to `""`** and every
day counts. Do not leave a settled day sitting in `SNAP_DAY` — it would be dropped
from the totals. `YDAY` is then the last day of the month.

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
