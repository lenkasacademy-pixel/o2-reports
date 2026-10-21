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

Frozen **21 Oct 2026, 8:20 am IST**, covering **4–30 September — the whole month,
now closed and fully settled**. There is no part-day in this cut, so `SNAP_DAY` is
`null` and every day on the page counts towards the headline.
Ad spend ₹31,099.61 + 18% GST ₹5,597.93 = **₹36,697.54 billed**.
437 calls placed · 105 lasted 20s · 47 lasted 60s. ₹51.46 per call placed and
**₹214.17 per call that actually held 20 seconds**.

**The part-day guard just paid for itself.** The previous cut showed 29 Sep as
₹71.22 for 3 calls, taken at 11:10 am. Settled, the 29th was **₹1,056.20 for 20
calls** — fifteen times the spend. Had that part-day been allowed into the
headline it would have read as a collapse in delivery that never happened.

**The month closed on two ordinary days.** 29 Sep ₹1,056.20 / 20 calls / ₹52.81
and 30 Sep ₹1,044.52 / 18 calls / ₹58.03, both split between Pain Management and
Lipoma only.

**Meta revised 28 Sep up by ₹4.53 after publication** — Autism ₹494.70 → ₹495.44,
Pain ₹694.21 → ₹694.98, Lipoma ₹370.06 → ₹373.08 — so the day now reads ₹1,563.50
against the ₹1,558.97 published. No call counts moved.

**Only Pain Management is still ACTIVE.** Lipoma went PAUSED after 30 Sep, joining
Autism, Endoscopy and Kukatpally. `LIVE` is now `new Set([4])`.

### Final September figures per campaign

| Campaign | Spend | Calls | Each | 20s | Per 20s call | Status |
|---|---|---|---|---|---|---|
| Pain Management | ₹12,900.47 | 222 | ₹58.11 | 61 | ₹211.48 | ACTIVE |
| Lipoma Removal | ₹3,493.24 | 102 | **₹34.25** | 21 | ₹166.34 | PAUSED |
| Endoscopy | ₹3,460.95 | 66 | ₹52.44 | 12 | ₹288.41 | PAUSED |
| Autism | ₹2,131.13 | 42 | ₹50.74 | 10 | ₹213.11 | PAUSED |
| Kukatpally (1 day) | ₹502.22 | 5 | ₹100.44 | 1 | ₹502.22 | PAUSED |
| NRI Elder Care (web) | ₹2,686.81 | — | — | — | — | PAUSED |
| NRI + Bengaluru (WhatsApp) | ₹5,924.79 | — | — | — | — | PAUSED |

**Lipoma finished the cheapest line on the account by a wide margin** — ₹34.25 a
call against ₹56.70 for everything else — and it closed on 30 Sep with its best
day of all, 13 calls for ₹457.23 (₹35.17 each).

**Read the headline carefully — the whole improvement is still Lipoma:**

| | 4–22 | 4–23 | 4–24 | 4–26 | 4–27 | 4–28 | **4–30 final** |
|---|---|---|---|---|---|---|---|
| Cost per call placed | ₹50.37 | ₹51.03 | ₹49.39 | ₹52.12 | ₹51.28 | ₹51.08 | **₹51.46** |
| …excluding Lipoma | ₹51.55 | ₹53.24 | ₹52.64 | ₹56.01 | ₹55.52 | ₹55.25 | **₹56.70** |
| Cost per 20-second call | ₹186.55 | ₹184.36 | ₹181.34 | ₹209.78 | ₹204.56 | ₹203.83 | **₹214.17** |
| …excluding Lipoma | ₹187.72 | ₹191.08 | ₹194.87 | ₹226.53 | ₹217.69 | ₹213.69 | **₹226.13** |

Across every refresh recorded here the per-call rate has stayed inside ₹49–₹53;
read it as flat. The 20-second call drifted up over the month and finished ₹214.17.
Keep both rows in front of the client. Per-call figures cover **call campaigns only**:
NRI Elder Care drives website traffic and the NRI + Bengaluru campaign optimised
for WhatsApp conversations, so both sit outside every per-call figure.

**18 September was a near-total stop** — the whole account spent ₹6.43 that day,
122 impressions, both campaigns still ACTIVE. Kept here because nobody has
explained it yet; delivery was normal for the rest of the month.

**WhatsApp stays paused and unchanged** at ₹5,924.79 for **27 conversations**,
₹219.44 each — identical to the previous cut, so the campaign has booked nothing
since. Meta also reports how far each went: 27 first replies, 13 conversations
past one message, 5 past three. (The `depth_5` key is no longer returned for this
period, so the earlier "3 past five" could not be re-verified this refresh.)
Bengaluru buys a conversation for ₹160.80 against Gulf's ₹273.88. None of that is
on the page; the `DAILY` row format has no field for messaging depth.

## ⚠️ October is live and is NOT on this page

The page is September-only by design, but the account did **not** stop:
1–21 Oct has already taken **₹16,256.19 for 253 calls** — Pain Management
₹11,799.84 / 142 calls (still ACTIVE) and Lipoma ₹4,456.35 / 111 calls (PAUSED).
That is over half a September again, invisible to the client on this page.
**Worth deciding whether to add month tabs** the way `halcyon-reports` does, rather
than leaving a report that silently stops at 30 September.

## GST and dates

`GST = 0.18` — Meta bills 18% GST on ad spend in India. The headline "Total billed"
is GST-inclusive; **every per-call cost is ex-GST**, so it reconciles against Ads
Manager, and each one is labelled that way on the page.

`SNAP_DAY` is the last day present in the data **when that day is still a part-day**,
and `YDAY` the last complete day, which is what the Yesterday card reads. Both are
plain constants — move them together on every refresh, or the card will silently show
a stale day.

**When the month is closed there is no part-day, so set `SNAP_DAY = null`.** Every
comparison against it (`r[1]!==SNAP_DAY`, `d===SNAP_DAY`) then simply matches nothing
and the whole month counts, which is what you want. Do **not** point `SNAP_DAY` at the
last settled day to "keep the shape" — that would label a full day "so far" and drop it
out of every headline. Two bits of copy are guarded on `SNAP_DAY` being truthy: the
"still counting" line under the card, and the card's own title, which reads
"Last day of the month" instead of "Yesterday" once the month is closed.

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
- **Do not let the `msg` campaign's `results` become `placed`.** At daily level its
  `results` indicator is `onsite_conversion.messaging_conversation_started_7d`, not
  `click_to_call_native_call_placed`, so a parser that blindly reads `results.values`
  files 27 WhatsApp conversations as 27 phone calls. On the 21 Oct refresh that put
  calls placed at 464 instead of 437 and cost per call at ₹48.47 instead of ₹51.46.
  Gate `placed` on the indicator actually being the call one, and let the
  per-campaign period-total check catch it — that is what caught it here.
