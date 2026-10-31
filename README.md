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

Frozen **31 Oct 2026, 11:30 am IST**, covering **4–30 Sep** — the whole month.
September closed a month ago, so **every day in this report is settled**: there is
no part-day to hold out and `SNAP_DAY` is `null`.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month closed on two ordinary days.** The 29th took ₹1,056.20 for 20 calls
(₹52.81 each, 3 over twenty seconds) and the 30th ₹1,044.52 for 18 calls (₹58.03,
2 over twenty seconds) — both from Pain Management and Lipoma alone. The 29th had
been published as a ₹71.22 part-day; it settled nearly fifteen times higher,
which is exactly why a part-day never sets a headline here.

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53 —
read it as flat. The 20-second rate is the one that moved: it closes ₹10.34 above
the 4–28 cut, because the last two days booked 38 calls but only 5 that held.
Lipoma is still holding the per-call average down on its own; excluding it the
month closes at ₹56.70 a call. Keep both rows in front of the client. Per-call
figures cover **call campaigns only**: NRI Elder Care drives website traffic and
the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit
outside every per-call figure.

**Final per-campaign standings (1–30 Sep):**

| Campaign | Days | Spend | Calls | Per call | 20s+ | Per 20s | Status |
|---|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | ACTIVE |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | PAUSED |
| Endoscopy | 5 | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | PAUSED |
| Autism | 6 | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | PAUSED |
| Kukatpally (1-day test) | 1 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | PAUSED |
| NRI Elder Care (web) | 4 | ₹2,686.81 | — | — | — | — | PAUSED |
| NRI + Bengaluru (WhatsApp) | 11 | ₹5,924.79 | — | — | — | — | PAUSED |

**Lipoma finished the cheapest line per call placed by a wide margin** — ₹34.25
against ₹56.70 for everything else — and it held that for its whole nine-day run.
Pain Management carried the month: 21 of the 26 delivering days and 41% of all
spend. It also still has the highest share of calls that last, 61 of 222 (27%)
past twenty seconds.

**Only Pain Management is still ACTIVE at Meta**; `LIVE` is now `new Set([4])`.
Lipoma, which was live at the last cut, reads PAUSED. Autism and Endoscopy never
came back after the 28th and the 27th respectively.

**Revisions since the 29 Sep snapshot.** Meta settled 28 Sep up by ₹4.53 in total
(Autism +₹0.74, Pain +₹0.77, Lipoma +₹3.02); no call counts moved on that day.
Every campaign's day rows now equal Meta's own period totals on spend,
impressions, link clicks, calls placed, 20s and 60s calls, and every day's rows
equal the account's own daily spend and impressions.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged, as the campaign has not run since September. Meta still reports 27
first replies and 13 conversations past one message, and the depth-3 figure
derives as 5. The `messaging_user_depth_5_message_send` key is **no longer
returned** for this campaign, so the earlier "3 past five" cannot be reproduced —
do not restate it without re-deriving it. Bengaluru buys a conversation for
₹160.80 against Gulf's ₹273.88 (unchanged ad-set split, not re-pulled this
refresh). None of that is on the page: the `DAILY` row format has no field for
messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it; it stayed an isolated day for the rest of the month.

## Out of scope: what happened after September

This report is **September only** and stops at the 30th. For context, the account
did keep running: it spent through **24 October** and has booked **nothing since
25 October** (seven consecutive zero days to 31 Oct). None of that is in the
arrays, and adding October means a second month tab, which this page does not
have — `halcyon-reports` is the one built for that. Say so to the client rather
than letting a September-only page imply the account has been quiet all along.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the day that is still accruing and `YDAY` the last complete day,
which is what the Yesterday card reads. Both are plain constants — move them
together on every refresh, or the card will silently show a stale day. **When the
report's window has fully settled, set `SNAP_DAY = null`**: nothing is then held
out of the headlines, and the Yesterday card drops its "still counting" line of
its own accord. Give it a date again only when the last `DAILY` row is a live
part-day.

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
