# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
**The month is now complete**, so there is no live part-day in the window and nothing is
excluded from the headlines - see *Snapshot* below.

> **The account did not stop with September.** Over 1-5 Oct it has spent a further
> **Rs 1,527.50 for 37 calls** - Lipoma Rs 614.12 / 23 calls (**Rs 26.70** each) and Pain
> Management Rs 913.38 / 14 calls (Rs 65.24). The other five campaigns are PAUSED at Rs 0.
> This page is September-scoped and will therefore look frozen from here on. Adding an
> October tab is the `halcyon-reports` pattern (one `DAILY_*` array + one `MONTHS` entry +
> one tab button) but o2 has no tab bar yet, so it is a build decision, not a refresh.

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

Frozen **5 Oct 2026, 8:40 am IST**, covering the complete month **4-30 September**.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September is closed, so `SNAP_DAY` is now `null`.** There is no part-day left to hold
out, and with `SNAP_DAY = null` the page excludes nothing, drops the "so far" tag and
relabels the Yesterday card *Final day · 30 Sep* with "September is complete - every
figure on this page is settled". `YDAY` is `2026-09-30`. **Set `SNAP_DAY` back to a real
date the moment the window reaches a live day again**, or an unsettled day will set a
headline number.

**Why that guard earns its keep, measured.** The 29th was published as a part-day at
₹71.22 for 3 calls. Settled, it is **₹1,056.20 for 20 calls** - the part-day had captured
7% of the day's spend and 15% of its calls. Had it been inside the September totals it
would have read as a collapse that never happened.

**The last two days of the month.**

| | spend | calls | each | 20s |
|---|---|---|---|---|
| 29 Sep | ₹1,056.20 | 20 | ₹52.81 | 3 |
| 30 Sep | ₹1,044.52 | 18 | ₹58.03 | 2 |

On the 30th Lipoma took ₹457.23 for 13 calls (₹35.17) and Pain Management ₹587.29 for
5 (₹117.46) - Pain Management's dearest day of the month, on 5 calls, so read it as noise.

**Both headline rates rose as the month closed**: cost per call ₹51.08 → **₹51.46**,
the 20-second call ₹203.83 → **₹214.17**. The 20s rate moved more than the per-call rate
because the last two days booked 38 calls but only 5 that held twenty seconds.

**Only Pain Management and Lipoma are live** (`LIVE = {4, 6}`, unchanged), and they are the
two still spending in October.

**Lipoma is the cheapest line on the account and never lost that place**: ₹3,493.24 for
**102 calls at ₹34.25**, against ₹56.70 for everything else. It was the cheapest call
campaign on every day it ran bar 28 Sep, when Autism beat it by sixteen paise.

**Autism closed on 28 Sep** at ₹2,131.13 for 42 calls (₹50.74), 10 over twenty seconds
(₹213.11) and 4 over a minute. It is PAUSED and spent nothing in October.

**Endoscopy closed on 27 Sep** at ₹3,460.95 for 66 calls (₹52.44) but only 12 held twenty
seconds, **₹288.41 per real conversation** - the dearest of the call campaigns bar the
one-day Kukatpally test (₹502.22 for 5 calls, ₹100.44 each).

**Pain Management** is the biggest line at ₹12,900.47 for 222 calls (₹58.11) and it holds
callers best in absolute terms: 61 of 222 (27%) reached twenty seconds at ₹211.48, and 32
reached a minute at ₹403.14 - the cheapest minute-long call on the account.

**Small revisions this refresh.** Meta settled 28 Sep up by ₹4.53 (Autism +₹0.74, Pain
+₹0.77, Lipoma +₹3.02); no call counts moved on that day.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each - unchanged,
and re-pulled this refresh. Meta also reports how far each went: 27 first replies, 13
conversations past one message, 5 past three, 3 past five. None of that is on the page;
the `DAILY` row format has no field for messaging depth.

> **Trap, newly confirmed.** Meta now returns a `results` **value** for the WhatsApp
> campaign per day (1, 2, 1, 4, 8, 5, 5, 1 across 13-24 Sep = 27), where it previously
> returned none. Those are **conversations, not phone calls** - the indicator is
> `actions:onsite_conversion.messaging_conversation_started_7d`, not
> `actions:click_to_call_native_call_placed`. **Read the indicator, never just the value**,
> or the account picks up 27 phantom calls and cost per call drops from ₹51.46 to ₹48.47.
> The builder keys off `CAMPS[i].type`, so `msg` and `web` rows are forced to 0 calls.
> One of those rows (24 Sep) had a conversation on ₹0 spend and no impressions; it is
> dropped rather than carried as a row of zeros.

**Read the headline carefully - Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | **4-30** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49-₹53; read it as
flat for the month. Keep both rows in front of the client. Per-call figures cover **call
campaigns only**: NRI Elder Care drives website traffic and the NRI + Bengaluru campaign
optimised for WhatsApp conversations, so both sit outside every per-call figure.

**NRI Elder Care still has nothing tracked back**: ₹2,686.81 on 2,700 impressions and 39
link clicks, and its own goal — the `HEnquiry` website event — reports no conversions at
all. The page carries this as a warning card. Worth settling before it runs again.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day and `YDAY` the last complete day, which is what the
Yesterday card reads. Both are plain constants — move them together on every refresh, or
the card will silently show a stale day. **When the window holds no part-day at all (a
closed month), set `SNAP_DAY = null`**: the totals then exclude nothing, the "so far" tag
disappears and the card relabels itself *Final day*. That is the current state.

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
  Even a closed month moves: this refresh found 28 Sep up ₹4.53 on figures published the
  day after it ended.
- **Read `results.indicator`, not just the value.** The msg and web campaigns return a
  `results` value too, and it is not phone calls. See the WhatsApp trap above.
- The daily pull with `cost_per_action_type` spills past the tool's output limit (each row
  carries ~25 `cost_per_action_type:*` keys). Split the month in two
  (1-15, 16-30 — 7 campaigns × 15 days = 105 rows, under the 200-row cap) and parse the
  spilled files with `jq`/python rather than trying to read them inline.
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
