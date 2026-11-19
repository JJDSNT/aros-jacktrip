# Roadmap — learning-oriented independent port

All gates require recorded evidence; none is currently completed.

| Gate | Outcome | Exit evidence |
| --- | --- | --- |
| G0 — source inventory | Pin upstream revision, license and dependency map | Source file references and explicit unsupported assumptions |
| G1 — toolchain | Compile minimal native C++ and synchronization probes | Compiler/linker commands, target ABI and test results |
| G2 — protocol | Header and PCM codec fixture tests | LE/BE vectors, malformed packet tests and desktop comparison |
| G3 — network | Native UDP P2P transport prototype | AROS ↔ desktop packet exchange, loss/cancel tests |
| G4 — AHI | Capture and playback backend | Measured local loopback and sustained duplex |
| G5 — musical audio | Interoperable real-time client | Audible AROS ↔ upstream JackTrip, measured latency/jitter/drift |
| G6 — upstream fidelity | Port source modules and reduce divergence | Documented reused code, test suite and maintenance strategy |
| G7 — expansion | Hub, multichannel, other transports if justified | Separate feasibility reviews |

## Decision checkpoints
- After G1: can the existing C++ code realistically be ported, or is a compatibility shim needed?
- After G2/G3: is native interoperability possible without modifying the upstream wire format?
- After G4/G5: are actual AHI latency and reliability adequate for musical use?
- After G6: can the port remain maintainable as upstream evolves?

## Scope
No TeleMIDI Band integration objective. Target AROS platform should be chosen for debugging convenience first; m68k is a separate explicit portability/performance validation target, not a default constraint for every milestone.
