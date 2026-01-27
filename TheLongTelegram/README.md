<div align="center">

<img src="Main.png" alt="Main Image" />

</div>

# The Long Telegram: A Technical & Design Brief

**Version:** v7.0 "Three Rooms" | **Platform:** Browser (Pure HTML/CSS/JS) | **Status:** Active Development

## Abstract

The Long Telegram is a browser-based Cold War strategy game (1946-1953) that explores asymmetric geopolitics through the lens of historical doctrines. Named after George Kennan's famous 8,000-word diplomatic cable that shaped American foreign policy, the game challenges players to navigate international crises while managing domestic politics—all without triggering nuclear annihilation.

The architecture prioritizes **zero dependencies**, **full state serializability**, and **narrative immersion** through period-accurate aesthetics.

---

## Core Architectural Principles

### 1. Zero Dependencies: Pure Web Stack

The entire game runs without frameworks, build steps, or external dependencies:

| Layer | Technology |
|-------|------------|
| Structure | Semantic HTML5 |
| Styling | CSS3 with CSS Variables |
| Logic | Vanilla ES6 JavaScript |
| Audio | Web Audio API |

This ensures the game works on any modern browser without installation, bundling, or transpilation. A deliberate constraint that forces simplicity.

### 2. Pure Functional State Management

Game state flows through a **reducer pattern** inspired by Redux but without the library:

```
[User Action] → actions.js → reducer.js (pure function) → New State → ui.js (render)
```

* **Immutable State:** The reducer never mutates; it returns a new state object
* **Deterministic Transitions:** Given the same state and action, the result is always identical
* **Serializable:** The entire game state can be JSON.stringify'd for save/load

This enables future features like replay systems, undo functionality, and asynchronous multiplayer via "Correspondence Protocol."

### 3. Asymmetric Faction Design

Both superpowers share the same action types but with radically different costs and motivations:

| Action | USA (Political Capital) | USSR (State Control) |
|--------|------------------------|---------------------|
| Diplomatic Note | 0.5 PC | 0.5 SC |
| Economic Aid | 1.5 PC | 1.5 SC (people starve at home) |
| Arms Shipment | 1.5 PC | 1.0 SC (cheap military aid) |
| Proxy Intervention | 3.0 PC | 2.0 SC |
| Border Probe | — | 0.5 SC (USSR exclusive) |

The asymmetry emerges from cost structure, not from different codepaths—the same reducer handles both factions.

### 4. The Doctrine System: Strategy as Configuration

Eight advisors unlock unique "Doctrine" gameplay modes. Rather than hardcoding different victory conditions, each doctrine is a **configuration object** with unique victory metrics, cost modifiers, and themed visual styling.

---

## Key Subsystems

### Three Rooms Architecture (v7.0)

The interface is split into three dedicated views with strict rendering boundaries:

| Room | Purpose | Primary Elements |
|------|---------|------------------|
| **War Room** | Foreign policy operations | World map, action panel, crisis responses |
| **Domestic Desk** | Economic management | Budget priorities, resources, policy levers |
| **Intelligence Hub** | Information synthesis | Gazette feed, Eyes Only reports |

### Risk & Uncertainty Stack (v5.5+)

No action is purely safe or deterministic:

* **Influence Fatigue + Backlash:** Repeated pressure builds fatigue, degrading effectiveness and triggering local resistance.
* **Uncertain Diplomacy:** Soft-power actions can fully land, partially land, stall, or backfire with delayed effects.
* **Crisis Fog of War:** Crisis responses include success uncertainty with LOW/MED/HIGH confidence hints.
* **Country Traits:** Personality tags (Pacifist, Military Junta, Labor Unrest) modulate action impact.
* **Exposure Pressure:** Aggressive actions add short-term exposure risk; leaks cost prestige.

### Domestic Economy Layer (v3.0+)

The "Guns vs. Butter" dilemma is realized through a parallel economic simulation:

* **Economic Report Card:** GDP, Inflation, Stability, Labor metrics
* **Strategic Resources:** Oil, Steel, Uranium, Grain with production/consumption balance
* **Budget Priorities:** Military, Industry, Welfare, Research, Infrastructure allocation
* **Resource Deficits:** Shortages create action cost multipliers

### Occupation Zone System (v5.7)

Historical accuracy meets gameplay:

* **1946 Start:** Germany and Korea begin as occupation zones, not independent states
* **Country Transformation Events:** Zones become independent states at historical dates (1948-1949)
* **Occupation Traits:** "Occupied", "Devastated", "Divided" affect stability and alignment

