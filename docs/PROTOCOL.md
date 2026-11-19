# JackTrip network protocol: porting checklist

**Authoritative upstream description:** [NetworkProtocol.md](https://github.com/jacktrip/jacktrip/blob/main/docs/Documentation/NetworkProtocol.md). This document is a checklist, not a replacement specification.

## Baseline
- Traditional stream: UDP datagrams with default header and planar (channel-major) audio payload.
- Default header fields: timestamp uint64; sequence uint16; buffer samples uint16; sample-rate enum uint8; bit resolution uint8; incoming/outgoing channel counts uint8 each (nominal 16-byte structure).
- Upstream serializes a native C struct with memcpy, without explicit header endian conversion. **m68k is big-endian; validate ABI layout and encode/decode compatibility rather than memcpying host structs.**
- Network samples: 8-bit signed, 16-bit little-endian signed, 24-bit custom 3-byte encoding, 32-bit float raw bytes (endianness assumptions).
- Wire samples are planar; internal samples may be interleaved.
- Optional redundancy concatenates newest and older complete packets.
- UDP stop datagram: 63 bytes of 0xFF.
- P2P UDP server mode uses the first received datagram as the peer endpoint; hub modes use a TCP port exchange and may require TLS/auth.

## Interoperability acceptance fixtures
- Known byte vectors for 16-byte default header on LE and BE targets.
- Sequence wrap, malformed lengths, channel count limits, sample rate and bit-depth mismatches.
- 16-bit stereo PCM, 24-bit custom representation, 32-bit float and planar/interleaved conversion.
- UDP redundancy recovery, reordered/lost datagrams, stop control handling.
- Peer handshake and error paths only after basic P2P passes.

## Additional transport research (deferred)
Upstream documents WebRTC **unreliable unordered data channels** using libdatachannel and WSS signaling; WebTransport uses QUIC datagrams via msquic. Both carry the same JackTrip audio packet format, but are separate dependency/portability projects.

## Security and robustness
Treat peer packet lengths and fields as untrusted. Preserve upstream validation behavior and add cross-architecture tests. Do not expose unauthenticated UDP services beyond a controlled test network before threat review.
