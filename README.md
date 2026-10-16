# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery; the month is
now complete through 30 Sep).

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

Frozen **16 Oct 2026, 8:05 am IST**, data window **4–30 September — the month is
now closed**. Every day in the data has settled, so for the first time there is no
part-day to exclude: `SNAP_DAY` is `null` and all 26 delivery days count towards
the headline (see *Refreshing* below).
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September closed slightly dearer than the 4–28 cut read.** The last two days
were the two most expensive of the month's end: the 29th took ₹1,056.20 for 20
calls (₹52.81) and the 30th ₹1,044.52 for 18 calls (₹58.03), against a
month average of ₹51.46. Both rates moved up from the previous refresh —
cost per call ₹51.08 → **₹51.46**, the 20-second call ₹203.83 → **₹214.17**.
The 20-second rate moved most because those two days bought ₹2,100 of spend and
only 5 calls that held twenty seconds.

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53;
read the month as flat. Lipoma held the average down on its own to the end —
excluding it the account sits at ₹56.70 a call. Keep both rows in front of the
client. Per-call figures cover **call campaigns only**: NRI Elder Care drives
website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

**Down to one live campaign.** Pain Management is the only campaign still ACTIVE
at Meta; Lipoma Removal is now PAUSED, as are Autism, Endoscopy, Kukatpally,
NRI Elder Care and WhatsApp. `LIVE` is `{4}`.

**Final per-campaign standing (full month, ex-GST).**

| Campaign | Spend | Calls | Each | 20s+ | Each | 60s+ | Each |
|---|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 32 | ₹403.14 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | 6 | ₹582.21 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 4 | ₹865.24 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 4 | ₹532.78 |
| Kukatpally (one-day test) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 1 | ₹502.22 |
| NRI Elder Care (website) | ₹2,686.81 | — | — | — | — | — | — |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | — | — | — | — | — | — |

**Lipoma finished the cheapest line per call placed, and never lost that spot**
— ₹34.25 against ₹56.70 for everything else. It is also the second-best line on
calls that hold twenty seconds (₹166.34), behind nothing but its own headline.
Pain Management remains the line whose calls last: 61 of its 222 (27%) held
twenty seconds and 32 (14%) held a minute, the best 60-second share on the
account.

**Revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Lipoma +₹3.02,
Pain +₹0.77, Autism +₹0.74); no call counts moved. The 29th, a ₹71.22 part-day
when last published, settled at ₹1,056.20 for 20 calls. 30 Sep is new.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged from the previous refresh. Re-pulled depth this refresh: 27 first
replies, 13 conversations past one message, 5 past three. (The
`messaging_user_depth_5_message_send` key that gave "3 past five" last time is
no longer returned for this campaign; treat that bucket as unknown, not zero.)
Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of that
is on the page: the `DAILY` row format has no field for messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal from the 19th to the end of the month.

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
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer),
  the baked-figures comment above `CAMPS`, and here.
- `SNAP_DAY` is the live part-day and is excluded from every headline. **September is
  closed, so it is now `null`** and `YDAY` is `2026-09-30`. The page derives
  `partDay = SNAP_DAY && R.some(...)`, so with `null` nothing is dropped, the "so far"
  tag disappears and the Yesterday card becomes a "Final day" card. If this report is
  ever re-opened against a live window, set `SNAP_DAY` back to that part-day and the
  old behaviour returns on its own — do not re-point it at a settled day just to have
  a value, or a good day silently vanishes from the totals.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
