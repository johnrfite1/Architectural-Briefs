# Golden Seam: A Technical & Philosophical Brief

**Version:** 1.0 | **Platform:** visionOS 2.0+ | **Status:** Sprint 3/4 Complete (95%)

## Abstract

Golden Seam is a minimalist, AI-powered journaling sanctuary for **visionOS**. Its core purpose is to provide a completely private, non-judgmental space for self-reflection, founded on a **Sacred Vow** of 100% on-device processing. Inspired by the Japanese art of *Kintsugi* (mending broken pottery with gold), the app's "Poetic Engine" curates a user's own words into beautiful artifacts that illuminate their personal journey.

The experience centers on a **3D-rendered ceramic bowl**—a spatial metaphor for containment and reflection in Apple's immersive computing paradigm.

---

## Core Architectural Principles

The architecture of Golden Seam is a direct translation of its philosophy. Every technical decision is weighed against the Sacred Vow and the "Sanctuary Prime Directives."

### 1. The Sacred Vow: Privacy by Default, Not by Option

The foundation of the app is its absolute commitment to privacy. This is not a setting; it is the architecture.

* **No Network Code:** The application contains no networking code for user data. No analytics, no telemetry, no cloud sync. A user's thoughts never leave their device.
* **Content-Level Encryption:** All journal entries are stored in an on-device Core Data store with CryptoKit encryption, providing a layer of protection beyond the standard visionOS file protection. Data is unreadable even if the device is compromised.

### 2. Durability by Design: The Unbreakable Vessel

A sanctuary must be reliable. The application is architected to protect a user's thoughts against common failure modes.

* **Atomic, Crash-Proof Saves:** A Swift Actor (`SessionIOActor`) serializes all write operations. Background task handling ensures that even in unexpected termination scenarios, data loss is minimized to the last few seconds of typing.
* **Keychain-Backed State:** Critical application state (transaction ledger, boot counter, user preferences) persists in the Keychain, surviving app reinstalls.

### 3. Verifiable Integrity: An Anti-Gaming Architecture

The app's time-gating and patronage model are protected against manipulation, ensuring the system's integrity.

* **Reboot-Hardened Clock:** The app uses a `TrustedElapsedClock` that tracks a Keychain-persisted boot counter and enters a "distrust state" to neutralize attempts to farm time-gated features by manipulating the system clock and rebooting.
* **Permanent, Serverless IAP Validation:** The `FuelLedger` uses a Keychain-persisted set of transaction digests with StoreKit 2, making it fully idempotent. This prevents fraudulent replay attacks across app reinstalls without requiring a central server.

### 4. Philosophy in Code: The Poetic Engine

The app's unique value comes from an AI that acts as a curator, not an inventor.

* **The Law of Authenticity:** The Poetic Engine is governed by one rule: it can only use words the user has written. Its art is in curation and arrangement, reflecting the user's own thoughts back to them in a new light.
* **Harm Filtering:** A curated `HarmLexicon` ensures generated artifacts exclude potentially harmful content while preserving user expression.

---

## Key Subsystems

### The Exchange: Quality-Gated Gift System

A novel social feature allowing users to share "Poetic Artifacts" with others:

* **Ed25519 Signed Tokens:** Each gift token is cryptographically signed, preventing forgery
* **Quality Gate:** Only artifacts meeting minimum quality thresholds can become gifts
* **Privacy-Preserving:** Gift creation and redemption require no server communication

### Tutorial & Onboarding

* **Kanji Introduction:** One-time immersive introduction to the bowl metaphor and core concepts
* **Scholar's Mark:** Contextual help overlay system (0.9s short-press / 1.6s long-press gestures)
* **Progressive Disclosure:** Features unlock naturally as users engage with the app

### Notification System

* **Monthly Reminders:** Opt-in notifications encourage regular reflection practice
* **Artifact Celebrations:** Gentle notifications when new poetic artifacts are ready
* **Respect for Attention:** No engagement-farming tactics; notifications serve the user's wellbeing

---

## Technical Stack

| Layer | Technology |
|-------|------------|
| Platform | visionOS 2.0+, Swift 5.10 |
| UI | SwiftUI, RealityKit (3D bowl) |
| Storage | Core Data + Keychain |
| Encryption | CryptoKit (AES-GCM) |
| IAP | StoreKit 2 |
| Signing | CryptoKit (Ed25519) |

---

## The Crucible Methodology

This project was forged using a rigorous framework for ideation and stress-testing called **The Crucible**. Every component was subjected to a `BUILD -> BREAK -> REFINE` cycle between an **Engineer** (The Machinist) and an **Adversary** (The Skeptic), with oversight from an **Advocate** to champion user ethics. This process ensures that the final product is not only functional but also philosophically coherent and resilient by design.

---

*Last Updated: January 2026*
