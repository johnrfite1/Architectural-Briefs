# Footprints of Money: A Technical Brief

**Version:** 1.0 | **Platform:** Python CLI | **Status:** Production

## Abstract

Footprints of Money is an automated trading scanner that identifies high-probability entry points by tracking institutional volume patterns across multiple timeframes. The system enforces strict risk gates before generating any buy signals, designed to run unattended via scheduled automation.

---

## Core Architectural Principles

### 1. Multi-Timeframe Confirmation

Signals require alignment across monthly, weekly, and daily timeframes. This cascading filter design dramatically reduces false positives by demanding that macro trends, intermediate momentum, and short-term triggers all agree before action.

### 2. Risk-First Philosophy

A "circuit breaker" system monitors market-wide volatility. When risk conditions exceed defined thresholds, the scanner halts entirely—no signals are generated regardless of individual asset strength. Capital preservation supersedes opportunity.

### 3. Volume Over Price

The core methodology tracks the "footprints" that large players leave in volume data, rather than relying solely on price patterns. Volume precedes price; smart money moves before headlines.

---

## System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     PHASE 0: RISK GATE                          │
│              Market-wide volatility check                       │
│              If unsafe → HALT (no signals)                      │
├─────────────────────────────────────────────────────────────────┤
│                   PHASE 1: MACRO FILTER                         │
│              Monthly timeframe analysis                         │
│              Multiple indicators scored                         │
│              Minimum threshold required                         │
├─────────────────────────────────────────────────────────────────┤
│                 PHASE 2: TACTICAL TRIGGER                       │
│              Weekly trend confirmation                          │
│              Daily entry timing                                 │
│              Momentum flip detection                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Key Subsystems

* **Airbag Module:** Real-time volatility monitoring with automatic halt logic.
* **Macro Scoring Engine:** Proprietary multi-indicator scoring on higher timeframes.
* **Tactical Trigger:** Momentum-based entry timing on lower timeframes.
* **Dual Logging:** All operations recorded to persistent log file for audit trail.
* **Scheduler Integration:** Cron-ready with separate schedules for different asset classes.

---

## Technical Stack

| Layer | Technology |
|-------|------------|
| Language | Python 3.8+ |
| Data Source | yfinance (Yahoo Finance API) |
| Scheduling | Cron (Linux/macOS) |
| Output | Console, Log File, CSV |

---

## Operational Modes

| Mode | Watchlist | Schedule | Rationale |
|------|-----------|----------|-----------|
| **Wall Street** | Equities, ETFs | Mon-Thu 3:30 PM EST | Pre-close scan, no Friday entries |
| **Crypto** | Digital assets | Daily 01:00 UTC | Post-close scan (24/7 markets) |

---

## Data Flow

```
[Cron Trigger] → [Fetch OHLCV Data] → [Risk Check] → [Macro Filter] → [Tactical Trigger] → [Signal Output]
                                           ↓
                                    [If Unsafe: HALT]
```

---

## Design Philosophy

The system embodies a "wait for the setup" mentality. Most days produce zero signals—this is by design. The goal is not to find trades, but to identify the rare moments when multiple independent factors align. Patience is encoded into the architecture.

---

---

*Last Updated: January 2026*
