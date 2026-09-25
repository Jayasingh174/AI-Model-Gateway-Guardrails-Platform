# AI Model Gateway & Guardrails Platform

An enterprise-oriented AI gateway platform designed to provide a secure, reliable, and controlled interface for LLM applications.

The platform combines **MCP-based service communication, authentication and authorization, PII protection, streaming guardrails, rate limiting, model routing, and fallback handling** into a modular architecture.

## 🚀 Key Capabilities

* **MCP Server** — Exposes structured AI/service functionality through an MCP-compatible interface.
* **MCP Gateway** — Handles authentication, authorization, request validation, and policy enforcement.
* **LLM Guardrails** — Detects and redacts sensitive Personally Identifiable Information (PII) from streaming LLM responses.
* **Model Router** — Routes requests between primary and secondary model endpoints with rate limiting and fallback support.
* **Usage Tracking** — Maintains request/usage information for controlled model access.
* **Automated Tests** — Includes component-level tests for the major platform modules.

## 🏗️ Architecture

```text
                    Client Application
                           │
                           ▼
                  ┌──────────────────┐
                  │   MCP Gateway    │
                  │                  │
                  │ Auth / Policies  │
                  │ Request Control  │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │    MCP Server    │
                  │                  │
                  │ Structured Tools │
                  │ Service Layer    │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │  LLM Guardrail   │
                  │                  │
                  │ PII Detection    │
                  │ Stream Redaction │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │   Model Router   │
                  │                  │
                  │ Rate Limiting    │
                  │ Primary Model    │
                  │ Fallback Model   │
                  └────────┬─────────┘
                           │
                    ┌──────┴──────┐
                    ▼             ▼
              Primary Model   Secondary Model
```

## 📁 Project Structure

```text
AI-Model-Gateway-Guardrails-Platform/
│
├── mcp-server/
│   ├── __init__.py
│   ├── models.py
│   ├── server.py
│   └── tests.py
│
├── mcp-gateway/
│   ├── __init__.py
│   ├── auth.py
│   ├── gateway.py
│   ├── policy.py
│   └── tests.py
│
├── llm-guardrail/
│   ├── __init__.py
│   ├── gateway.py
│   ├── pii_patterns.py
│   ├── stream_redactor.py
│   └── tests.py
│
├── model-router/
│   ├── __init__.py
│   ├── rate_limiter.py
│   ├── router.py
│   ├── usage_store.py
│   └── tests.py
│
├── .gitignore
├── requirements.txt
└── README.md
```

## 🔐 Security & Guardrails

The platform is designed around several security controls:

### Authentication & Authorization

The gateway provides request-level authentication and authorization before allowing access to downstream services.

### PII Protection

The guardrail layer identifies configurable PII patterns and redacts sensitive information from LLM output streams.

Example:

```text
Original:
My email is user@example.com and my phone is 9876543210.

Processed:
My email is [REDACTED] and my phone is [REDACTED].
```

### Rate Limiting

The model router applies request limits to control model usage and prevent uncontrolled traffic.

### Model Fallback

When the primary model endpoint is unavailable or cannot process a request, the router can fall back to a secondary model endpoint.

## 🧩 Technology Stack

| Area           | Technologies                                      |
| -------------- | ------------------------------------------------- |
| Language       | Python                                            |
| API / Services | HTTP, REST-style services                         |
| AI Integration | LLM API endpoints                                 |
| Protocol       | Model Context Protocol (MCP)                      |
| Security       | Authentication, Authorization, Policy Enforcement |
| Guardrails     | PII Detection & Redaction                         |
| Routing        | Primary / Secondary Model Routing                 |
| Storage        | SQLite                                            |
| Testing        | Pytest                                            |
| Development    | Git, GitHub, VS Code                              |

## ⚙️ Configuration

Create a local `.env` file for development configuration.

Example:

```env
PRIMARY_URL=http://localhost:9100/generate
SECONDARY_URL=http://localhost:9200/generate
DOWNSTREAM_URL=http://localhost:8001/mcp
UPSTREAM_URL=http://localhost:9000/generate
```

Do not commit real API keys, credentials, tokens, or other secrets to the repository.

## 🛠️ Installation

Clone the repository and create a virtual environment:

```bash
git clone https://github.com/Jayasingh174/AI-Model-Gateway-Guardrails-Platform.git

cd AI-Model-Gateway-Guardrails-Platform

python -m venv .venv
```

Activate the environment on Windows:

```bash
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## 🧪 Running Tests

Run the available tests with:

```bash
pytest
```

Individual components can also be tested independently depending on the module configuration.

## 🔄 Request Flow

A typical request follows this flow:

```text
Client
  │
  ▼
Authentication
  │
  ▼
Authorization / Policy Check
  │
  ▼
MCP Service
  │
  ▼
LLM Guardrail
  │
  ├── PII Detection
  └── Stream Redaction
  │
  ▼
Model Router
  │
  ├── Primary Model
  │
  └── Secondary Model (Fallback)
  │
  ▼
Controlled Response
```

## 🎯 Engineering Focus

This project demonstrates practical implementation of:

* AI application infrastructure
* LLM gateway design
* MCP service integration
* Authentication and authorization
* LLM output safety
* PII detection and redaction
* Streaming response processing
* Rate limiting
* Model fallback strategies
* Usage persistence
* Modular Python architecture
* Automated testing

## 🔮 Future Improvements

Potential extensions include:

* JWT/OAuth-based authentication
* Redis-backed distributed rate limiting
* Request tracing and observability
* Structured audit logging
* Prometheus metrics
* OpenTelemetry integration
* Configurable policy management
* Model health checks
* Circuit breakers
* Token and latency monitoring
* Containerized deployment
* Cloud deployment
* LLM evaluation and safety metrics

## 👩‍💻 Author

**Jaya Singh**

AI Engineer focused on **LLM applications, RAG systems, AI agents, FastAPI, and intelligent automation**.

GitHub: [Jayasingh174](https://github.com/Jayasingh174)
