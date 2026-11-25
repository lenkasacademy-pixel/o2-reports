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

Frozen **25 Nov 2026, 8:15 am IST**. **September 2026 is now a closed month** —
every day on the page is final, nothing is still settling, and the report covers
the full delivery window **4-30 September** (26 days with spend).
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed / 105 lasted 20s / 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

Because the month is shut, `SNAP_DAY` is `null` and `YDAY` is 30 Sep: there is no
part-day to hold out of the totals. The page says so in place of the "still
counting" line.

### What moved since the 29 Sep cut

**The part-day guard earned its keep.** 29 Sep was published as a ₹71.22
part-day; it settled at **₹1,056.20** — fifteen times larger. Pain Management
went ₹43.37 -> ₹669.68 (1 call -> 9) and Lipoma ₹27.85 -> ₹386.52 (2 -> 11).
Had the 29th been allowed into a headline it would have been badly wrong.

30 Sep then added ₹1,044.52 for 18 calls, and the 28th was revised up ₹4.53
(Autism +0.74, Pain +0.77, Lipoma +3.02) with no call counts moving. Nothing
else in 4-27 Sep changed at all.

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30 final** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| ...excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| ...excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh the per-call rate stayed inside ₹49-53 and closed at
₹51.46 — read it as flat for the month. The 20-second call is the one that got
dearer: ₹203.83 -> ₹214.17 on the last two days, because the 29th and 30th
bought 27 calls but only 3 that held twenty seconds. Lipoma is still holding the
average down on its own; without it the month is ₹56.70 a call. Keep both rows in
front of the client. Per-call figures cover **call campaigns only**: NRI Elder Care
drives website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

### Where the month closed, per campaign

| Campaign | Spend | Calls | Each | 20s | Each |
|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 |
| Kukatpally (one day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |
| NRI Elder Care (web) | ₹2,686.81 | — | — | — | — |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | — | — | — | — |

**Lipoma finished cheapest by a wide margin** — ₹34.25 a placed call against
₹56.70 for everything else, and it also had the cheapest 20-second call at
₹166.34. It ran only 23-30 Sep and is now PAUSED. If one line is worth
restarting, it is this one.

**Pain Management is the only campaign still ACTIVE** (`LIVE` is now just index 4).
It was the dearest call line at ₹58.11 but holds callers best in absolute terms:
61 of its 222 calls (27%) reached twenty seconds and 32 reached a minute — more
60-second calls than the rest of the account put together.

**Autism and Endoscopy both closed paused** and did not spend again after the
28th and 27th respectively. Endoscopy stays the dearest real conversation of the
call campaigns bar Kukatpally: ₹288.41 per 20-second call.

**WhatsApp is unchanged** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
no late attribution moved it. Depth this refresh: 29 total messaging connections,
27 first replies, 13 conversations past one message, 5 past three. Meta no longer
returns a `messaging_user_depth_5_message_send` key for this campaign, so the
"3 past five" figure from the 29 Sep cut is not reproducible now and has been
dropped rather than restated as zero. The Bengaluru/Gulf ad-set split
(₹160.80 vs ₹273.88) is unchanged because the campaign totals are. None of this
is on the page: the `DAILY` row format has no field for messaging depth.

**NRI Elder Care still shows nothing for its own goal.** ₹2,686.81 over four days
(4-6 and 10 Sep), 39 link clicks, and the `HEnquiry` website event reports no
conversions at all. The page already flags this as a warning card. Unresolved
since the first snapshot.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Still unexplained; delivery was
normal on either side of it.

## Out of scope, and a human should decide

**This account spent ₹18,476.76 in October 2026** (283,130 impressions) and that
spend is **not on this page**. The report's scope is September 2026 only — fixed by
this README and by the refresh brief — so October was deliberately left out rather
than silently folded into a page titled "September 2026".

November 2026 is ₹0.00 to date: the account has not spent since October.

If the client should see October, it needs a decision about shape: either a month
tab bar like `halcyon-reports`, or a second page. Do not just extend `DAILY` — the
masthead, eyebrow, footer and the "September is closed" line all say September.


## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still running**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently
show a stale day. With September closed there is no part-day, so `SNAP_DAY` is
`null`: the totals filter then drops nothing, the day table tags nothing "so far",
and the card heading and sub-line switch to their closed-month wording. Set
`SNAP_DAY` back to a date the moment this page is ever pointed at a live month.

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
- Update the snapshot date in `index.html` — **four places**: the line-8 title
  comment, the masthead stamp, the footer, and the `baked figures` comment above
  `CAMPS` — and here.
- Re-pull the whole month even now that it is closed. The 29 Sep part-day settled
  up 15x and 30 Sep appeared only on this refresh; appending would have missed both.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
