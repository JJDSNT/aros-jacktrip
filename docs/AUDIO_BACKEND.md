# AHI audio backend investigation

**Status:** design hypotheses only; no AHI API audit or hardware measurements completed.

## Goal
Capture and play bidirectional low-latency PCM using native AROS AHI while preserving JackTrip's audio periods, channel routing and network buffering.

## Questions to answer from AROS source
- Which AHI APIs and device modes provide capture, playback and full-duplex operation?
- Which sample formats, sample rates, channels and buffer sizes are supported by target drivers?
- Can capture and playback proceed simultaneously with stable clocks?
- How are callbacks, interrupts, tasks and signals scheduled? What can safely run in an audio callback?
- Which conversions and copies are unavoidable?
- How do device and network clocks drift over long sessions?
- What are the latency floor and CPU/memory costs for each AROS target?

## Proposed boundary
```text
AHI capture -> format conversion -> nonblocking queue -> JackTrip network sender
AHI playback <- format conversion <- nonblocking queue <- jitter/network receiver
```

Do not put blocking socket calls, DNS, dynamic allocations or logging in an audio callback.

## Test plan
1. Local loopback with known signal, measure capture-to-playback latency.
2. Full-duplex sustained playback/capture with underrun and overflow counters.
3. 48 kHz mono/stereo PCM at multiple period sizes; record actual supported configurations.
4. Local UDP round trip against desktop JackTrip.
5. 10+ minute drift and loss tests; capture CPU, memory and audio artifacts.

## Evidence needed
Specific AROS AHI source paths, driver capabilities, exact target architecture, audio hardware, commands and measurements. Do not claim generic AHI low-latency or recording support without confirming the relevant backend.
