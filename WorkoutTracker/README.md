# Workout Tracker: A Technical Brief

**Version:** Active | **Platform:** Browser (Pure HTML/CSS/JS) | **Status:** Live Utility

## Abstract

Workout Tracker is a single-page training utility that combines an analog rest timer, set tracking, and exercise notes in a single offline-capable interface. The design emphasizes visibility at a distance, fast interaction, and persistent local state.

---

## Core Architectural Principles

### 1. Zero Dependencies
The entire application is a single HTML file with embedded CSS and JavaScript, requiring no build step or external libraries.

### 2. High-Visibility Interface
A large analog clock and bold UI elements prioritize readability during workouts without fine interaction.

### 3. Local-Only Persistence
Notes, checkmarks, and set state are stored in `localStorage` for instant save/restore without server calls.

---

## Key Subsystems

* **Analog Rest Timer:** Second-hand animation with rest countdown and audio alert.
* **Set Tracker:** Incremental set counter with visual indicator lights.
* **Exercise Notes:** Per-exercise notes and completion checks persisted locally.

---

## Technical Stack

| Layer | Technology |
|-------|------------|
| UI | HTML5, CSS3 |
| Logic | Vanilla JavaScript |
| Storage | localStorage |

---

## Data Flow

```
[User Input] → [Timer + Set State] → [UI Render] → [localStorage Persist]
```

---

*Last Updated: January 2026*
