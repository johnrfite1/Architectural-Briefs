# The Long Telegram: A Technical & Design Brief

**Version:** 2.9 (Polish Phase) | **Platform:** Browser (Pure HTML/CSS/JS) | **Status:** Feature Complete

## Abstract

The Long Telegram is a browser-based Cold War strategy game (1946-1991) that explores asymmetric geopolitics through the lens of historical doctrines. Named after George Kennan's famous 8,000-word diplomatic cable that shaped American foreign policy, the game challenges players to navigate international crises while managing domestic politics—all without triggering nuclear annihilation.

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
| Economic Aid | 1.0 PC | 2.0 SC (people starve at home) |
| Arms Shipment | 3.0 PC | 1.0 SC (cheap military aid) |
| Proxy Intervention | 4.0 PC | 2.0 SC |

The asymmetry emerges from cost structure, not from different codepaths—the same reducer handles both factions.

### 4. The Doctrine System: Strategy as Configuration

Eight advisors unlock unique "Doctrine" gameplay modes. Rather than hardcoding different victory conditions, each doctrine is a **configuration object**:

```javascript
doctrine: {
  victoryMetric: "Long Peace Score",
  victoryCondition: 100,
  costModifiers: { economicAid: 0.5, proxyIntervention: 2.0 },
  specialAbility: "DECLARE_DOCTRINE",
  lossCondition: () => { /* function checking satellite loss */ }
}
```

This pattern allows:
* **Easy balancing:** Tweak numbers without touching logic
* **Thematic CSS:** Each doctrine loads a unique stylesheet
* **Clear victory paths:** Different metrics reward different playstyles

---

## Key Subsystems

### Domestic Economy Layer (v3.0)

The "Guns vs. Butter" dilemma is realized through a parallel economic simulation:

* **Economic Report Card:** GDP, Population, Stability, Labor metrics
* **Strategic Resources:** Oil, Steel, Uranium, Grain with production/consumption balance
* **Budget Priorities:** Military, Industry, Welfare, Research, Infrastructure allocation
* **Resource Deficits:** Shortages create pressure for foreign intervention

The domestic layer constrains foreign policy—you can't fund foreign adventures if your economy collapses.

### Policy Levers (v3.1)

Interactive mechanisms that convert domestic stats into Action Points:

| Faction | Example Lever | Effect |
|---------|--------------|--------|
| USA | Defense Production Act | +3 AP, +2% Inflation, -5 Congressional Support |
| USSR | Industrial Storming | +3 AP, -10 Stability, -2 Grain |

One lever per turn enforces strategic focus.

### Morning Briefing System (v3.2)

Each turn opens with a narrative intelligence briefing:

* **Domestic Front:** Translates raw stats into human stories
* **Global Flashpoint:** Identifies the hottest region
* **Opponent Estimate:** Fog of War hints about enemy priorities
* **Period Leaders:** Presidential/Soviet leader signatures change with era

This transforms spreadsheet mechanics into Cold War atmosphere.

### Red Narrative System

When playing as USSR, events are reframed through Soviet propaganda:

| Western View | Soviet View |
|-------------|-------------|
| "The Iron Curtain Speech" | "Churchill's War Mongering" |
| "The Marshall Plan" | "Dollar Imperialism Threatens Europe" |
| "THE MORNING HEADLINES" | "PRAVDA DISPATCH" |

Same mechanics, different narrative lens.

---

## Visual Design Philosophy

### Board Game Aesthetic (v3.0)

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
| Beria | Lubyanka Basement (black, typewriter, classified dossiers) |
| Litvinov | Diplomat's Salon (velvet red, gold leaf) |

---

## Data Flow

```
// Game Loop
[Turn Start]
    → briefing.js generates Morning Briefing
    → ui.js renders domestic stats + map
    → Player selects Policy Lever (optional)
    → Player takes foreign policy actions
    → events.js triggers historical events
    → Crisis resolution (if triggered)
    → reducer.js calculates new state
    → Victory/Loss check
[Turn End]

// State Shape
{
  turn: 1,
  year: 1946,
  faction: "USA",
  doctrine: "kennan",
  politicalCapital: 5,
  tension: 0,
  regions: { ... },
  domestic: { gdp, inflation, stability, resources },
  doctrineScore: 0
}
```

---

## Design Philosophy

* **History as Teacher:** Real events provide narrative scaffolding without dictating outcomes
* **Asymmetry over Complexity:** Different costs create emergent strategy without complex rules
* **Aesthetic as Mechanic:** Period styling isn't decoration—it's immersion that supports decision-making
* **Serializable for Multiplayer:** "Correspondence Protocol" enables play-by-email async games

---

## Future Architecture (Roadmap)

* **LLM Narrative Engine:** Dynamic briefings and crisis descriptions
* **Audio Atmosphere:** Typewriter clicks, teletype, bunker ambience
* **Bureaucratic Friction:** Realistic delays on orders
* **Async Multiplayer:** Turn-based play via state serialization

---

*Last Updated: January 2026*
