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

Frozen **17 Nov 2026, 8:15 am IST**. **September 2026 is now a closed, fully
settled month** — data window **4–30 September** (1–3 and 7 Sep had no delivery).
There is no part-day any more, so `SNAP_DAY` is empty and nothing is held out of
the headline; `YDAY` is 30 Sep, the last day of the month.

Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. **₹51.46 per call placed** and
**₹214.17 per call that actually held 20 seconds** (₹478.47 per 60-second call).

**The two days the previous cut could not see closed the month quietly.** 29 Sep was
published as a part-day at ₹71.22; it settled at **₹1,056.20 for 20 calls** (₹52.81
each). 30 Sep took ₹1,044.52 for 18 calls at ₹58.03. Only Pain Management and Lipoma
were still delivering by then.

| Campaign | Spend | Calls | Per call | 20s | 60s |
|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | 32 |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | 6 |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | 4 |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | 4 |
| Kukatpally (one day) | ₹502.22 | 5 | ₹100.44 | 1 | 1 |
| *WhatsApp (msg)* | *₹5,924.79* | *27 conv.* | *₹219.44* | — | — |
| *NRI Elder Care (web)* | *₹2,686.81* | — | — | — | — |

**Only Pain Management is still ACTIVE at Meta** (`LIVE` is now the single index 4).
Lipoma was paused after September, so `LIVE` went from `{4, 6}` to `{4}`.

**Lipoma held the average down to the end.** ₹34.25 a call against ₹56.70 for
everything else; it was the cheapest line per call placed every single day it ran.
Keep both rows in front of the client.

**Read the headline carefully — the whole improvement is the new campaign:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30 (final)** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every cut recorded here the per-call rate stayed inside ₹49–₹53; read it as
flat. The 20-second rate drifted up over the month and finished ₹214.17, dearer than
any mid-month cut. Per-call figures cover **call campaigns only**: NRI Elder Care
drives website traffic and the NRI + Bengaluru campaign optimised for WhatsApp
conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions. Still unexplained; delivery was normal either side of it.

**WhatsApp finished at ₹5,924.79 for 27 conversations**, ₹219.44 each. September's
depth split: 27 first replies, **13 past one message, 5 past three**. The ad-set
split is Bengaluru ₹2,090.41 / 13 conversations / **₹160.80 each** against Gulf
₹3,834.38 / 14 / **₹273.88** — Bengaluru is still much the cheaper of the two, and
the deep conversations are no longer all Gulf's (Gulf 3 past three, Bengaluru 2).
Note that on a September-only window Meta returns **no
`messaging_user_depth_5_message_send` key at all**, so the "3 past five" figure in
the previous cut cannot be reproduced on this window — do not carry it forward
without re-deriving it. None of this is on the page: the `DAILY` row format has no
field for messaging depth.

## Out of scope: the account kept running, then went dark

The report is September only, and that is unchanged. For context only, **October
took a further ₹18,476.76** (1–2 Oct, then 6–24 Oct after a three-day gap), and
**the account has spent ₹0.00 every day since 25 October** — more than three weeks
dark — while Pain Management still reads ACTIVE at Meta. That is worth a look; it
is not visible anywhere on this page because October is outside the window.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently show
a stale day. **Now that September is closed, `SNAP_DAY` is the empty string**: no day
in the data matches it, so nothing is excluded from the headline and no row carries the
"so far" tag. The Yesterday card re-titles itself "Last day of the month" and says the
month is final. If the window is ever reopened onto a live day, set `SNAP_DAY` back to
that date and the part-day guard switches itself on again.

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and went
  back to the single `{4}` on 17 Nov when Lipoma was found PAUSED. Keep it in step
  with the statuses or the "live" tag lies. Status is read **now**, not as at the end
  of the window — a campaign that delivered all September can still read PAUSED today.
- **Include ARCHIVED and DELETED in the campaign listing.** `O2 Guardian | NRI Elder
  Care | CTWA | v1` (`120251798076370695`) is ARCHIVED and an unfiltered listing omits
  it. It has never delivered (₹0, no impressions), so it stays out of `CAMPS` — but
  the only way to know that is to ask for it. Same trap as `halcyon-reports`.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
