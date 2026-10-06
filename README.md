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

Frozen **6 Oct 2026, 8:10 am IST**, covering **4–30 Sep**. **September is now
complete** — every day in scope is settled, so for the first time there is no
part-day to hold out. `SNAP_DAY` is the empty string and the Yesterday card
reads *Last day of the month*.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The two days that were missing last time are both ordinary on spend and poor
on duration.** 29 Sep settled at ₹1,056.20 for 20 calls (₹52.81) and 30 Sep at
₹1,044.52 for 18 calls (₹58.03) — but between them only **5 of those 38 calls
held twenty seconds**, against a month-long rate of one in four. That is what
moved the 20-second figure ₹203.83 → ₹214.17 while the per-call rate barely
budged.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| **29 Sep** Pain Management | ₹669.68 | 9 | ₹74.41 | 1 |
| **29 Sep** Lipoma | ₹386.52 | 11 | ₹35.14 | 2 |
| **30 Sep** Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |
| **30 Sep** Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |

**Pain Management ended the month badly.** ₹117.46 a call on the 30th is its
dearest day of September by a wide margin (its month average is ₹58.11), on five
calls and none that held. The 29th was already ₹74.41. Two days is not a trend,
but it is the line to watch when October is added.

**Lipoma closed as the cheapest line in the account and never wavered** — ₹35.14
and ₹35.17 on its last two days, ₹34.25 across all nine. Everything else
together ran ₹56.70. It also carries the cheapest real conversation, ₹166.34 per
20-second call.

**Only Pain Management and Lipoma ran to month end.** Autism's last day was the
28th and it is PAUSED; Endoscopy stopped on the 27th and is PAUSED; Kukatpally
(one day, 8 Sep) and NRI Elder Care are PAUSED; WhatsApp stays paused.

**Small revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Lipoma
+₹3.02, Pain +₹0.77, Autism +₹0.74); no call counts moved. The 29th, which was
published as a ₹71.22 part-day, settled at ₹1,056.20 — the part-day guard was
worth having.

**Final per-campaign standings, 4–30 Sep:**

| Campaign | days | spend | calls | per call | 20s | per 20s call |
|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 |
| WhatsApp (msg) | 11 | ₹5,924.79 | — | — | — | — |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | **₹34.25** | 21 | **₹166.34** |
| Endoscopy | 5 | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 |
| NRI Elder Care (web) | 4 | ₹2,686.81 | — | — | — | — |
| Autism | 6 | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 |
| Kukatpally (1-day test) | 1 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged this refresh. Meta still reports 27 first replies, 13 conversations
past one message, 5 past three, 3 past five, and every one of the deep ones is
the Gulf ad set. None of that is on the page; the `DAILY` row format has no
field for messaging depth.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4–22 | 4–24 | 4–26 | 4–27 | 4–28 | 4–30 |
|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53;
read it as flat. The 20-second rate is the one that has drifted, and the final
two days pushed it to its highest reading yet. Keep both rows in front of the
client. Per-call figures cover **call campaigns only**: NRI Elder Care drives
website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

**Out of scope but worth knowing: the account has gone quiet in October.** It
billed ₹989.84 on 1 Oct and ₹537.66 on 2 Oct, then **nothing at all from 3 to 6
Oct**, with Pain Management and Lipoma both still reading ACTIVE. This page is
September-only so nothing here is affected, but somebody should find out whether
that is a deliberate stop or a billing/limit problem before October is reported.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` the last complete day, which is what the Yesterday card
reads. Both are plain constants — move them together on every refresh, or the
card will silently show a stale day. **When the scope has closed and no day in
it is unsettled — as now, with September complete — set `SNAP_DAY` to the empty
string**, never to a real date in `DAILY`: the page excludes `SNAP_DAY` from
every headline, so pointing it at a settled day would silently drop that day
from the totals. With it empty, nothing is excluded, the "so far" tag disappears
and the card relabels itself *Last day of the month*.

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
