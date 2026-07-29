# Dmitrii Kosterin

**Swift developer — iOS and macOS, no third-party dependencies anywhere.**

I build complete applications: transport layers, protocol parsers, simulation engines and custom vector graphics. Nothing below pulls in an SPM package or a CocoaPod.

---

## Projects

### [AutoScan](https://github.com/comixcap/AutoScan) — macOS car diagnostics over OBD-II
Talks to a real engine control unit through an ELM327 adapter and works out whether someone cleared the fault codes before selling the car — by cross-referencing distance, time and warm-up cycles since the last erase against incomplete readiness monitors. **Three transports written from scratch** behind one protocol: TCP on raw BSD sockets (`getaddrinfo`, `setsockopt`, dedicated reader thread), serial via hand-configured termios, and CoreBluetooth bridged to `async` with MTU-aware chunking. Defensive parsing of multi-frame CAN responses, capability discovery by bitmask, negative-response handling. Ships with a **Python ECU emulator** and a headless `--selftest` mode, so the whole system can be demonstrated without a car.

`SwiftUI` · `CoreBluetooth` · `POSIX sockets` · `actor` · ~6,300 lines · RU/EN

### [TOON_TOON](https://github.com/comixcap/TOON_TOON) — pixel-art platformer, iOS
A game with **no asset files of any kind**. Every sprite is a character grid authored in Python, reviewed as a rendered image on both a pale and a near-black background, then emitted into Swift source — the previewer ships **its own PNG encoder** (zlib plus hand-built chunks, no dependencies). The engine is hand-written: `CADisplayLink` driving a fixed 1/60 s timestep with spiral protection, axis-separated tile collision, coyote time and jump buffering, four boss state machines. Levels generate deterministically from a per-district seed. All music and effects are synthesized at runtime through `AVAudioEngine`.

`SwiftUI` · `Canvas` · `CADisplayLink` · `AVFoundation` · `Python` · ~7,750 lines Swift + ~1,300 Python

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

- **SwiftUI**, iOS 16+ and macOS 14+, universal — one proportional layout from iPhone SE to iPad, no per-device branching
- **`ObservableObject` + `@EnvironmentObject`** with a single source of truth per app; `Codable` into `UserDefaults`
- **Concurrency where it fits** — `actor` to serialize access to a device that physically can't be asked two things at once, `@MainActor` for UI stores, raw `Thread` for blocking read loops, continuations to bridge delegate APIs into `async`
- **No dependencies.** No SPM, no CocoaPods, no analytics, no ads, no tracking
- **No asset shortcuts.** Covers, loaders, backgrounds and game scenes are vector art written in `Canvas` / `Path`, rasterized once through `.drawingGroup()` for scroll performance
- **No placeholders.** Every button runs a real method, every write persists, every screen has a way out

## How these were built

I build these with Claude, Anthropic's AI assistant, as a coding partner — and I'd rather say so up front than have it be a question.

What that means in practice: I write the specification, set the architecture constraints the code has to live inside — no third-party dependencies, no raster assets, `UserDefaults` through a single store, a proportional layout that survives from iPhone SE to iPad — and I run the review cycle. I read what comes back, test it in the simulator across device sizes, and send it back when it's wrong. The assistant writes code against that spec; the decisions about what gets built, how it's structured and whether it's actually finished are mine.

The engines are the part I'd point at: a transport layer on raw sockets, an OBD-II protocol parser that survives malformed hardware responses, a recursive formula parser, a seeded RNG, procedural audio synthesis. They work, they're testable, and I can walk through why each one is written the way it is.

## Contact

[comixcap@gmail.com](mailto:comixcap@gmail.com) · open to iOS work — contract or full-time
