# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery). The month is
now **complete and fully settled** — the account went on running into October, but that
spend is deliberately out of scope for this page.

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

Frozen **12 Oct 2026, 8:05 am IST**, covering **4-30 Sep — the whole month, every
day settled**. Nothing is held back as a part-day any more (see below).
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September is closed, so `SNAP_DAY` is now `null`.** Every previous refresh ran while
the month was still live, so the last row was an unsettled part-day and the page held it
out of every headline. There is no such day left: 30 Sep settled twelve days ago. With
`SNAP_DAY = null` the filter `R.filter(r => r[1] !== SNAP_DAY)` drops nothing, the
"so far" tag never renders, and the full month sets the headline — which is the point of
the guard, not the opposite of it. The Yesterday card reads "Last day of the month"
instead of "Yesterday" while `SNAP_DAY` is null. **Set `SNAP_DAY` back to a date string
the moment an unsettled day enters the data** and both behaviours revert untouched.

**The two days that were still open at the last refresh both came in full.** 29 Sep was
read as ₹71.22 for 3 calls when it was hours old; it settled at **₹1,056.20 for 20
calls** (₹52.81 each). 30 Sep closed the month at ₹1,044.52 for 18 calls (₹58.03). Meta
also revised 28 Sep up ₹4.53 after publication (Autism +₹0.74, Pain +₹0.77, Lipoma
+₹3.02); no call counts moved.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |
| Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |

**The 20-second call got dearer in the last two days, and the 60-second call with it.**
₹203.83 → **₹214.17** per 20s call, ₹478.47 per 60s call. The two closing days bought 38
calls but only 5 that held twenty seconds, and Pain Management's last day booked
₹587.29 for 5 calls and **not one** over 20s. Cost per call placed moved much less
(₹51.08 → ₹51.46) — the volume held up, the duration did not. Worth putting to the
client as the month's one soft note.

**Only Pain Management and Lipoma ran to the end of the month**, and both are still
ACTIVE at Meta. Everything else is PAUSED: Autism and Endoscopy stopped on the 28th and
27th, WhatsApp on the 22nd, NRI Elder Care and the one-day Kukatpally test long before.

Final per-campaign standings for the month:

| Campaign | days | spend | calls | each | 20s | per 20s |
|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | **₹34.25** | 21 | **₹166.34** |
| Endoscopy | 5 | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 |
| Autism | 6 | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 |
| Kukatpally (1-day test) | 1 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |
| NRI Elder Care (website) | 4 | ₹2,686.81 | — | — | — | — |
| WhatsApp (messaging) | 11 | ₹5,924.79 | — | — | — | — |

**Lipoma finished the cheapest line on the account by a wide margin** and held it to the
last day: ₹34.25 a call placed and ₹166.34 per 20-second call, against ₹56.70 and
₹226.13 for every other call campaign put together. It ran only nine days. If one thing
goes into October's plan, it is more of this.

**Pain Management carried the month** — 21 of the 27 delivery days and 41% of all ad
spend — at ₹58.11 a call, the dearest of the three real lines but with the best
duration: 61 of its 222 calls (27%) held twenty seconds and 32 held a minute,
₹403.14 each, the cheapest minute-long call on the account.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal on either side of it.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged, it has not spent since 22 Sep. Meta still reports the same depth:
27 first replies, 13 conversations past one message, 5 past three, 3 past five — and
every one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for
₹160.80 against Gulf's ₹273.88. None of that is on the page: the `DAILY` row format has
no field for messaging depth.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate stayed inside ₹49-₹53 and it closed
the month at ₹51.46 — read it as flat. Keep both rows in front of the client: excluding
Lipoma the account sits at ₹56.70 a call. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised
for WhatsApp conversations, so both sit outside every per-call figure.

## Reconciliation on this refresh

Campaign sums equal the `level: "ad_account"` daily totals on **spend, impressions and
link clicks for all 26 delivery days**, and each campaign's period total equals its own
no-`time_increment` pull on spend, impressions, link clicks and calls placed. Every
20s/60s derivation divided to a whole number — no exceptions. No mismatch anywhere.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the part-day at the end of the data and `YDAY` the last complete day,
which is what the Yesterday card reads. Both are plain constants — move them together on
every refresh, or the card will silently show a stale day. **When the month in scope has
closed there is no part-day: set `SNAP_DAY = null`** so the whole month counts toward the
headlines, and point `YDAY` at the last day in scope. The two card strings that name
`SNAP_DAY` are guarded on it, so they read correctly either way.

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
- Recent days keep settling for ~48h; re-pull the whole month rather than appending. This
  refresh is the proof: 29 Sep was published at ₹71.22/3 calls and settled at
  ₹1,056.20/20 calls, and 28 Sep moved ₹4.53 after publication.
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
