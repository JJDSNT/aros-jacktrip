# Portability audit — initial source-based findings

**Scope:** initial upstream default-branch file inspection, 2026-11-19. Pin a commit before implementation. No AROS compile or runtime validation performed.

| Area | Evidence in upstream | AROS question / action | State |
| --- | --- | --- | --- |
| Language | `meson.build` defaults to C++20; `CMakeLists.txt` sets C++17 | Verify AROS target compiler, STL, atomics and ABI | Open |
| Build | Meson recommended; CMake warns limited support | Choose cross-build or staged compilation | Open |
| GUI | `nogui` disables GUI but not Qt Core/Network | Map Qt usage in headless core | Confirmed upstream |
| Qt runtime | `JackTrip.h`, `AudioInterface.h`, `RingBuffer.h`, `UdpDataProtocol.cpp` | QObject/signals, Qt containers, mutexes, timers, DNS, sockets | Confirmed upstream |
| Audio | JACK and optional RtAudio backends | Audit AHI recording, playback, callback/interrupt semantics | Open |
| Network | UDP POSIX-style sockets and Qt network facilities | Verify bsdsocket.library, IPv4/IPv6, select/poll, timeouts | Open |
| Event wait | `UdpDataProtocol.cpp` uses Linux epoll or non-Linux sys/event.h in a branch | Audit AROS event/wait mechanism; no assumed kqueue | Open |
| Buffers | `RingBuffer.h` uses QMutex/QWaitCondition; jitter code uses QMutexLocker | Replace synchronization safely; quantify memory | Open |
| Wire layout | Raw C struct serialization in `PacketHeader.h` and protocol documentation | Big-endian m68k and alignment interoperability | Open |
| Sample data | Protocol documents 16-bit LE, special 24-bit encoding and float32 raw | Verify endian-safe conversion and IEEE float | Open |
| Optional transports | WebRTC/libdatachannel; WebTransport/msquic | Defer until baseline UDP | Deferred |
| Licensing | Original file headers carry permissive notice | Audit entire dependency tree and license files | Open |

## First executable probes
1. Compile a tiny C++ target with chosen AROS cross-toolchain (atomics, threads, chrono, STL).
2. Build AROSTCP UDP echo/send-receive test, including cancellation and timing.
3. Encode/decode known JackTrip header fixtures across LE and BE hosts, including malformed packets.
4. Verify AHI full-duplex feasibility, supported formats, periods and underrun behavior on real AROS hardware/emulator.
5. Only then attempt linking selected upstream core units.

For each probe log target, compiler version, command line, source revision, memory, CPU, measured timings and raw output. Do not infer AROS support from upstream POSIX portability.