### Client State Autonomy (v5.3)

Your allies are not puppets—they have their own agendas:

* **Militancy System:** Each country tracks militancy (0-100) visible on map nodes
* **Patron's Dilemma:** High militancy triggers autonomous ally provocations
* **Forced Responses:** Back your ally, disavow them, or attempt covert restraint

### Intelligence Systems

* **Epistemic Fog (v4.2+):** Briefings show confidence-based estimates of opponent posture
* **Intent Spiral (v5.4):** Defensive moves can appear aggressive when intel confidence is low
* **Dual-Channel Logs (v5.1):** Public "Global Gazette" and secret "Eyes Only" feeds
* **Operation Morning Paper (v6.1):** Turn-start auto-generates situational reports for both channels

### Command & Control (v5.8)

Surface critical data without sub-menu diving:

* **Situation Board:** Ticker alerts for resource deficits, rogue agencies, flashpoints
* **Intelligence Layers:** Three toggleable map modes (Political, Instability, Intel)
* **Clear Light Mode:** Accessibility option restoring bright, neutral lighting

### Visual Decay System (v5.0)

The desk physically degrades as the Cold War intensifies:

| Tier | Trigger | Visual Effect |
|------|---------|---------------|
| 0 | Turn 1-7, Tension < 30 | Bright lighting, organized desk |
| 1 | Turn 8-15, Tension 30-50 | Subtle vignette, scattered papers |
| 2 | Turn 16-24, Tension 50-75 | Coffee rings, overflowing ashtrays |
| 3 | Turn 25+, Tension 75+ | Red emergency tint, extreme clutter |

---

## Visual Design Philosophy

### Board Game Aesthetic

The strategic map evokes 1947 cartography:

* Parchment background with vintage map styling
* Positioned game pieces at real geographic locations
* Blue/Red/Purple tokens for faction alignment
* Subtle adjacency lines showing diplomatic relationships

### Doctrine Theming

Each doctrine loads a unique CSS file creating distinct atmospheres:

| Doctrine | Aesthetic |
|----------|-----------|
| Kennan | Policy Planning Staff (wood paneling, brass) |
| LeMay | SAC Bunker (concrete, warning lights) |
| Wallace | Progressive Campaign (clean white, Futura) |
| Acheson | NATO Summit (institutional blue, formal) |
| Konev | Soviet Command Post (military green) |
| Molotov | Foreign Ministry (diplomatic gray) |
| Beria | Lubyanka Basement (black, typewriter, classified) |
| Litvinov | Diplomat's Salon (velvet red, gold leaf) |

---

## Technical Implementation

### Headless Simulation

The game includes a Node.js simulation harness for testing and balance analysis:

```bash
node sim.js --count 1000 --cautious    # Run 1000 games with tension-aware AI
node sim.js --doctrines                 # Test all 8 advisor doctrines
node sim.js --validate                  # Enable state invariant checking
```

### Project Structure

```
the-long-telegram/
├── index.html          # Main game page
├── sim.js              # Headless simulation harness
├── css/                # Base themes + 8 doctrine stylesheets
├── js/
│   ├── state.js        # Game state (isomorphic: browser + Node.js)
│   ├── reducer.js      # State transitions (pure functions)
│   ├── events.js       # Historical event system
│   ├── advisors.js     # Doctrine configurations
│   ├── briefing.js     # Morning briefing generator
│   └── ui.js           # DOM rendering (Three Rooms architecture)
└── assets/             # Maps, portraits, audio
```

---

## Design Philosophy

* **History as Teacher:** Real events provide narrative scaffolding without dictating outcomes
* **Asymmetry over Complexity:** Different costs create emergent strategy without complex rules
* **Aesthetic as Mechanic:** Period styling isn't decoration—it's immersion that supports decision-making
* **Serializable for Multiplayer:** "Correspondence Protocol" enables play-by-email async games

---

## Version History Highlights

| Version | Codename | Key Features |
|---------|----------|--------------|
| v7.0 | Three Rooms | War Room/Domestic Desk/Intelligence Hub split |
| v6.0 | Map Maximized | Log modals, header toggles, taller map |
| v5.8 | Command & Control | Situation Board, Intelligence Layers, Clear Light Mode |
| v5.7 | The Long Balance | Occupation zones, resource economy loop |
| v5.5 | The Knife's Edge | Influence fatigue, uncertain diplomacy, country traits |
| v5.0 | Visual Decay | Stress tiers, Intel glitch effects |
| v4.0 | Client State Autonomy | Militancy system, Patron's Dilemma |

---

*Last Updated: January 2026*
