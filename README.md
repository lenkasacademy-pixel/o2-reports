# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).

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

Frozen **13 Oct 2026, 8:10 am IST**, covering **4-30 Sep — September is now closed**
and every day on the page is fully settled, so there is no part-day and nothing is
excluded. `SNAP_DAY` is `null` for that reason and `YDAY` is 30 Sep; the card that
used to read "Yesterday" now reads "Last day of the month".
Ad spend &#8377;31,099.61 + 18% GST &#8377;5,597.93 = **&#8377;36,697.54 billed**.
437 calls placed &middot; 105 lasted 20s &middot; 47 lasted 60s. &#8377;51.46 per call placed and
**&#8377;214.17 per call that actually held 20 seconds**.

**October is running and is NOT on this page.** Scope is September only, by design.
But 1-13 Oct has already taken &#8377;11,011.93 on the two live campaigns (Lipoma
&#8377;4,080.23 / 107 calls, Pain Management &#8377;6,931.70 / 95 calls) &mdash; 202 calls at
&#8377;54.51. If the client wants the current month, this page needs a month tab the
way `halcyon-reports` has one; it has no mechanism for a second month today.

**The last two days of the month closed the headline rates upward.** 29 Sep settled
at &#8377;1,056.20 for 20 calls (&#8377;52.81) and 30 Sep at &#8377;1,044.52 for 18 calls
(&#8377;58.03), but between them they produced only **5** twenty-second calls on
&#8377;2,100 of spend. That is what moved cost per 20-second call from &#8377;203.83
(4-28) to &#8377;214.17 (4-30) while cost per call placed only went &#8377;51.08 to
&#8377;51.46. The expensive number here is duration, not volume.

**Only Pain Management and Lipoma ran past 28 Sep**, and both are still ACTIVE.
Autism, Endoscopy, Kukatpally, NRI Elder Care and WhatsApp were all finished by the
28th. `LIVE` is unchanged at `{4, 6}`.

| campaign | days | spend | calls | per call | 20s+ | per 20s |
|---|---|---|---|---|---|---|
| Pain Management | 21 | &#8377;12,900.47 | 222 | &#8377;58.11 | 61 | &#8377;211.48 |
| WhatsApp *(msg)* | 11 | &#8377;5,924.79 | &mdash; | &mdash; | &mdash; | &mdash; |
| Lipoma | 9 | &#8377;3,493.24 | 102 | **&#8377;34.25** | 21 | **&#8377;166.34** |
| Endoscopy | 5 | &#8377;3,460.95 | 66 | &#8377;52.44 | 12 | &#8377;288.41 |
| NRI Elder Care *(web)* | 4 | &#8377;2,686.81 | &mdash; | &mdash; | &mdash; | &mdash; |
| Autism | 6 | &#8377;2,131.13 | 42 | &#8377;50.74 | 10 | &#8377;213.11 |
| Kukatpally | 1 | &#8377;502.22 | 5 | &#8377;100.44 | 1 | &#8377;502.22 |

**Lipoma finished the month as the cheapest line by a wide margin** &mdash; &#8377;34.25 a
call against &#8377;56.70 for every other call campaign put together, and &#8377;166.34 per
20-second call against &#8377;226.13. It is the only line that improved as it scaled.

**Autism gained a day nobody had seen.** 25 Sep carries &#8377;81.41 and 1,076
impressions with **no calls at all** &mdash; a re-pull day that was zero at the last
refresh. It does not change the month materially (Autism closes at &#8377;2,131.13 / 42
calls / &#8377;50.74) but it is why Autism now shows 6 days rather than 5.

**Revisions since the 29 Sep cut.** 28 Sep settled up by &#8377;4.53 across three
campaigns (Autism +&#8377;0.74, Pain +&#8377;0.77, Lipoma +&#8377;3.02); no call counts
moved on it. Everything from 4-24 Sep is unchanged to the paisa.

**WhatsApp now reports conversations per day.** It closes unchanged at &#8377;5,924.79
for **27 conversations**, &#8377;219.44 each, but `results` now returns the daily split
(1 on the 13th, 2 on the 15th, 1, 4, 8, 5, 5 and 1 on the 24th). **Those counts are
deliberately NOT written into `DAILY`** &mdash; the `placed` column is phone calls only and
the page sums it straight into the "Calls placed" headline, so a conversation count in
that column would be counted as a call. Depth this pull: 27 first replies, 13
conversations past one message, 5 past three. Bengaluru buys a conversation for
&#8377;160.80 against Gulf's &#8377;273.88.

**Read the headline carefully &mdash; Lipoma is still holding the average down:**

| | 4-22 | 4-23 | 4-24 | 4-26 | 4-27 | 4-28 | 4-30 |
|---|---|---|---|---|---|---|---|
| Cost per call placed | &#8377;50.37 | &#8377;51.03 | &#8377;49.39 | &#8377;52.12 | &#8377;51.28 | &#8377;51.08 | **&#8377;51.46** |
| &hellip;excluding Lipoma | &#8377;51.55 | &#8377;53.24 | &#8377;52.64 | &#8377;56.01 | &#8377;55.52 | &#8377;55.25 | **&#8377;56.70** |
| Cost per 20-second call | &#8377;186.55 | &#8377;184.36 | &#8377;181.34 | &#8377;209.78 | &#8377;204.56 | &#8377;203.83 | **&#8377;214.17** |
| &hellip;excluding Lipoma | &#8377;187.72 | &#8377;191.08 | &#8377;194.87 | &#8377;226.53 | &#8377;217.69 | &#8377;213.69 | **&#8377;226.13** |

Across every refresh recorded here the per-call rate has stayed inside &#8377;49-&#8377;53;
read it as flat. Per-call figures cover **call campaigns only**: NRI Elder Care drives
website traffic and the NRI + Bengaluru campaign optimised for WhatsApp conversations,
so both sit outside every per-call figure.

**18 September was a near-total stop** &mdash; the whole account spent &#8377;6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

**Reconciliation.** Campaign sums equal the account's own `level: "ad_account"` daily
spend *and* impressions on all 26 delivering days, to the paisa, and every
20s/60s/tapped division lands on a whole number.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` the last complete day, which is what the card below the headline reads.
Both are plain constants - move them together on every refresh, or the card will
silently show a stale day. **When the month is closed there is no part-day: set
`SNAP_DAY = null`** and nothing is excluded from the totals. The card then titles
itself "Last day of the month" instead of "Yesterday". Do not point `SNAP_DAY` at a
settled day to make it disappear - that drops a real day out of every headline.

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
- Update the snapshot date in `index.html` (title comment, the block comment above
  `CAMPS`, masthead stamp, footer) and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
