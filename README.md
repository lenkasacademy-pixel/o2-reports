# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network.

**Scope: September 2026 only** (4-30 Sep; 4 Sep was the first day with delivery).
The month is **closed and fully settled**, so there is no part-day to hold back.

## What it shows

- Amount spent, calls placed, and how many calls lasted 20s / 60s.
- A duration funnel: placed → 20s+ → 60s+, with the true cost of each.
- Daily spend split by campaign (stacked bars), calls placed (solid line) and
  calls over 20s (dashed line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals including cost per 20-second call.
- A **Last day** card (30 Sep) with that day's billed amount, calls, 20s calls
  and cost per call, broken out by campaign. It reads "Yesterday" while a
  part-day is still accruing; with `SNAP_DAY` null it reads "Last day".

## Snapshot

Frozen **11 Nov 2026, 8:10 am IST**, covering the whole of **4-30 September**.
September is over and every day in it has settled, so nothing is excluded.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**September closed on two quiet days and the account has not spent since.**
29 Sep took ₹1,056.20 for 20 calls and 30 Sep ₹1,044.52 for 18 — only Pain
Management and Lipoma were left running, and both days landed near the month's
average. The account did spend again in October (1-24 Oct, then nothing from 25
Oct through 11 Nov), but that is **outside this report's scope**; this page is
September only.

| 30 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | ₹587.29 | 5 | ₹117.46 | 0 |
| Lipoma | ₹457.23 | 13 | ₹35.17 | 2 |

**The two closing days cost the headline rate a little.** Adding the 29th and
30th moved cost per call from ₹51.10 to **₹51.46** and the 20-second call from
₹203.87 to **₹214.17** — the five extra 20s calls came on ₹2,100 of extra spend,
a thinner rate than the month had been running. Per-call is still inside the
₹49-₹53 band every refresh has reported: read it as flat.

**Pain Management closes as the dearest live line and Lipoma the cheapest.**
Pain Management: ₹12,900.47 over 21 days, 222 calls at **₹58.11**, 61 of them
(27%) past twenty seconds at ₹211.48. Its last two days were its worst two of
the month on price — ₹74.41 (29th) then ₹117.46 (30th) on five calls — which is
what pulled the blended rate up. Lipoma: ₹3,493.24 over 9 days, 102 calls at
**₹34.25**, and it never had a day above ₹42.42. It is the only line that beat
the account average on every single day it ran.

**Final per-campaign standing (call campaigns, ex-GST):**

| Campaign | Days | Spend | Calls | Each | 20s | Each |
|---|---|---|---|---|---|---|
| Pain Management | 21 | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 |
| Lipoma Removal | 9 | ₹3,493.24 | 102 | ₹34.25 | 21 | ₹166.34 |
| Endoscopy | 5 | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 |
| Autism | 6 | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 |
| Kukatpally (one-day test) | 1 | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 |

**Lipoma is still holding the average down on its own.** Excluding it the
account sits at **₹56.70** a call and ₹226.13 per 20-second call. Keep both rows
in front of the client. Per-call figures cover **call campaigns only**: NRI Elder
Care drives website traffic and the NRI + Bengaluru campaign optimised for
WhatsApp conversations, so both sit outside every per-call figure.

**Revisions since the 29 Sep cut.** Meta settled 4-28 Sep up by ₹4.53 in total
(₹28,994.36 → ₹28,998.89); no call count inside that window moved. The 29th,
published as a part-day at ₹71.22 for 3 calls, settled at ₹1,056.20 for 20.
That is exactly what the part-day rule exists for.

**Status now (11 Nov).** Pain Management is the only campaign still ACTIVE at
Meta; Lipoma has been paused since the end of September, and Autism, Endoscopy,
Kukatpally, NRI Elder Care and WhatsApp are all paused. `LIVE` is down to the
single index 4.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unchanged from the last cut. Meta also reports how far each went: 27 first
replies, 13 conversations past one message, 5 past three, and 29 total messaging
connections. Meta no longer returns a `messaging_user_depth_5_message_send` key
for this campaign, so the earlier "3 past five" cannot be reproduced and has
been dropped rather than carried forward. Bengaluru buys a conversation for
₹160.80 against Gulf's ₹273.88 (ad-set split, unchanged — the campaign has not
spent since 28 Sep). None of that is on the page: the `DAILY` row format has no
field for messaging depth.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal afterwards.

**6 September is still the odd one.** Two calls arrived with zero spend behind
them (delayed attribution), so they sit in "placed" and carry no derivable
duration. Recorded as 0/0, treated as unknown rather than a real zero.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a
part-day**, and `YDAY` the last complete day, which is what the Last day card
reads. Both are plain constants — move them together on every refresh, or the
card will silently show a stale day.

Now that September is closed there is no part-day, so **`SNAP_DAY` is `null`**
and `YDAY` is 30 Sep. A null `SNAP_DAY` holds nothing back: the settled-day
filter becomes a no-op, no row gets the *so far* tag, and the card titles itself
"Last day" instead of "Yesterday". Do not point `SNAP_DAY` at 30 Sep to keep the
old shape — that would drop a fully settled day out of every headline and
understate the month.

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
