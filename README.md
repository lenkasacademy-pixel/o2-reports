# O2 Health Hub — Meta Ads calls report

Client-facing report for **O2 Health Hub** (Meta ad account `924502380456661`).

Live: https://lenkasacademy-pixel.github.io/o2-reports/

A single self-contained `index.html`. Figures are baked into the `CAMPS` and
`DAILY` arrays near the bottom of the file — nothing calls the network, so the
page opens instantly and works offline.

## What it shows

- Amount spent, phone calls placed, and cost per call.
- Daily spend split by campaign (stacked bars) with calls placed overlaid (line).
- A day-by-day matrix of **which campaign each call came from**.
- Per-campaign totals.

## Snapshot

Frozen **11 Sep 2026**. Spend ₹6,731.83 · 68 calls · ₹59.57 per call
(call campaigns only; the NRI Elder Care campaign sends traffic to the website,
not the phone, so it is excluded from cost per call).

## Refreshing

`DAILY` rows are `[campaignIndex, "YYYY-MM-DD", spend, calls, impressions, reach, linkClicks]`.

- Pull with Meta MCP `ads_get_ad_entities`, `level: "campaign"`, `time_increment: "1"`.
- **Calls = `results`** where the indicator is
  `actions:click_to_call_native_call_placed` ("Phone calls placed"). There is no
  queryable `calls` field — `results` carries it, and the indicator differs per
  campaign, so check it before treating a number as calls.
- The account returns a row for every campaign × every day including empty ones;
  keep only rows with spend, calls or impressions. A 500-row response is
  truncated — fetch newer campaigns separately rather than trusting one page.
- `CAMPS` order must not be reshuffled; `DAILY[0]` indexes into it.
- After editing, assert each campaign's `DAILY` totals equal its lifetime
  figures from Meta, and update the snapshot date in `index.html` (title comment,
  masthead stamp, footer) and here.

## Note

`reach` is summed across days, so it double-counts anyone reached on more than
one day. The page labels it "sum of days". Meta's de-duplicated lifetime reach
for this account is 70,718.
