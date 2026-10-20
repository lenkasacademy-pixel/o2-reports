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
  calls, 20s calls and cost per call, broken out by campaign. It titles itself
  **Final day** once the month is closed and there is no part-day left to exclude.

## Snapshot

Frozen **20 Oct 2026, 8:20 am IST**. **September is now closed**, so this report
covers the complete month, **4–30 September** — every day on the page is fully
settled and there is no part-day. `SNAP_DAY` is therefore `null`.

Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. **₹51.46 per call placed** and
**₹214.17 per call that actually held 20 seconds**.

### ⚠ The account is still running, but this report stops at 30 September

The scope of this page is September only, by design. Since then the account has
spent **₹15,834.18 over 1–19 October** and is still live (₹9.27 so far on the 20th),
with a three-day gap at 3–5 Oct when it spent nothing at all. **None of that is on
this page.** If the client wants October, the cleanest change is a month tab bar like
`halcyon-reports` has — that is a real feature decision, not a refresh, so it has
deliberately not been made here.

### How the month closed

The last two days of September were ordinary and almost identical in size:

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

**Both headline rates edged up as the month closed.** Cost per call placed
₹51.08 → **₹51.46**; the 20-second call ₹203.83 → **₹214.17**. The last two days
added ₹2,034.03 of call spend and 38 calls, but only 5 more 20-second calls — which
is what moved the duration rate. Across every refresh recorded here the per-call rate
has stayed inside ₹49–₹53; read it as flat.

**The 29 Sep part-day is the reason the part-day rule exists.** When it was published
as a live day it read ₹71.22 for 3 calls. Settled, it is **₹1,056.20 for 20 calls** —
fifteen times the spend. Nothing about the page's headline numbers moved at the time,
because the part-day was already excluded from them.

**Only Pain Management is live now.** Lipoma Removal is **PAUSED** at Meta, so `LIVE`
is down to the single index `4`. Lipoma still closes as the cheapest line on the
account by a distance: ₹3,493.24 for **102 calls at ₹34.25**, against ₹56.70 for
everything else. Excluding Lipoma the account sits at **₹56.70 a call** — keep both
rows in front of the client.

**Autism and Endoscopy stayed shut.** Autism closed at ₹2,131.13 for 42 calls
(₹50.74) and Endoscopy at ₹3,460.95 for 66 calls (₹52.44), of which only 12 held
twenty seconds — ₹288.41 per real conversation, the dearest of the call campaigns bar
the one-day Kukatpally test. Meta revised Autism up by ₹0.74 after publication; no
call counts moved.

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged since 22 Sep. Meta also reports how far each went: 27 first replies, 13
conversations past one message, 5 past three. None of that is on the page; the `DAILY`
row format has no field for messaging depth. Per-call figures cover **call campaigns
only**: NRI Elder Care drives website traffic and the NRI + Bengaluru campaign
optimised for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal on either side of it.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently show
a stale day. **When the month is closed there is no part-day: set `SNAP_DAY = null`.**
The page then keeps every day in its totals, drops the "so far" tag, and the card
titles itself *Final day* instead of *Yesterday*.

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and dropped
  back to the single index `4` on the 20 Oct refresh when Lipoma was paused. Keep it
  in step with the statuses or the "live" tag lies.
- **List campaigns with `effective_status IN [..., "ARCHIVED", "DELETED"]`**, the same
  way `halcyon-reports` does. An unfiltered listing omits them silently. On this
  account `O2 Guardian | NRI Elder Care | CTWA | v1` is ARCHIVED at zero spend, so it
  changes nothing today — but a non-zero one would look like a Meta data gap.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
