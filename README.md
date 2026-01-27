# Architectural Briefs

A curated collection of technical briefs for experimental software projects—spanning spatial computing, strategy games, AI agents, and macroeconomic tools. Each project is designed with intentional constraints: zero-dependency web apps, privacy-first architectures, or novel UI paradigms.

---

## Featured Projects

### 🎮 [The Long Telegram](./TheLongTelegram/README.md)
**Cold War Strategy Game** | v7.0 "Three Rooms" | Pure HTML/CSS/JS

A browser-based strategy game (1946-1953) where every decision carries consequence. Eight unique doctrines, fog of war intelligence systems, dynamic domestic economies, and client state autonomy create emergent Cold War narratives. Zero dependencies—runs anywhere.

*Features: Asymmetric factions • Doctrine-based victory conditions • Visual decay system • Occupation zones • Morning briefings*

---

### 📿 [Golden Seam](./GoldenSeam/README.md)
**AI Journaling Sanctuary** | visionOS 2.0+ | Swift/RealityKit

A spatial journaling app founded on a "Sacred Vow" of absolute privacy—100% on-device processing, zero network code for user data. Inspired by Kintsugi, the app curates your own words into poetic artifacts through a 3D ceramic bowl interface.

*Features: Content-level encryption • Reboot-hardened clock • Serverless IAP validation • Ed25519 gift signing*

---

### 📊 [Singularity Tracker](./SingularityTracker/README.md)
**AI Milestone Dashboard** | v5 | Pure HTML/CSS/JS

A single-file tracker monitoring progress toward advanced AI capabilities. Features three operational modes (Manual/Live/Template), LLM-powered update packs, and provenance tracking for every data point. Optional Worker integration for real-time market and prediction data.

*Features: Kurzweil scorecard • Crowd predictions • Friction monitor • Energy demand tracking • JSON import/export*

---

## Strategy & Simulation

* **[Macro Terminal](./MacroTerminal/README.md)** — Retro CRT dashboard tracking macroeconomic deleveraging. Six gauges monitor whether the economy can outgrow its debt burden. Transparent calculations, manual inputs, instant clarity.

---

## AI Infrastructure

* **[Trinity Core](./TrinityCore/README.md)** — Autonomous AI agent framework with dual runtime modes. Mission-focused (Trinity) or persona-injected (Foundry) agents, unified by a shared SDK adapter with built-in budget constraints.

* **[The Relay](./TheRelay/README.md)** — Lightweight messaging service for inter-agent communication. CQRS pattern, append-only logs, and watchdog supervision ensure reliable, auditable message delivery.

---

## Framework & Methodology

* **[The Crucible](./TheCrucible/README.md)** — A methodology for conducting cognitive ensembles of AI models. Six personas (Architect, Oracle, Historian, Engineer, Advocate, Adversary) stress-test ideas through structured debate.

* **[The Triumvirate System](./AIGovernanceTriumvirate/README.md)** — Multi-layered AI governance architecture with Proof-of-Alignment consensus, automated risk triage, and integration doctrine.

---

## Labs & Utilities

* **[AI Music Lab](./AIMusicLab/README.md)** — Curated repository for AI-generated music with Git LFS governance.

* **[Footprints of Money](./FootprintsOfMoney/README.md)** — Multi-timeframe trading scanner tracking institutional volume patterns.

* **[Progress Tracker](./ProgressTracker/README.md)** — Static 8-week reset tracker with timeline phases and progress stats.

* **[Workout Tracker](./WorkoutTracker/README.md)** — Single-page workout utility with analog rest timer and set tracking.

---

## Design Philosophy

These projects share common constraints:

| Principle | Implementation |
|-----------|----------------|
| **Zero Dependencies** | Browser apps use vanilla JS—no frameworks, no build steps |
| **Privacy by Architecture** | User data stays local; networking is opt-in or absent |
| **Serializable State** | All game/app state can be JSON.stringify'd for save/load |
| **Aesthetic as Interface** | Period styling, CRT effects, and spatial UI aren't decoration—they're information design |

---

*Last Updated: January 2026*
