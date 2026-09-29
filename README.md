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

Frozen **29 Sep 2026, 10:10 am IST**, covering 4–28 Sep (the 29th is a part-day
and is excluded from every headline).
Ad spend ₹28,990.93 + 18% GST ₹5,218.37 = **₹34,209.30 billed**.
399 calls placed · 100 lasted 20s · 46 lasted 60s. ₹51.08 per call placed and
**₹203.79 per call that actually held 20 seconds**.

**Both headline rates improved again, and this time the mix helped rather than
hid.** Cost per call placed ₹51.28 → **₹51.08**, the 20-second call
₹204.56 → **₹203.79**. That is the second consecutive refresh in the right
direction after the 26th's spike.

**28 September was the cheapest full day of the month**: ₹1,555.54 for **32 calls
at ₹48.61**, 8 of them over twenty seconds.

| 28 Sep | spend | calls | each | 20s |
|---|---|---|---|---|
| Pain Management | ₹692.96 | 11 | ₹62.997 | 4 |
| Autism | ₹493.49 | 12 | ₹41.12 | 3 |
| Lipoma | ₹369.09 | 9 | ₹41.01 | 1 |
| Endoscopy | — | — | — | — |

**Autism came back, ran well, and then stopped.** Yesterday's note expected it
back after its ₹12.37 part-day; it returned on the 28th and was the *second
cheapest* line at ₹41.12 — a long way from the ₹87.50 it cost on the 26th. It
now reads **PAUSED**, as does Endoscopy. `LIVE` is down to Pain Management and
Lipoma; two of the four call campaigns that were running last refresh are off.

**Endoscopy did not run on the 28th.** Its daily rate now reads
₹45.41 → ₹55.51 → ₹57.29 → ₹60.18 → **₹41.58** and then nothing. The
"gets dearer the longer it runs" reading is still dead; with the campaign paused
there is no next point to test it against.

**Lipoma is still the best line, seven days running**, at ₹2,645.50 for **78 calls
at ₹33.92** over the settled days, against ₹55.25 for everything else.

**WhatsApp stays paused** at ₹5,924.79 for **27 conversations**, ₹219.44 each —
unmoved for a fifth refresh. Meta's depth figures are also unchanged: 27 first
replies, 13 conversations past one message, 5 past three, 3 past five, and every
one of the deep ones is the Gulf ad set. Bengaluru buys a conversation for
₹160.80 against Gulf's ₹273.88. None of that is on the page yet; the `DAILY` row
format has no field for messaging depth.

**Read the headline carefully — Lipoma is still holding the average down:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 |
|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | **₹51.08** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | **₹55.25** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | **₹203.79** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | **₹213.66** |

Every row moved the right way, but none is back to the 24th's level and the
20-second call is still the third-dearest reading recorded. Excluding Lipoma the
account sits at ₹55.25 a call. Keep both rows in front of the client. Per-call
figures cover **call campaigns only**: NRI Elder Care drives website traffic and
the NRI + Bengaluru campaign optimised for WhatsApp conversations, so both sit
outside every per-call figure.

**26 September was revised after publication.** Autism's row for that day gained
89 impressions, 60 reach and 3 link clicks (spend unchanged at ₹875.00). The
account-level reconciliation caught it; the row is corrected here. Spend and call
counts for the day are unchanged, so no headline moved.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery has been normal since.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data (a part-day) and `YDAY` the last
complete day, which is what the Yesterday card reads. Both are plain constants —
move them together on every refresh, or the card will silently show a stale day.

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
  in step with the statuses or the "live" tag lies. On the 29 Sep pull it dropped
  from `{0, 3, 4, 6}` to `{4, 6}` — Autism and Endoscopy both went PAUSED.
- Update the snapshot date in `index.html` (title comment, masthead stamp, footer)
  and here.
- The `msg` campaign has **no column for messaging conversations** — `DAILY`'s
  `placed` is phone calls only, and the page renders msg rows as "no calls —
  WhatsApp". Conversation counts live in this README alone, so re-pull them
  (`results`, indicator `onsite_conversion.messaging_conversation_started_7d`)
  whenever you touch the WhatsApp paragraph above.
