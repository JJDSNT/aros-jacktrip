# Research references

## Primary upstream
- [JackTrip source](https://github.com/jacktrip/jacktrip)
- [Upstream network protocol](https://github.com/jacktrip/jacktrip/blob/main/docs/Documentation/NetworkProtocol.md)
- [Upstream connection types](https://github.com/jacktrip/jacktrip/blob/main/docs/Documentation/ClientConnectionTypes.md)
- [Upstream Meson build](https://github.com/jacktrip/jacktrip/blob/main/meson.build)
- [Upstream CMake build](https://github.com/jacktrip/jacktrip/blob/main/CMakeLists.txt)
- [Upstream build documentation](https://github.com/jacktrip/jacktrip/tree/main/docs/Build)
- [JackTrip documentation](https://jacktrip.github.io/jacktrip/)
- [JackTrip Labs product](https://www.jacktrip.com/) — commercial product; do not conflate with upstream source capabilities

## AROS platform
- [AROS source](https://github.com/aros-development-team/AROS)
- [AROS MIDIHub](https://github.com/JJDSNT/aros-midihub) — related ecosystem context only, not a dependency
- AHI and AROSTCP APIs: exact source and documentation paths **to be verified during G0/G1**

## Source files to audit first
`src/JackTrip.h`, `src/UdpDataProtocol.cpp`, `src/AudioInterface.h`, `src/RingBuffer.h`, `src/JitterBuffer.cpp`, `src/PacketHeader.h`, `src/RtAudioInterface.cpp`, `meson.build`.

## Evidence convention
For every substantial claim, cite exact upstream revision/file and distinguish inspected code from inferred portability. Record tests before asserting functionality.
