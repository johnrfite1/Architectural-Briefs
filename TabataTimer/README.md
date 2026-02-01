# Tabata Timer: A SwiftUI Sprint Companion

**Version:** 1.0 | **Platform:** iOS 17+ | **Status:** MVP Complete

## Abstract

Tabata Timer is a privacy-conscious iOS workout companion built for runners who favor high-intensity interval training. The app keeps the phone unlocked or pocketed while it **tracks sprints**, **announces transitions via voice**, and **lets Spotify/Apple Music continue playing** by mixing prompts with background audio. The focus is on delivering clear cues, zero clutter, and enough customization to match a runner’s ritual without exposing implementation details.

---

## Experience Pillars

1. **Frantic-Proof Controls** – Oversized typography, monospaced countdowns, and color-coded states make it readable at full stride. Run/pause/reset/end buttons are intentionally sparse to avoid mid-sprint confusion.
2. **Audio-First Guidance** – AVSpeech announcements plus a three-second ticking countdown before each sprint keep a runner informed without checking the screen.
3. **Background Harmony** – An `AVAudioSession` configured with `.mixWithOthers` ensures voice cues sit underneath external music rather than pausing it.
4. **Zero Friction Setup** – Steppers adjust sprint/rest durations (5–120s) and round counts (1–20) with guardrails so the timer logic always has sane inputs.

---

## High-Level Architecture

| Layer | Responsibility |
|-------|----------------|
| `TabataTimerModel` | ObservableObject state machine governing sprint/rest/finish phases, countdown math, pause/resume, and spoken cues. |
| `ContentView` | Single-screen SwiftUI interface (NavigationStack + ScrollView) hosting status card, controls, and setup panel with `@AppStorage` theme toggle. |
| `AudioSessionManager` | Boots the app with a playback session that mixes our prompts with any external audio source. |

### Phase Engine Highlights

* **Deterministic Timer** – Uses a scheduled `Timer` with a stored `targetDate` so pausing/resuming keeps sub-second accuracy.
* **Speech Synthesizer** – Lightweight `AVSpeechUtterance` prompts for “Sprint,” “Recover,” and completion.
* **Recovery Tick Cues** – Uses `AudioServicesPlaySystemSound` for the final three seconds of rest to create urgency without new assets.

### UI Considerations

* **Progress Feedback** – ProgressView bound to elapsed time per phase + text like “Sprint 5 of 8” to track session progress at a glance.
* **Theme Preference** – `@AppStorage` behind a simple toggle flips between light/dark mode, giving runners control over contrast in bright or low-light conditions.

---

## Privacy & Offline Posture

* No network stack or analytics—timers, preferences, and audio cues operate entirely on-device.
* Default Core Data template remains unused; future history features can hook into it without changing the privacy stance.

---

## Near-Term Roadmap (Public-Safe)

1. **Workout History Layer** – Store completed sessions with stats for trend summaries.
2. **Tips Jar Entry Point** – Surface an optional “Support the Builder” button (likely via StoreKit tips or deep link) without altering the workout flow.
3. **Live Activity / Lock Screen Widget** – Keep countdown and phase state visible when the phone is locked.
4. **Haptics + Voice Packs** – Offer haptic taps and optional alternate voices to match personal preference.

---

*Last Updated: January 2026*
