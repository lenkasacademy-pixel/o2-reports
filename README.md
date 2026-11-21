# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** — 4–30 Sep (4 Sep is the first day with delivery).
The month is complete and every day on the page is settled.

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **Yesterday** card (the last complete day) with that day's billed amount,
  calls, 20s calls and cost per call, broken out by campaign. When the month is
  closed and `SNAP_DAY` is `null` the same card is titled **"Last day of the
  month"** instead, because calling 30 September "yesterday" in November is a lie.

## Snapshot

Frozen **21 Nov 2026, 8:15 am IST**, covering **4–30 Sep — the whole month, every
day settled**. September closed long ago, so for the first time this report
excludes nothing: `SNAP_DAY` is `null` and all 30 days are in every headline.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The month is closed. What the last cut was missing was two ordinary days.**
The 4–28 Sep window published on 29 Sep has been revised up by only **₹4.53** in
total and its call count has not moved at all (399, exactly as published). The
whole difference in the headline is the two days that were still to come:
29 Sep settled at ₹1,056.20 for 20 calls and 30 Sep at ₹1,044.52 for 18 — both
Pain Management and Lipoma only. On the old snapshot the 29th read "₹71.22 for
3 calls" because it was 11am; it finished fifteen times larger. That is the
part-day rule earning its keep.

| Final figures, Sep 2026 | spend | calls | each | 20s+ | per 20s call | last day |
|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | 30 Sep |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | **₹166.34** | 30 Sep |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | 27 Sep |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | 28 Sep |
| Kukatpally (one day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | 8 Sep |
| WhatsApp (conversations) | ₹5,924.79 | — | — | — | — | 22 Sep |
| NRI Elder Care (website) | ₹2,686.81 | — | — | — | — | 10 Sep |

**Lipoma finished the month as the cheapest line by a wide margin** — ₹34.25 a
call against ₹56.70 for every other call campaign put together, and ₹166.34 per
20-second call, the best on the account. It ran to the last day of the month and
is now PAUSED.

**Only Pain Management is still ACTIVE at Meta**, so `LIVE` is down to one index
(it was `{4, 6}`; Lipoma has since been paused). Pain Management closed September
at ₹58.11 a call with the highest share of calls that last: 61 of 222 (27%) held
twenty seconds.

**Both headline rates finished slightly worse than the 4–28 cut read:** cost per
call ₹51.08 → **₹51.46**, the 20-second call ₹203.83 → **₹214.17**. Across every
refresh recorded here the per-call rate has stayed inside ₹49–₹53; read it as flat
for the month.

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |

Keep both per-call rows in front of the client. Per-call figures cover **call
campaigns only**: NRI Elder Care drives website traffic and the NRI + Bengaluru
campaign optimised for WhatsApp conversations, so both sit outside every per-call
figure.

**⚠ The account has delivered nothing since 24 October.** October ran 1–2 Sep-style
days, paused 3–5 Oct, ran 6–24 Oct, and has spent ₹0.00 every day from 25 Oct to
21 Nov — four weeks dark — even though Pain Management still reads ACTIVE. That is
outside this report's September scope and is deliberately not on the page, but it
is the first thing to raise with the client. Check the account spending limit and
the payment method.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged. Meta still reports 27 first replies, 13 conversations past one message
and 5 past three; the "past five" key it used to return is no longer in the
response, so treat that figure as unavailable rather than zero. Bengaluru buys a
conversation for ₹160.80 against Gulf's ₹273.88. None of that is on the page: the
`DAILY` row format has no field for messaging depth.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data (a part-day) and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.
**Once the month is complete, set `SNAP_DAY = null`** and point `YDAY` at the last
day of the month: with no live part-day there is nothing to hold out, and leaving
a stale date in `SNAP_DAY` would drop a real settled day from every total. The
page keys its "so far" tag and its exclusion filter off `SNAP_DAY`, so `null` is
all it takes.

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
