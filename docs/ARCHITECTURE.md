# Architecture: upstream and prospective AROS seams

## Upstream observations
JackTrip is a C++ application with transport, buffering, audio interface and UI layers, but the core is **not independent of Qt**. Relevant upstream files:
- `src/JackTrip.h`: central QObject mediator, Qt network/event facilities, audio mode selection
- `src/UdpDataProtocol.cpp`: UDP transport, Qt DNS/synchronization and OS socket handling
- `src/AudioInterface.h`: audio abstraction with Qt container types
- `src/RingBuffer.h`, `src/JitterBuffer.cpp`: buffers with Qt synchronization
- `src/PacketHeader.h`: header model coupled to QObject
- `meson.build`: main build, Qt Core/Network even in nogui mode; C++20 default
- `CMakeLists.txt`: C++17 setting; upstream warns CMake is not officially supported for full builds

## Proposed adaptation boundary (not implemented)

```text
Existing JackTrip client/engine (retain behavior and upstream compatibility)
   |             |                  |
   |             |                  +-- event/thread/time adapter -> AROS Exec / verified APIs
   |             +-- UDP/socket adapter -> AROSTCP / bsdsocket.library
   +-- audio device adapter -> AHI (capture + playback, pending audit)
           |
     native CLI / diagnostics (initially no Qt GUI)
```

There are **two alternative port strategies** to test:
1. Incremental source port: retain upstream classes, substitute Qt dependencies at narrow seams and implement AHI backend.
2. Minimal native interoperable client: implement protocol subset for initial feasibility; use this as a test harness, **not** as proof of a full JackTrip source port.

Prefer (1) for long-term port fidelity; (2) can de-risk packet/audio feasibility. Record divergence and maintenance costs.

## Explicit non-goals for the initial milestone
Qt GUI, Virtual Studio, browser video, WebRTC, WebTransport, plugins, authentication and multi-user hub server. These may be reconsidered after UDP audio interoperability.

## Architecture concerns
- Audio callbacks cannot wait for network or allocations.
- Device period, packet period, jitter queue and clock drift must be measured independently.
- IPv4/IPv6, socket semantics, cancellation and cleanup require AROS validation.
- Big-endian and 32-bit ABI differences can break upstream wire-format assumptions.
