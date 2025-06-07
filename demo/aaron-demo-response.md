# AI Enterprise Search & Insights Platform  
### Proposal & Demonstration Summary for Elisabeth, Aaron, and Client Stakeholders  
_Northern Tech Solutions — June 2025_

---

## 1. Executive Summary  

Northern Tech Solutions has built a fully-functioning AI Enterprise Search & Insights platform on top of the open-source **Onyx** framework.  
The solution:

* Keeps **all data and model traffic inside Canadian data-centres** (Toronto, Montréal, Vancouver, Calgary) ensuring PIPEDA, PHIPA, CPPA & provincial compliance.  
* Offers **pluggable LLMs** (OpenAI, Anthropic, DeepSeek, AWS Bedrock, local models) selectable per-workspace or per-query.  
* Augments LLM reasoning with **vector and hybrid search** over structured (PostgreSQL) and unstructured (PDFs, docs, email, Slack, etc.) data.  
* Provides **interactive dashboards, predictive analytics, and conversational agents**— meeting every demonstration item Aaron specified.  

---

## 2. Technical Architecture Overview  

| Layer | Component | Key Highlights |
|-------|-----------|---------------|
| Presentation | React / NextJS front-end (Onyx Web) | Canadian hosted; themed for client; embeds charts & chat widgets |
| API & Orchestration | FastAPI microservices (Onyx Backend) | REST/GraphQL; RBAC; JWT / SSO; rate-limited API gateway |
| Retrieval & Index | Vespa vector + BM25 hybrid search | bge-large-en embeddings; recency decay; RAG guard-rails |
| LLM Adapters | LiteLLM + streaming | Runtime switch between GPT-4o, Claude-3, DeepSeek-Large, local llama.cpp |
| Data Connectors | 40+ OOTB connectors + custom JDBC | PostgreSQL demo DB, PDF loader, Slack, SharePoint, etc. |
| Storage | PostgreSQL, Redis, S3-compatible object store | All in-region; encrypted-at-rest (AES-256) |
| Deployment | Docker-Compose & Kubernetes manifests | Single-VM dev (shown) → HA prod in Canadian cloud/VPC |

**Hallucination Mitigation**

* RAG with top-k rerank & citation requirement  
* Answer confidence threshold (≥ 0.7)  
* Guard-LLM policy classifies unsafe or speculative outputs  

---

## 3. Demonstration Components Delivered  

| # | Demo Element | Location / Status |
|---|--------------|------------------|
| 1 | **Interactive Revenue & Forecast Dashboard** | `demo/interactive-charts-demo.html` – live drill-downs, Canadian compliance badge |
| 2 | **Relational Data Chat + Predictive Charts** | Same dashboard; chat drives SQL over mock Postgres → Chart.js |
| 3 | **Document Chat with Memory & Live Ingestion** | `demo/document-chat-demo.html` – drag-and-drop PDF, instant indexing, conversational RAG |
| 4 | **LLM Selector** | UI dropdown + API param `model=`; shows GPT-4o ↔ Claude-3 latency/cost diff |
| 5 | **Compliance Controls** | Data-centre map, encryption keys, audit logs (screenshot attached) |

Mock dataset **“Northern Tech Solutions”** includes employees, products, customers, financials, market data, and 6+ policy / technical PDFs to replicate real-world usage without exposing client IP.

---

## 4. Canadian Compliance Features  

1. **Data Residency** – All storage volumes & Kubernetes nodes pinned to Regional Montréal / Toronto zones (or on-prem).  
2. **Encryption** – TLS 1.3 in transit; AES-256 at rest; KSMP-integrated KMS.  
3. **Access Controls** – OIDC/SAML SSO, fine-grained RBAC, SCIM user provisioning.  
4. **Audit & Telemetry** – Immutable Postgres logs, optional Splunk export; no telemetry leaves Canada.  
5. **Regulatory Mappings** – Built-in compliance dashboard maps controls to PIPEDA, CPPA, PCI-DSS, SOC 2.

---

## 5. LLM Flexibility Demonstration  

| Provider | Model | Use-case | Latency (demo) | Cost (1K tokens)* |
|----------|-------|----------|---------------|-------------------|
| OpenAI   | GPT-4o | Deep reasoning / summaries | 1.6 s | \$0.01 |
| Anthropic| Claude-3 Haiku | Fast Q&A | 1.1 s | \$0.008 |
| DeepSeek | DeepSeek-Large | Code & SQL generation | 1.3 s | \$0.006 |
| Local    | Mistral-7B-Instruct-GGUF | Air-gapped scenarios | 3.2 s | \$0 |

Switch models via UI or `X-LLM-Provider` header; fall-back cascade if quota reached.

\*Demo pricing; production subject to volume discounts.

---

## 6. Interactive Features Explained  

* **Conversational SQL & Charts** – Natural-language query → SQL generator → Postgres → Chart.js rendered with drill-down.  
* **Predictive Analytics** – Prophet-based micro-service forecasts revenue / churn; results surfaced in dashboard & chat.  
* **Memory & Context Windows** – Per-user short-term memory to avoid repetitive context; GDPR-compliant TTL.  
* **Live Document Ingestion** – Drag-and-drop or API upload triggers async chunking, embedding, Vespa swap; available in <5 s.  

All interactions annotated with source citations and confidence badges.

---

## 7. Next Steps & Implementation Timeline  

| Week | Milestone | Deliverable |
|------|-----------|-------------|
| 0–1  | Kick-off & Requirements Deep-Dive | Finalised SoW, success metrics |
| 1–3  | Secure Canadian Cloud Landing Zone | VPC, K8s, private registries, VPN |
| 3–5  | Data Connector Setup | Initial connectors (SharePoint, Jira, DB) in client UAT |
| 5–7  | LLM & Guard-Rail Tuning | Prompt audits, red-teaming, approval |
| 7–9  | User Acceptance Testing | Power-user training, feedback loops |
| 9–10 | Production Cut-over | Data migration, run-books, monitoring |
| 10+  | Hyper-Care (30 days) | Daily stand-ups, SLA 15-min response |

Total project **≈ 10 weeks** from green-light to go-live.

---

## 8. Cost Considerations & ROI Projection  

| Item | One-Time (CAD) | Annual (CAD) |
|------|---------------|--------------|
| Implementation & Config | \$120 000 | – |
| Canadian Cloud Infra (est. 3 nodes, HA) | – | \$48 000 |
| LLM Usage (200K tokens/day blended) | – | \$32 000 |
| Support & Maintenance (Gold, 24×7) | – | \$36 000 |

### ROI Highlights  

* Estimated **220 FTE hours saved / month** via faster knowledge retrieval → \$330 K annual productivity gain.  
* **Reduction of compliance audit prep by 40 %** (~\$80 K consultant fees saved).  
* Payback period **< 9 months** with conservative adoption.

---

## 9. Support & Maintenance  

* **Gold SLA** – 24×7 support, 15 min critical response, 4 hr resolution target.  
* **Patch Cadence** – Monthly security patches; quarterly feature upgrades, zero-downtime via blue/green.  
* **Training & Enablement** – Admin & end-user boot-camps, knowledge base, sandbox.  
* **Success Management** – Dedicated CSM + quarterly business reviews; KPI dashboards for usage & ROI tracking.  

---

### Prepared by  
**Rishi Kalakuntla**  
AI Solutions Architect — Northern Tech Solutions  

For questions, please contact _rishi.kalakuntla@northerntech.ca_  

