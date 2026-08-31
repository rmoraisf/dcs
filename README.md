# The Distributed Cognitive Stack (DCS v0.3.0): A Unified Protocol and SecOps Reference Model for the Internet of Agents

> **Status:** Draft / Open Request for Comments (RFC)  
> **Version:** 0.3.0  
> **Maintainers:** Open for community contributions

## Abstract
Traditional network stacks (OSI and TCP/IP) were engineered for deterministic, syntactic data transport between hosts, stopping short of defining how applications or autonomous entities share meaning[cite: 1]. While containerized microservice architectures successfully distributed compute, the rapid rise of Large Language Models (LLMs) and autonomous multi-agent systems has exposed a critical architectural gap: workloads no longer communicate solely via syntactic request-response cycles, but instead negotiate intent, share fluid context windows, and execute actions via protocol envelopes[cite: 1]. 

This manifesto unifies the **Internet of Agents (IoA)** architectural framework—originally proposed by Fleming et al. (Cisco Research) to establish an Agent Communication Layer (L8) and an Agent Semantic Layer (L9) above application transport[cite: 1]—with an orthogonal **SecOps & Observability Plane**. By merging protocol-level semantic coordination with enterprise-grade threat modeling, trust boundaries, and per-layer telemetry, DCS provides a complete reference model for building, debugging, and securing next-generation multi-agent infrastructure.

---

## 1. Introduction: The Limits of the Seven-Layer Paradigm
For decades, network engineering has relied on deterministic transport boundaries. Even as applications evolved into containerized microservices managed by service meshes, the fundamental contract of Layer 7 remained unchanged: it assumes a client talks to a known endpoint expecting a syntactic response[cite: 1]. 

Today, that assumption breaks down as multi-agent systems coordinate complex tasks[cite: 1]. Current protocols like A2A[cite: 1], MCP[cite: 1], and FIPA-ACL[cite: 1] successfully standardize the *syntax* of messages (envelopes, task structures, performatives) but cannot enforce semantic agreement[cite: 1]. This leaves systems vulnerable to two critical failure modes identified in IoA research[cite: 1]:
1. **Syntax Without Semantic Context:** Terms like "switch" parse correctly as syntax strings but remain ambiguous without a shared domain model, forcing expensive, non-deterministic LLM clarification loops[cite: 1].
2. **Semantic Underspecification:** Messages can be syntactically valid yet missing core execution parameters (e.g., booking a flight without dates or airports), leading to execution failures or costly conversational retries[cite: 1].

Following the historical precedent of how HTTP evolved to fill the gap between transport and web applications[cite: 1], the **Internet of Agents (IoA)** architecture establishes formal protocol layers above transport[cite: 1]. DCS integrates these layers while adding the operational security and observability matrix required for production environments.

---

## 2. The Two-Dimensional Architectural Blueprint
The DCS framework intersects the structural layers of agent communication (building directly on the IoA model) with a cross-cutting security and observability plane.

| Layer | Domain | Primary Protocols & Primitives | Core Function |
| :--- | :--- | :--- | :--- |
| **Layer 9** | **Agent Semantic Layer (SL)** | Shared Context URNs, Handshakes (`SL-HELLO`), Consensus Primitives | Establishes protocol-level semantic discovery, grounding, validation, and population-wide consensus[cite: 1]. |
| **Layer 8** | **Agent Communication Layer (ACL)** | A2A, MCP, Speech Acts (`REQUEST`, `INFORM`), Interaction Patterns | Standardizes message envelopes, communicative intent, and interaction flows independently of meaning[cite: 1]. |
| **Layer 7** | **Application Transport Layer** | HTTP/2, HTTP/3, gRPC, SLIM, mTLS | Leverages binary framing, stream multiplexing, and end-to-end encryption for reliable transport[cite: 1]. |
| **Layers 1–6** | **Traditional Lower Stack** | TCP, IP, Ethernet, Physical Media | Delivers raw packets between underlying host infrastructure[cite: 1]. |

---

## 3. Technical Specifications & SecOps Matrix

### Layer 7: Application Transport Layer
* **Structural Primitives:** HTTP/2 and HTTP/3 framing, stream multiplexing, and Message Layer Security (MLS) via protocols like SLIM[cite: 1].
* **Trust Boundaries:** Host-to-host and container-to-container encrypted transport channels.
* **Threat Model:** Packet sniffing, transport-layer interception, and unauthorized routing.
* **Required Telemetry:** Connection health, stream latencies, mTLS status, and packet-drop rates.
* **Controls:** Transport-layer encryption (TLS/MLS) and network segmentation policies[cite: 1].

### Layer 8: Agent Communication Layer (The Synapse)
* **Structural Primitives:** Standardized message envelopes, speech-act performatives (`REQUEST`, `AGREE`, `PROPOSE`, `INFORM`), and interaction patterns (Request-Reply, Publish-Subscribe, Aggregation) as defined in IoA[cite: 1].
* **Trust Boundaries:** Cross-agent peer communication and task delegation across transient container lifecycles[cite: 1].
* **Threat Model:** Agent impersonation, delegation-depth recursion bombs, and message-envelope spoofing.
* **Required Telemetry:** Agent-to-agent transaction traces, message delivery status, and delegation depth counters.
* **Controls:** Signed **Agent Cards** (adding system-prompt hash attestation and explicit delegation depth limits on top of base A2A standards).

### Layer 9: Agent Semantic Layer (The Teleology)
* **Structural Primitives:** Context discovery handshakes (`SL-HELLO`, `SL-SELECT`, `SL-LOCK`), versioned Shared Context URNs (`urn:contexts:...`), formal schemas (JSON-LD, Protobufs), and state consensus primitives[cite: 1].
* **Trust Boundaries:** The semantic perimeter between raw L8 message payloads and the agent’s internal reasoning engine (LLM/rules engine)[cite: 1].
* **Threat Model (MITRE ATLAS / OWASP LLM):** 
  * *Semantic Injection:* Malicious instructions embedded inside syntactically/semantically valid fields (e.g., overriding system instructions via tool results)[cite: 1].
  * *Context Poisoning/Spoofing:* Malicious registries serving modified Shared Context definitions[cite: 1].
  * *Semantic Denial of Service (SDoS):* Flooding agents with ambiguous requests to exhaust LLM inference budgets[cite: 1].
  * *Semantic Downgrade Attacks:* Forcing negotiation of older, vulnerable context versions[cite: 1].
* **Required Telemetry:** Semantic validation failure logs, context handshake latencies, drift indicators, and guardrail trigger rates.
* **Controls:** 
  * *Authenticated Contexts:* Cryptographically signed context definitions validated against trusted Schema Authorities (SAs)[cite: 1].
  * *Semantic Firewalls:* Inline filters positioned between the SL and application logic to enforce concept-level authorization and rate limits[cite: 1].
  * *Confidentiality of Capability:* Encrypting capability advertisements during `SL-HELLO` handshakes via extended MLS channels[cite: 1].

---

## 4. References & Attribution
* **Foundational Architecture:** Fleming, C., Muscariello, L., Pandey, V., & Kompella, R. (2026). *A Layered Protocol Architecture for the Internet of Agents*. Cisco Research. arXiv:2511.19699[cite: 1].

## 5. Contributing & Feedback
This unified specification combines the protocol taxonomy of the Internet of Agents with enterprise operational rigor. We invite platform engineers, network architects, and AI researchers to stress-test these definitions.
* Open an **Issue** or submit a **Pull Request** to refine layer definitions or expand the SecOps matrix.
