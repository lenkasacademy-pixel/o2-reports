# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery, through 30 Sep).
The month is complete — see *October is live* below for what that now leaves out.

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

Frozen **30 Oct 2026, 8:15 am IST**, covering **4–30 Sep — the complete month**.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September is closed, so nothing on this page is provisional any more.** Every one
of the 27 delivery days is settled, which is why `SNAP_DAY` is now `null` rather than
a date: there is no live part-day to hold out of the headlines. The guard itself is
unchanged and still fires the moment `SNAP_DAY` names a day again. `YDAY` is 30 Sep,
the last day of the month, and the Yesterday card reads it.

**The two days the previous cut could not see.** 29 Sep was published as a ₹71.22
part-day; it settled at **₹1,056.20 for 20 calls**. 30 Sep closed the month at
₹1,044.52 for 18 calls. Together they added ₹2,100.72 and 38 calls.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |
| Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |

**Pain Management had a poor last two days** — ₹74.41 a call on the 29th and
₹117.46 on the 30th against its ₹58.11 month average — while Lipoma closed strongly
at ₹35.14 and ₹35.17. That split is what moved both headline rates up.

**Small revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Lipoma +₹3.02,
Pain +₹0.77, Autism +₹0.74); no call counts moved.

**Only Pain Management is still ACTIVE.** Lipoma is now PAUSED, so every other
campaign on the account is closed. Final positions:

| Campaign | Spend | Calls | Cost / call | 20s | Cost / 20s |
|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 |
| Kukatpally (1 day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |

**Lipoma ended the cheapest line per call placed, by a distance** — ₹34.25 against
₹56.70 for everything else. It is also the reason the blended rate looks as good as
it does; keep both rows in front of the client.

**Read the headline carefully — Lipoma is still carrying the average:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Both rates rose on the final two days after two refreshes of falling. Across every
refresh recorded here the per-call rate has stayed inside ₹49–₹53; read it as flat.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website traffic
and the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit
outside every per-call figure.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unmoved this refresh. Meta still reports 27 first replies, 13 conversations past one
message and 5 past three. (The "past five" depth key is no longer returned for this
campaign, so that figure is not re-verifiable; it was 3 when last pulled.) None of
this is on the page: the `DAILY` row format has no field for messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## October is live and is NOT on this page

The report's scope is September only, so **₹18,476.76 of October delivery is not
shown anywhere on it**. 1–24 October ran Pain Management (₹14,020.41, 162 calls) and
Lipoma (₹4,456.35, 111 calls) — **273 calls at ₹67.68 blended, a third dearer than
September's ₹51.46**. There was no delivery on 3–5 Oct, and **the account has spent
nothing since 25 October** (six days dark as of this refresh); Lipoma now reads PAUSED
while Pain Management is still ACTIVE.

Two decisions for a human, neither taken here:

1. **Widen the scope to a month tab bar** (as `halcyon-reports` already has) or cut a
   separate October page. A client-facing page stamped today that stops on 30 September
   understates the account by ₹18,477 and hides a materially worse cost per call.
2. **Find out why delivery stopped on 25 October.** Nothing in this refresh explains
   it; check the prepaid balance and the account spending limit first.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still accruing**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently show
a stale day. When the reporting month has closed and every day is settled, set
`SNAP_DAY = null`: nothing is then held out of the totals, the “so far” tag stops
rendering, and the Yesterday card says the month is final instead of naming a
part-day. Do **not** leave a settled day in `SNAP_DAY` — it would drop a real day of
spend and calls out of every headline.

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
