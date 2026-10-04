# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4–30 Sep; 4 Sep is the first day with delivery).

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

Frozen **4 Oct 2026, 7:00 am IST**, covering **4–30 Sep — September is now
complete**, so for the first time every day in this report is settled and
nothing is excluded.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**There is no part-day in this cut, so `SNAP_DAY` is `null`.** The page's
part-day guard is keyed off that constant: with it null nothing is filtered out,
no row gets the *so far* tag, and the Yesterday card relabels itself "Last day
of the month" and says September is closed. Set `SNAP_DAY` back to a date the
moment the report's window reaches into a live day again.

**The account did not stop at the end of September — the scope did.** Meta shows
₹989.84 on 1 Oct and ₹537.66 on 2 Oct, then nothing on the 3rd or 4th. That
October spend is deliberately outside this report; if the client wants it, the
page needs an October scope, not an extra row.

**The last three days of the month got steadily dearer** as Pain Management's
calls thinned out:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 28 Sep | ₹1,563.50 | 32 | ₹48.86 | 8 |
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

On the 30th Pain Management took ₹587.29 for **5 calls (₹117.46 each, none over
20s)** against Lipoma's ₹457.23 for 13 (₹35.17). One day at that volume is noise,
but it is the dearest day Pain Management has had, and it is the line carrying
the budget.

**Autism closed for good on 28 September.** It is PAUSED and spent nothing on the
29th or 30th, finishing at ₹2,131.13 for 42 calls (₹50.74 each), 10 of them over
twenty seconds (₹213.11 per real conversation).

**Endoscopy stayed paused** and closes unchanged at ₹3,460.95 for 66 calls
(₹52.44 each), only 12 past twenty seconds — **₹288.41 per real conversation**,
the dearest of the call campaigns bar the one-day Kukatpally test.

**Only Pain Management and Lipoma were still live at month end.** Pain Management
finished at ₹12,900.47 for 222 calls (₹58.11), with 61 over twenty seconds
(₹211.48) and 32 over sixty (₹403.14) — still the best duration profile on the
account.

**Lipoma stayed the cheapest line per call placed, every single day it ran** —
₹3,493.24 for **102 calls at ₹34.25**, against ₹56.70 for everything else. It
also had the month's best last week, and on the 30th it bought more than twice
Pain Management's calls for less money.

**Revisions this refresh.** Meta settled 27 Sep unchanged and nudged 28 Sep up by
₹4.53 in total (Autism +₹0.74, Pain +₹0.77, Lipoma +₹3.02); no call or duration
counts moved. The 29th, published as a ₹71.22 part-day with 3 calls, settled at
₹1,056.20 with 20 — which is exactly the reason the part-day is excluded.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each.
Meta also reports how far each went: 27 first replies, 13 conversations past one
message, 5 past three, 3 past five — and every one of the deep ones is the Gulf
ad set. Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of
that is on the page yet; the `DAILY` row format has no field for messaging depth.

**Read the headline carefully — the whole improvement is the new campaign:**

| | 4–22 | 4–24 | 4–26 | 4–28 | 4–29 | 4–30 |
|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹49.39 | ₹52.12 | ₹51.10 | ₹51.18 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹52.64 | ₹56.01 | ₹55.26 | ₹55.78 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹181.34 | ₹209.78 | ₹203.87 | ₹208.19 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹194.87 | ₹226.53 | ₹213.71 | ₹219.14 | **₹226.13** |

Both rates have now risen for two refreshes running. Across every refresh
recorded here the per-call rate has stayed inside ₹49–₹53, so read it as flat;
the 20-second rate has not — it is up 15% on the 24th's ₹181.34 and is the
number to watch. Lipoma is still holding the average down on its own; excluding
it the account sits at ₹56.70 a call. Keep both rows in front of the client.
Per-call figures cover **call campaigns only**: NRI Elder Care drives website
traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations,
so both sit outside every per-call figure.

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
card will silently show a stale day. When the window contains no live day at all
(as now, with September closed), set `SNAP_DAY = null`: the page then counts
every row and says so, instead of dropping a settled day from the headlines.

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
