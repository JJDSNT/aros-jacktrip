# Guidance for contributors and coding agents

This repository is a **standalone JackTrip-to-AROS porting laboratory**, not a TeleMIDI Band integration project.

1. Read README.md and docs/* before proposing implementation.
2. Preserve upstream JackTrip provenance, licenses, copyright notices and protocol interoperability. Pin upstream commit IDs for every source audit or import.
3. Prefer minimal platform adaptations and upstream-friendly seams over unrelated rewrites. Do not claim that removing the GUI removes Qt Core/Network.
4. Distinguish **verified upstream source**, **AROS source evidence**, **hypothesis** and **measured results**. Record exact files/revisions, target architecture, commands, outputs and limitations.
5. Start with a headless UDP interoperability experiment. Qt, C++ toolchain, AHI recording, AROSTCP sockets, timing and thread semantics are open verification gates.
6. Never assume little-endian layout on m68k; verify packet bytes, struct alignment, sample formats, timestamps and hub handshake against upstream.
7. Keep audio callbacks nonblocking; test buffer underrun/overrun, clock drift, packet loss, cancellation and cleanup.
8. No unverified performance, AROS compatibility or feature claims. A document-only change is not a port.
9. Keep work focused and incremental. Do not create branches unless explicitly requested; propose changes on main when authorized.
10. AROS upstream fixes should be justified by independently reproducible platform deficiencies, not port-specific assumptions.
