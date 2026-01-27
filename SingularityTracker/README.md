# Singularity Tracker: A Technical Brief

**Version:** V5 | **Platform:** Browser (Pure HTML/CSS/JS) | **Status:** Active Development

## Abstract

Singularity Tracker is a single-file dashboard for monitoring progress toward advanced AI capability milestones. It presents market signals, crowd predictions, friction indicators, and strategic analysis in a retro-terminal interface—designed for deliberate, low-frequency updates with full provenance tracking on every data point.

The tracker operates in three modes: **Manual** (offline JSON workflows), **Live** (Worker-fetched real data), and **Template** (blank state for LLM updates).

---

## Core Architectural Principles

### 1. Zero Dependencies, Single File

The tracker is a single HTML file with embedded CSS and JavaScript. No build step, no frameworks, no external services required for core operation. Opens instantly in any modern browser.

### 2. Provenance-First Data Model

Every metric tracks its source:

```javascript
{
  "value": "3.2T",
  "asOf": "2026-01-15",
  "sourceName": "NVIDIA Q4 Earnings",
  "sourceUrl": "https://...",
  "confidence": "HIGH"
}
```

Metrics without provenance render as `PENDING_VERIFICATION`, ensuring data integrity is visible at a glance.

### 3. LLM-Native Update Workflow

The tracker is designed for AI-assisted data maintenance:

* **Copy LLM Update Pack:** Generates a structured JSON skeleton with instructions
* **Import JSON:** Paste LLM responses directly; the tracker merges known fields
* **Core-Only Pack:** Focused skeleton for high-priority metrics only

This workflow enables keeping dozens of data points current with minimal manual effort.

### 4. Optional Real-Time Integration

Live mode connects to a Cloudflare Worker for real-time data:

* NVIDIA stock price and movement
* Manifold prediction market probabilities
* Automatic provenance fill for legacy payloads

If the Worker is unavailable, the tracker gracefully falls back to stored values with a status banner.

---

## Key Subsystems

### Signal Panels

| Panel | Metrics Tracked |
|-------|-----------------|
| **Kurzweil Scorecard** | Prediction accuracy by year (2009, 2019, 2025, 2029, 2045) |
| **Capital Flow** | AI CapEx, NVIDIA price, VC deployment, compute cost trends |
| **Crowd Predictions** | Manifold AGI 2027/2030 probabilities |
| **Friction Monitor** | Regulatory, compute, AI winter, energy constraints |
| **Geopolitical Stress** | TSMC risk, US-China gap, export controls, EU regulation |
| **Energy Demand** | Datacenter load, AI share, nuclear pipeline, curtailment risk |
| **Sector Heatmap** | AI displacement by sector (Legal, Finance, Creative, etc.) |
| **Artifact Integrity** | Task completion, plan accuracy, recommendation quality |

### Operational Modes

| Mode | Network | Use Case |
|------|---------|----------|
| **MANUAL** | None | Offline operation, JSON import/export, LLM workflows |
| **LIVE** | Worker fetch | Real-time market data, auto-refresh |
| **TEMPLATE** | None | Blank state for generating fresh LLM update packs |

### Probability Sliders

Interactive sliders for subjective probability estimates:

* Singularity by 2026
* Tariff-driven inflation risk
* Deficit reduction targets

Values persist in local storage and export with state snapshots.

### News Ticker & Intelligence Brief

* **Headlines Array:** Rotating ticker of recent AI developments
* **Commander's Intent:** Strategic summary field for analyst commentary
* **Swing Factors:** Key variables that could shift trajectories

---

## Technical Stack

| Layer | Technology |
|-------|------------|
| UI | HTML5, CSS3 (terminal aesthetic) |
| Logic | Vanilla JavaScript (ES6+) |
| Storage | localStorage (state persistence) |
| Real-Time | Fetch API → Cloudflare Worker (optional) |
| Export | File System Access API / download fallback |

---

## Data Flow

```
[Mode Selection]
    ↓
[MANUAL] ←→ [Import/Export JSON] ←→ [LLM Update Pack]
    ↓
[LIVE] → [Worker Fetch] → [Merge with Provenance] → [Render]
    ↓
[State] → [localStorage] → [Snapshot Export (HTML)]
```

---

## Import/Export Workflow

### Export Capabilities

* **Export JSON:** Full state object to clipboard (all metrics, notes, probabilities)
* **Export Snapshot HTML:** Self-contained static HTML preserving current values

### Import Capabilities

* **Full State:** Replace entire tracker state
* **Partial Metrics:** Merge only specified fields (preserves unmentioned data)
* **Legacy Support:** Handles older Worker payload formats with auto-mapping

### LLM Update Pack

The "Copy LLM Update Pack" button generates:

1. Instruction block explaining the expected format
2. JSON skeleton with current values as hints
3. Provenance field requirements (`asOf`, `sourceName`, `sourceUrl`)

Paste this into any LLM, request updates, then paste the response back into "Import JSON."

---

## Field Mapping Reference

Key state paths for data integration:

| UI Element | State Path |
|------------|------------|
| News ticker | `notes.headlines[]` |
| NVIDIA price | `metrics.nvidiaPrice` |
| Manifold AGI 2027 | `metrics.crowdAgi2027` |
| Manifold AGI 2030 | `metrics.crowdAgi2030` |
| AI CapEx | `metrics.capex` |
| Regulatory friction | `metrics.frictionRegulatory` |
| TSMC risk | `metrics.geoTsmc` |
| Singularity probability | `probs.singularity2026` |

---

## Design Philosophy

* **Manual-First:** Real-time data is nice, but deliberate updates with provenance are better than stale auto-refresh
* **Transparent Sources:** Every number should trace back to a verifiable origin
* **LLM-Augmented:** Designed for humans + AI collaboration on data maintenance
* **Portable Artifacts:** Snapshot exports create permanent records independent of the app

---

*Last Updated: January 2026*
