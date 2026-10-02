# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (from 4 Sep, the first day with delivery).
**The month is now complete** — 1-30 Sep, every day settled, no part-day in the window.

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

Frozen **2 Oct 2026, 8:06 am IST**, covering **4-30 Sep — the whole month, every
day settled**. There is no part-day in this window: 1 October onward is out of
scope, so `SNAP_DAY` is `null` and nothing is held back from the headlines.
Ad spend ₹31,098.64 + 18% GST ₹5,597.76 = **₹36,696.40 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.16 per call that actually held 20 seconds**.

**September closes dearer than it read on the 28th, and Pain Management is why.**
Cost per call placed went ₹51.08 → **₹51.46** and the 20-second call
₹203.83 → **₹214.16**. The last two days added ₹2,099.75 of call spend and
38 calls but only 3 that held twenty seconds.

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep — Pain Management | ₹669.68 | 9 | ₹74.41 | 1 |
| 29 Sep — Lipoma | ₹386.52 | 11 | ₹35.14 | 2 |
| 30 Sep — Pain Management | ₹587.29 | 5 | **₹117.46** | 0 |
| 30 Sep — Lipoma | ₹456.26 | 13 | ₹35.10 | 2 |

**₹117.46 is Pain Management's dearest day of the month** — five calls on
₹587.29, against a campaign average of ₹58.11. Its daily rate ran ₹62.59 ->
₹63.18 → ₹74.41 → **₹117.46** over its last four days. Four days is not a
trend, but it is the steepest run the campaign has had, and it is the only reason
both headline rates moved up. Worth checking the creative and the audience before
October's budget follows it.

**Lipoma did not move at all.** ₹35.14 and ₹35.10 on the last two days, either
side of its ₹34.24 month average. It closes September at **₹3,492.27 for 102
calls, ₹34.24 each**, against ₹56.70 for every other call campaign — eleven
days running as the cheapest line, and still the only thing holding the account
average under ₹52.

**Both live campaigns are still live, and both are running in October.** Pain
Management and Lipoma are the only ACTIVE campaigns (`LIVE` = indexes 4 and 6).
On 1 Oct they took ₹647.78 (7 calls) and ₹334.33 (11 calls); 2 Oct is a
part-day at ₹4.53 and ₹10.35. None of that is on this page — the scope is
September — so **October needs its own tab or its own scope decision** before the
next refresh, the way `halcyon-reports` handles months.

**Pain Management closes as the dearest line per call but the best at holding
one.** ₹12,900.47 for 222 calls (₹58.11), and 61 of those 222 (27%) held
twenty seconds at ₹211.48 — a better 20-second rate than Endoscopy
(₹288.41) or Autism (₹213.11) despite the dearer placed call. 32 held a full
minute, ₹403.14 each, the best 60-second rate on the account.

**Autism and Endoscopy are closed and paused.** Autism ends at ₹2,131.13 for
42 calls (₹50.74), 10 over twenty seconds at ₹213.11; it spent nothing after
the 28th. Endoscopy ends at ₹3,460.95 for 66 calls (₹52.44) but only 12 held
twenty seconds, **₹288.41 per real conversation** — the dearest of the call
campaigns bar the one-day Kukatpally test.

**Revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Autism +₹0.74,
Pain +₹0.77, Lipoma +₹3.02); no call counts moved. The 29th, a part-day at
₹71.22 for 3 calls when it was last published, settled at **₹1,056.20 for 20
calls** — the clearest reminder yet of why the part-day is kept out of headlines.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each,
unchanged on this pull. Meta also reports how far each went: 27 first replies, 13
conversations past one message, 5 past three, 3 past five — and every one of the
deep ones is the Gulf ad set. Bengaluru buys a conversation for ₹160.80 against
Gulf's ₹273.88. None of that is on the page yet; the `DAILY` row format has no
field for messaging depth.

**Read the headline carefully — Lipoma is still doing the work:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.16** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49-53;
read it as flat for the month. The 20-second rate is the one that has drifted —
₹181 at its best on the 24th, ₹214.16 at the close. Keep both rows in front of
the client. Per-call figures cover **call campaigns only**: NRI Elder Care drives
website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day **when the window has one**, and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.
Now that September is closed `SNAP_DAY` is `null`: the filter that drops it
matches nothing, so every day counts, the "so far" tag disappears, and the card
reads *Last day of the month* instead of *Yesterday*. **Set `SNAP_DAY` back to a
date the moment a part-day enters the data** — never leave a day that is still
accruing inside the totals.

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
