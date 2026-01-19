# Macro Terminal: A Technical Brief

**Version:** Active | **Platform:** Browser (Pure HTML/CSS/JS) | **Status:** Live Dashboard

## Abstract

Macro Terminal is a retro CRT-styled dashboard for monitoring macroeconomic deleveraging indicators. It tracks whether the U.S. economy is shrinking its debt burden through growth by visualizing four key gauges derived from manually updated economic inputs.

---

## Core Architectural Principles

### 1. Zero Dependencies
The dashboard is a single HTML file with embedded CSS and JavaScript, requiring no build step, frameworks, or external services.

### 2. Transparent Inputs
All calculations are driven by a small set of explicit constants (GDP growth, yield, inflation, productivity, data quality), making the underlying logic easy to audit and update.

### 3. Readability First
A CRT-inspired visual language provides immediate signal clarity while preserving an operator-console aesthetic.

---

## Key Subsystems

* **Gauge Engine:** Calculates spread, productivity velocity, real rate, and signal quality.
* **Signal Thresholds:** Color-coded thresholds communicate green/amber/red regimes.
* **Data Input Layer:** Manual constants in the script section allow quick updates without tooling.

---

## Technical Stack

| Layer | Technology |
|-------|------------|
| UI | HTML5, CSS3 |
| Logic | Vanilla JavaScript |
| Deployment | Local file or static hosting |

---

## Data Flow

```
[Manual Inputs] → [Gauge Calculations] → [CRT UI Render]
```

---

*Last Updated: January 2026*
