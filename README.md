# Dmitrii Kosterin

**AI engineer for software delivery — I build the systems that let coding agents ship
production apps, and the gates that keep them honest. Swift/Kotlin engineer underneath.**

Three years of running Claude Code agents on real client work for a mobile app studio
(contract, NDA). The result is not a prompt collection but an operated system: a
multi-agent pipeline that has produced 800+ iOS and Android builds from client
specifications since March 2026 (21 Flutter games in September alone, 10 iOS apps in one
day), with a self-built Telegram bridge to a dispatcher agent, parallel background workers,
mechanical quality gates that no agent can talk past, and a rulebook that grows from the
fixes I make by hand.

---

## Agent systems

### [agent-delivery-pipeline](https://github.com/comixcap/agent-delivery-pipeline) — spec → release-ready build, unattended
Dispatcher agent on Telegram — reached through an **own Bot API bridge** that replaced the
MCP plugin (single poller, 409 as a diagnosis, a watchdog that reads the session screen,
not the PID) — classifies and queues but never executes; build lane
(≤ 6 parallel agent sessions, five stages, git snapshot each) and fast lane (store-review
replies, recolors); **non-LLM gates** — compile, an 11-section static-analysis script, a
fingerprint comparison against 826 previously built apps; **self-improvement loop** — Stop
hook journals manual fixes → nightly agent proposes rules → human adopts. Includes a
17-class **agent failure catalog** mapped to the gate that catches each, a tool policy
(no network, no store, no force-push, no simulator), and a zero-dependency **BM25 RAG +
eval harness** over the rulebook (hit@1 0.92, hit@5 1.0, MRR 0.95 on 26 symptoms, clean
abstention on out-of-scope).

`Claude Code` · `multi-agent orchestration` · `context engineering` · `Telegram Bot API` · `launchd` · `tmux` · `Python`

---

## Engineering foundation — source public, no third-party dependencies

### [AutoScan](https://github.com/comixcap/AutoScan) — macOS car diagnostics over OBD-II
Three hand-written transports behind one protocol (raw BSD sockets, termios serial,
CoreBluetooth with MTU chunking), binary SAE J1979 parsing over ELM327 with multi-frame
assembly and garbage resilience, an `actor` serialising device access. Ships a **Python
ECU emulator** and a headless `--selftest`, so the whole stack is testable without a car.
`Swift` · `POSIX sockets` · `CoreBluetooth` · `Python` · ~6,300 lines

### [Android branch of the pipeline](https://github.com/comixcap/agent-delivery-pipeline/blob/main/docs/android-port.md) — from zero to hands-off in two weeks
First a Kotlin + Compose arcade game (~3,700 lines, shipped to Google Play) proved the
orchestration was platform-agnostic. Then the branch was rebuilt on **Flutter** and taken
to the iOS level of automation: **21 games delivered 7–23 Sep 2026**, 5–7k lines of Dart
each, every one with headless layout tests at three screen sizes and an audio-context test,
20 of 21 with a solver checking level fairness. Each defect the operator caught once became
a rule plus a test the agent runs itself.
`Flutter` · `Dart` · `Kotlin` · `Python` · case study, rulebook, workflows public; games private

### [TOON_TOON](https://github.com/comixcap/TOON_TOON) — pixel-art platformer, iOS
No asset files: sprites are character grids authored in Python and emitted as Swift
source; the previewer ships its own PNG encoder. Hand-written `CADisplayLink` engine,
fixed 1/60 s timestep, axis-separated collision, coyote time, deterministic levels from a seed.
`Swift` · `Canvas` · `Python` · ~12,800 + ~2,150 lines

### [Tinlark](https://github.com/comixcap/Tinlark) — vertical shoot 'em up, iOS
120 Hz fixed-timestep simulation inside SwiftUI without fighting it: one `CADisplayLink`
beat observed by exactly one view, the whole battle in a single `Canvas` pass, enemies and
bosses expressed as two small DSLs. No asset files.
`Swift` · `Canvas` · `AVFoundation` · ~8,500 lines

### [Synthix](https://github.com/comixcap/Synthix) · [Leviora](https://github.com/comixcap/Leviora) · [DeadLane](https://github.com/comixcap/DeadLane)
Recursive-descent chemical formula parser with atom-conservation checking; a
queueing-theory operations simulator with drag-and-drop and live recalculation; a 60 fps
lane-runner with a seeded xorshift64 RNG and fully synthesised audio.
`Swift` · `SwiftUI` · `Swift Charts` · ~24,500 lines combined

---

## How I work

- **Spec, constraints, gates, acceptance are mine; typing is the agent's.** I write the
  specification, fix the architectural constraints the code must live within, decide what
  is checked mechanically and what needs judgment, and I am accountable for the result.
- **If it can be caught without an LLM, it is caught without an LLM.** Compile, grep,
  fingerprint diff, arithmetic on layout metrics. LLM audits are advisory, logged, never gates.
- **I verify by testing, not by trust.** Device sizes from iPhone SE to iPad computed on
  paper; upgrade paths over existing saved data; purpose-built harnesses (an ECU emulator,
  a headless self-test) where checking by hand is expensive.
- **No third-party dependencies, no placeholders, one source of truth per app.** Verifiable
  in every repository above.
- **I say how things were built.** Every README states that Claude is my coding partner.

## Contact

[comixcap@gmail.com](mailto:comixcap@gmail.com) · Telegram @g_r_o_m_o_v · open to AI
engineering roles: agent systems, delivery automation, agent quality — remote.
