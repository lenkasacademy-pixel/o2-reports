# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** — 4 Sep (the first day with delivery) to 30 Sep.
The month is complete and fully settled. The account also spent in October;
that is deliberately **not** on this page — see *October ran* below.

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

Frozen **22 Nov 2026, 8:15 am IST**, covering **4-30 September - the complete month**.
September closed almost eight weeks ago and every day in it has settled, so nothing is
held back: `SNAP_DAY` is `null` and all 26 delivering days sit in the headline.
Ad spend Rs 31,099.61 + 18% GST Rs 5,597.93 = **Rs 36,697.54 billed**.
437 calls placed - 105 lasted 20s - 47 lasted 60s. Rs 51.46 per call placed and
**Rs 214.17 per call that actually held 20 seconds**.

**The 29th is the clearest case yet for the part-day rule.** The previous refresh caught
29 Sep as a part-day at Rs 71.22 for 3 calls and kept it out of every headline. It
settled at **Rs 1,056.20 for 20 calls** - fourteen times the spend. Had that part-day
been allowed into the totals it would have read as delivery falling off a cliff on the
29th, which never happened. 30 Sep then closed the month at Rs 1,044.52 for 18 calls.
Meta also revised 28 Sep up by Rs 4.53 (Autism +Rs 0.74, Pain +Rs 0.77, Lipoma +Rs 3.02);
no call counts moved on it.

Both headline rates rose once the last two days landed: cost per call Rs 51.08 ->
**Rs 51.46**, the 20-second call Rs 203.83 -> **Rs 214.17**. The 20-second rate moved
most because the 29th and 30th together booked 38 calls but only 3 that held twenty
seconds.

### The month as it finally stands

| Campaign | spend | calls | each | 20s | per 20s | 60s |
|---|---|---|---|---|---|---|
| Pain Management | Rs 12,900.47 | 222 | Rs 58.11 | 61 | Rs 211.48 | 32 |
| Endoscopy | Rs 3,460.95 | 66 | Rs 52.44 | 12 | Rs 288.41 | 4 |
| Lipoma | Rs 3,493.24 | 102 | **Rs 34.25** | 21 | Rs 166.34 | 6 |
| Autism | Rs 2,131.13 | 42 | Rs 50.74 | 10 | Rs 213.11 | 4 |
| Kukatpally (one day) | Rs 502.22 | 5 | Rs 100.44 | 1 | Rs 502.22 | 1 |
| **Call campaigns** | **Rs 22,488.01** | **437** | **Rs 51.46** | **105** | **Rs 214.17** | **47** |
| NRI Elder Care (web) | Rs 2,686.81 | - | - | - | - | - |
| NRI + Bengaluru (WhatsApp) | Rs 5,924.79 | 27 convs | Rs 219.44 | - | - | - |

**Lipoma finished the cheapest line on the account** at Rs 34.25 a call, and it is still
holding the average down on its own - excluding it the account reads Rs 56.70 a call and
Rs 226.13 per 20-second call. Keep both rows in front of the client.

**Pain Management was the only campaign still ACTIVE at Meta** when this was taken, so
`LIVE` is now `new Set([4])`. Lipoma, Autism, Endoscopy, Kukatpally, NRI Elder Care and
the WhatsApp campaign all read PAUSED (and the NRI CTWA campaign ARCHIVED).

**18 September was a near-total stop** - the whole account spent Rs 6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has explained
it yet; delivery was normal on either side of it.

**WhatsApp closed** at Rs 5,924.79 for **27 conversations**, Rs 219.44 each: 27 first
replies, 13 conversations past one message, 5 past three, 3 past five, and every one of
the deep ones is the Gulf ad set. Bengaluru bought a conversation for Rs 160.80 against
Gulf's Rs 273.88. None of that is on the page - the `DAILY` row format has no field for
messaging depth, so those counts live in this README alone.

## October ran, and it is outside this report

**The account did not stop at the end of September.** It spent **Rs 18,476.76 in
October** across two campaigns, then **nothing at all in November** (Rs 0.00, 1-22 Nov).
This page is a September report by design and does not show any of it, which means a
client reading it today is looking at a closed month while the newer, dearer month is
invisible:

| Oct 2026 | spend | calls | each | 20s | per 20s | 60s |
|---|---|---|---|---|---|---|
| Pain Management | Rs 14,020.41 | 162 | **Rs 86.55** | 44 | Rs 318.65 | 24 |
| Lipoma | Rs 4,456.35 | 111 | Rs 40.15 | 39 | Rs 114.27 | 17 |
| **Total** | **Rs 18,476.76** | **273** | **Rs 67.68** | **83** | **Rs 222.61** | **41** |

Two things a human should look at before this is shown to the client:

1. **Pain Management's calls got 49% dearer** - Rs 58.11 in September to Rs 86.55 in
   October - on slightly more spend and roughly the same impressions. That is the single
   biggest movement on the account and the September page cannot show it.
2. **Lipoma went the other way**: Rs 34.25 to Rs 40.15 a call, but its 20-second call
   fell from Rs 166.34 to Rs 114.27, the cheapest real conversation the account has
   bought in either month.

Extending the page to October is a **scope decision, not a refresh**: `index.html` has no
month-tab machinery (unlike `halcyon-reports`), so October means either widening the
declared scope and every "September" label with it, or porting Halcyon's tab bar across.
Neither was done here without a human asking for it.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the live part-day and is kept out of every total; `YDAY` is the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.
**September is now closed, so `SNAP_DAY` is `null`** and nothing is held back; the
card titles itself *Last day* instead of *Yesterday* and says the month has settled.
Set `SNAP_DAY` back to a real date the moment this page is pointed at a month still
in progress, or an unsettled day will set the headline.

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
  It became a set on 23 Sep when Lipoma started and WhatsApp was paused, and is now
  back to one member, `{4}` (Pain Management) - everything else is PAUSED or
  ARCHIVED. Keep it in step with the statuses or the "live" tag lies.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer,
  and the comment above the baked figures - four places) and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
