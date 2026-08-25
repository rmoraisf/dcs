# Contributing to the Distributed Cognitive Stack (DCS)

Thank you for your interest in evolving the network and application stack for AI-native infrastructure. Because this framework aims to bridge cloud-native networking with autonomous agent systems, we welcome rigorous technical debate, critique, and real-world architectural use cases.

## How to Participate

1. **Open an Issue:** Use GitHub issues to debate theoretical assumptions, point out security gaps, or discuss overlapping industry protocols (e.g., MCP, A2A specs, or service mesh extensions).
2. **Submit a Pull Request (PR):** If you want to refine a layer definition, introduce new primitive types, or add a case study:
   - Fork the repository.
   - Create a feature branch (`git checkout -b feature/refine-layer-8`).
   - Submit your PR with a clear summary of *why* the architectural change is necessary.

## Design Principles for Contributions
* **Pragmatism over Purity:** Proposals must anchor to real-world cloud-native components (Kubernetes, Envoy, vector stores, LLM gateways) rather than remaining purely abstract.
* **Security First:** Any addition to Layers 7.5 through 9 must address zero-trust boundaries, credential leakage, or token hygiene.
