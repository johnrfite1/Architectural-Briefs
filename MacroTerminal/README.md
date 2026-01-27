# Macro Terminal: A Technical Brief

**Version:** Active | **Platform:** Browser (Pure HTML/CSS/JS) | **Status:** Live Dashboard

## Abstract

Macro Terminal is a retro CRT-styled dashboard for monitoring macroeconomic deleveraging indicators. It answers one question: **Can the economy outgrow its debt?**

Six gauges track whether the U.S. is achieving a "beautiful deleveraging"—where nominal GDP growth exceeds interest rates, allowing debt burdens to shrink organically without defaults, austerity, or runaway inflation.

---

## Core Architectural Principles

### 1. Zero Dependencies

The dashboard is a single HTML file with embedded CSS and JavaScript, requiring no build step, frameworks, or external services.

### 2. Transparent Inputs

All calculations derive from explicit constants visible in the source. No black boxes—anyone can audit the math and update values from public data releases.

### 3. Signal Clarity

A CRT-inspired visual language provides immediate regime identification through color-coded thresholds. Green/Amber/Red states are visible at a glance.

---

## The Gauges

### 1. Deleveraging Engine (The Spread)

```
Spread = Nominal GDP Growth − 10Y Treasury Yield
```

**Why it matters:** If the economy grows faster than the interest rate on debt, the debt-to-GDP ratio shrinks over time without painful cuts.

| Signal | Interpretation |
|--------|----------------|
| Green (> 0%) | Debt burden shrinking organically |
| Red (< 0%) | Debt compounding faster than growth |

### 2. Productivity Velocity

```
Non-Farm Productivity Growth (%)
```

**Why it matters:** Productivity is the only sustainable source of real growth. Without it, GDP growth is just inflation or debt-fueled consumption.

| Signal | Interpretation |
|--------|----------------|
| Green (> 2.5%) | Real wealth creation, sustainable |
| Red (< 2.5%) | Growth may be artificial |

### 3. Real Interest Rate

```
Market Real Yield = 10Y TIPS Real Yield
```

**Why it matters:** High real rates crush debtors (including governments). Low/negative real rates ease the debt burden.

| Signal | Interpretation |
|--------|----------------|
| Green (< 1.0%) | Accommodative, debt-friendly |
| Amber (1.0-1.5%) | Neutral, watch closely |
| Red (> 1.5%) | Restrictive, debt burden increasing |

### 4. Data Signal Quality

```
Distortion Score (0-10 scale, manual assessment)
```

**Why it matters:** GDP data can be distorted by one-time factors like gold exports, inventory builds, or accounting quirks. This gauge flags when headlines may not reflect underlying reality.

| Score | Interpretation |
|-------|----------------|
| 0-2 | Data is clean and reliable |
| 3-5 | Some distortion (gold/inventory noise) |
| 6-10 | High probability of accounting mirage |

### 5. Primary Balance (% of GDP)

```
Primary Balance = Revenues − Non-Interest Spending
```

**Why it matters:** A healthy primary balance offsets debt dynamics when r − g is unfavorable. Persistent deficits make deleveraging much harder.

| Signal | Interpretation |
|--------|----------------|
| Green | Surplus / near-balance (fiscal tailwind) |
| Amber | Moderate deficit (manageable drag) |
| Red | Large deficit (structural headwind) |

### 6. Interest Burden

```
Net Interest Outlays (% of GDP or % of Revenue)
```

**Why it matters:** High interest costs squeeze fiscal capacity and can force austerity or inflation, even if growth is solid.

| Signal | Interpretation |
|--------|----------------|
| Green | Sustainable burden |
| Amber | Elevated but manageable |
| Red | Crowding out other spending |

---

## Technical Stack

| Layer | Technology |
|-------|------------|
| UI | HTML5, CSS3 (CRT aesthetic) |
| Logic | Vanilla JavaScript |
| Deployment | Local file or static hosting |

---

## Data Flow

```
[Manual Inputs] → [Gauge Calculations] → [Threshold Evaluation] → [CRT UI Render]
```

All inputs are constants in the script section. Update from FRED, BEA, or Treasury releases as needed.

---

## Design Philosophy

The dashboard embodies a specific macroeconomic thesis: debt crises are not inevitable if policymakers can achieve the right balance of growth, inflation, and fiscal restraint. The gauges surface the key variables that determine whether "growing out of debt" is working.

* **CRT Aesthetic:** Period styling evokes the operator consoles where these decisions were historically made
* **Manual Updates:** Deliberate friction prevents over-reliance on potentially stale or misleading real-time feeds
* **Basis Consistency:** Nominal GDP growth and yields must use the same basis (SAAR or YoY) to avoid comparison errors

---

*Last Updated: January 2026*
