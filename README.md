# 🤖 SynthAgent — Multi-Agent Decision Simulation (Llama 3.1 + SQLite)

**SynthAgent** simulates a cross-functional leadership team — **CEO, CTO, CIO, PM, Business Analyst, Data Architect, Engineer, Analyst, and Vice President** — that debates a scenario and produces tangible artifacts: **PRD.md, design.md (with Mermaid), exec_summary.md, controls.md, financials.md, forecast.csv**.

- **Free, Local LLM:** Uses **Ollama** with `llama3.1:8b` (no API keys or cloud cost).
- **Free Database:** Uses **SQLite** via SQLAlchemy, auto-migrated on startup.
- **Local-first, Cloud-ready:** The bus/store/LLM are pluggable; you can later swap to GCP (Pub/Sub, Firestore/Cloud SQL, Vertex AI) without changing core logic.

> “Not another chatbot.” It’s a **system**: event-driven orchestration, typed contracts, persistent state, and reproducible artifacts.

---

## ✨ Highlights

- Multi-agent turn engine (event-driven, deterministic order)
- Pluggable LLM (Ollama now; Vertex AI later)
- SQLite persistence (runs, messages, artifacts)
- FastAPI control plane (create runs, start, view transcript & artifacts)
- Artifact generators using Jinja (PRD, design, exec summary, controls, financials + CSV)
- Clean, testable architecture with minimal dependencies

---

## 🧩 Architecture

```mermaid
flowchart LR
  API[FastAPI API] --> ORC[Orchestrator]
  ORC --> BUS[(InMemoryBus)]
  ORC --> DB[(SQLite via SQLAlchemy)]
  ORC --> LLM[Ollama (llama3.1:8b)]
  DB -->|writes| ART[./artifacts/<run_id>]
