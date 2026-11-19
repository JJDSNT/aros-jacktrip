# JackTrip for AROS

Independent learning-oriented porting project for [JackTrip](https://github.com/jacktrip/jacktrip) to [AROS](https://github.com/aros-development-team/AROS).

**Status:** research and port feasibility; no AROS build, working audio, or interoperability test has yet been demonstrated.

## Purpose
Study and, where feasible, port the **upstream JackTrip implementation**, retaining its network interoperability and attribution. This is **not** a TeleMIDI Band component or dependency. Prefer discovering platform gaps through concrete experiments rather than rewriting JackTrip from scratch.

## Starting scope
- AROS-native command-line client, no GUI or Virtual Studio initially
- UDP audio and peer interoperability first; hub handshake later
- AHI capture/playback backend and AROSTCP sockets
- Explicit byte-order and ABI tests, especially for big-endian m68k
- Measure latency, jitter, drift, memory and CPU; evaluate other AROS targets before m68k optimization

## Documentation
- [Architecture](docs/ARCHITECTURE.md)
- [Portability audit](docs/PORTABILITY_AUDIT.md)
- [Protocol and interoperability](docs/PROTOCOL.md)
- [Audio backend](docs/AUDIO_BACKEND.md)
- [Roadmap](docs/ROADMAP.md)
- [References](docs/REFERENCES.md)
- [Agent guidance](AGENTS.md)

## Upstream and attribution
Original JackTrip by Juan-Pablo Cáceres, Chris Chafe and contributors, CCRMA / Stanford. Upstream source contains permissive MIT-style notices; **verify root license and per-component licenses before importing code**. Keep original headers, credits and provenance. No upstream source has been copied into this repository.
