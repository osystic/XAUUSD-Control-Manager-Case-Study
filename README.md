# MT4 XAUUSD Trade Control Manager Case Study

> **PUBLIC SHOWCASE · SANITIZED · PORTFOLIO-SAFE**
>
> This repository is a public engineering proof artifact. It contains **no client-delivery source code, no client identity, no account details, no private infrastructure, no credentials, no payment information, and no private conversations**.

![Architecture](assets/architecture.svg)

## What this repository is

An anonymized engineering case study for a completed MetaTrader 4 / MQL4 manual trade-control engagement focused on XAUUSD workflows. The delivery consolidated on-chart position protection controls, multi-chart synchronization, broker-aware stop validation, per-position and basket break-even behavior, and an acceptance-driven Cover workflow.

The final Cover semantics were deliberately separated into **trigger** and **protection**: the configured CVR pip value determines when a profitable trade is eligible for Cover, while the resulting protective stop targets the trade's original entry price rather than a second profit offset.

## Public vs. private repository boundary

| Area | This public showcase | Confidential delivery repository |
|---|---|---|
| Visibility | **Public** | **Private** |
| Purpose | Portfolio, proposals, capability proof | Engineering source of truth |
| MQL4 source code | **Not included** | Included |
| Client identity | **Not included** | Protected/confidential |
| Account/ticket data | **Not included** | Controlled operational context |
| Private conversations | **Not included** | Controlled operational context |
| Safe to share in a relevant proposal | **Yes** | **No** |

This repository is not a fork, mirror, or source-code export. It is an independently sanitized documentation artifact with separate history.

## Challenge

- Provide a compact manual trade-control panel without obscuring the trading chart.
- Keep settings consistent when the same XAUUSD workflow is open on multiple timeframes.
- Distinguish initial-risk settings from actions that modify already-open positions.
- Respect broker StopLevel/FreezeLevel and executable Bid/Ask behavior when moving protective stops.
- Implement both per-position and basket break-even controls without silently loosening stronger protection.
- Resolve Cover semantics through target-environment acceptance rather than assumptions.

## Architecture

```text
MT4 chart controls
      ↓
Shared XAUUSD control state
      ↓
Managed-position registry
      ↓
Trade protection / action layer
  ├─ Initial SL
  ├─ TP
  ├─ CVR trigger → original entry price
  ├─ Repeatable SL stepping
  ├─ Per-position break-even
  ├─ Basket break-even
  ├─ Exact SL-ALL validation
  └─ Close All
      ↓
Broker-side distance / price-side validation
      ↓
MetaTrader 4 order modification / explicit close action
```

## Engineering highlights

- **Multi-chart synchronization:** shared terminal/account/symbol state prevents conflicting values from different XAUUSD timeframes.
- **Cover semantics:** positive trigger measured on the executable close side; protection targets original entry price.
- **Net-profit guard:** Cover requires positive floating net P/L at trigger evaluation.
- **Broker-aware safety:** exact stop placement respects market side and broker stop/freeze constraints.
- **Initial-SL hardening:** fallback protection preserves the configured distance rather than collapsing to a tiny near-market stop.
- **Exact SL-ALL behavior:** unsafe or wrong-side exact stop levels are rejected instead of silently clamped.
- **Break-even choices:** both own-entry and lot-weighted basket break-even controls are supported.
- **Low-distraction UI:** verbose diagnostics are hidden by default while troubleshooting logs remain available.

## Validation evidence

![Validation evidence](assets/validation.svg)

The maintained private baseline was validated through:

1. source-integrity checksum tracking;
2. static delimiter and expected-symbol checks;
3. behavior-specific invariants for Cover, multi-chart synchronization, and broker-safety paths;
4. MetaTrader target-environment acceptance, including confirmation of the final Cover behavior.

> Public CI validates this showcase's disclosure boundary and required artifacts. It does not contain or compile the confidential MQL4 implementation.

## Technology

`MetaTrader 4` · `MQL4` · `XAUUSD` · `OrderModify` safety · `Bid/Ask execution semantics` · `GitHub Actions`

## What is intentionally not claimed

This showcase does **not** claim:

- profitability, win rate, alpha, ROI, or loss prevention;
- exact break-even net P/L after commission, swap, slippage, gaps, or execution effects;
- identical behavior across every broker, symbol suffix, spread model, or MT4 build;
- independent public reproduction of confidential account screenshots;
- publication of client-delivery source code.

## Full case study

[**Read the full public case study**](case-study.md)

Additional public-safe detail:

- [Technical overview](docs/technical-overview.md)
- [Validation evidence](docs/validation-evidence.md)
- [Disclosure boundary](docs/disclosure-boundary.md)

## Disclosure boundary

This repository intentionally omits client identity, personal details, account identifiers, ticket IDs, credentials, private repository URLs, contract/payment information, private conversations, confidential screenshots, broker credentials, and implementation source code.

This is a **sanitized public showcase**, not the engineering source of truth.
