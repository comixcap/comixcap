# Dmitrii Kosterin

**iOS developer — SwiftUI, offline-first apps with no third-party dependencies.**

I build complete iOS applications end to end: architecture, simulation engines, custom vector graphics and App Store submission. Everything below ships without SPM packages, CocoaPods, backends or accounts — and without a single raster image asset. All artwork is drawn in code with `Canvas` and `Path`.

---

## Projects

### [Synthix](https://github.com/comixcap/Synthix) — chemistry lab simulator
A reaction sandbox that actually understands what you type. `ChemEngine` implements a **recursive descent parser for chemical formulas** with nested parentheses and multipliers, verifies atom conservation across the equation, scores reagent sets against known reaction pathways, and simulates the run against temperature, pressure, medium, catalyst and addition order — then names the reason it failed.

`SwiftUI` · `Swift Charts` · ~10,700 lines · 20 files

### [DeadLane](https://github.com/comixcap/DeadLane) — 60 fps lane-runner
A real-time arcade game built entirely in SwiftUI, with no game engine, no sprites and no audio files. A hand-rolled **xorshift64 seeded RNG** makes every level byte-identically reproducible, combat runs on Lanchester's square law, the whole battlefield renders through `Canvas`, and **all eleven sound effects plus the music are synthesized at runtime via `AVAudioEngine`**.

`SwiftUI` · `AVFoundation` · ~3,500 lines · 119 Canvas art blocks

### [Leviora](https://github.com/comixcap/Leviora) — operations management simulator
A queueing-theory sandbox: distribute a case backlog across inspectors under six routing rules, reorder queues by drag-and-drop with live recalculation, run processing cycles and sampled reviews, then read the delay attribution to find out which stage actually caused the lateness.

`SwiftUI` · `Swift Charts` · ~10,300 lines · 5 tabs · 23 modal modules

---

## How I work

- **SwiftUI, iOS 16+**, universal — one proportional layout from iPhone SE to iPad, no per-device branching
- **`ObservableObject` + `@EnvironmentObject`** with a single source of truth per app; `Codable` into `UserDefaults`
- **No dependencies.** No SPM, no CocoaPods, no backend, no analytics, no ads, no tracking
- **No asset shortcuts.** Covers, loaders, backgrounds and game scenes are vector art written in `Canvas` / `Path`, rasterized once through `.drawingGroup()` for scroll performance
- **No placeholders.** Every button runs a real method, every write persists, every screen has a way out

## Contact

[comixcap@gmail.com](mailto:comixcap@gmail.com) · open to iOS work — contract or full-time
