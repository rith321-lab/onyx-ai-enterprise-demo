# AI Enterprise Search & Insights Demo  
### Presentation Guide for Elisabeth & Aaron  

---

## 1&nbsp;&nbsp;Purpose of This Demo  
Showcase a **fully-functional, Canadian-compliant AI enterprise search solution** built on the open-source **Onyx** platform, using fictional “Northern Tech Solutions” data.  
The demo covers every requirement Aaron outlined:

| Requirement | Where It Appears in Demo |
|-------------|-------------------------|
| Canadian data-centres & privacy | Compliance badges on every page, talking point §4 |
| LLM model flexibility | Model selector in chat sidebar (GPT-4o, Claude-3, DeepSeek) |
| Text + relational augmentation | PDF RAG in *Document Chat* & SQL/Chart fusion in *Interactive Charts* |
| Hallucination mitigation | Source citations, confidence labels, guard-rail text |
| Maintenance UX | Config files (.env.canadian) + drag-and-drop doc ingestion |
| REST integration | `/api/v1/query` endpoint (curl sample in §5) |

---

## 2&nbsp;&nbsp;Local Quick-Start (No Docker Needed)

| Step | Command / Action |
|------|------------------|
| 1. Clone demo repo | `git clone https://github.com/onyx-dot-app/onyx.git onyx-demo` |
| 2. Enter project      | `cd onyx-demo/demo` |
| 3. Launch static server (any)** | `python -m http.server 8088` |
| 4. Open in browser    | visit `http://localhost:8088/interactive-charts-demo.html` (*charts page*)<br>open new tab `http://localhost:8088/document-chat-demo.html` (*doc chat*) |

> **Any static server works – VS Code “Live Server” plugin, `npx serve`, or simple double-clicking files if security settings allow.

---

## 3&nbsp;&nbsp;Demo Flow & Narration

### 3.1 Intro (1 min)
1. Welcome – “All data in this demo is mock but **physically located in Canada** (see maple-leaf banners).”
2. High-level architecture slide (optional) – Onyx → Vespa → LLM adapters.

### 3.2 Interactive Charts + Relational Chat (5 min)
1. **Filters**: change *Date Range* → note KPI tiles animate.  
2. **Revenue Forecast graph**: mention AI forecast (red dashed line) & confidence shading.  
3. **LLM Chat (right sidebar)**:  
   * Ask “What drove Q1 2024 revenue growth?”  
   * Highlight model dropdown → switch from GPT-4o to Claude-3; ask follow-up.  
4. **Predictive section**: click 🔄 refresh icons to show real-time inference.

> Talking point: “Structured data lives in Postgres; we generate SQL from the user’s question, fetch rows, then feed context & chart to the LLM.”

### 3.3 Document Chat with Memory (5 min)
1. Library left-pane: pick *SecureVault Manual* → preview loads.  
2. Ask in chat: “Summarize key encryption features.” → show citations.  
3. **Live ingestion**:  
   * Click *Add Sample Document* or drag any PDF – watch processing banner.  
   * Ask: “What’s new in the AI Integration Whitepaper?” → assistant answers, memory badge increments.  
4. Click **Memory → Clear** to demonstrate privacy controls.

### 3.4 Wrap-Up (2 min)
* Emphasise **hallucination mitigation** (citations, confidence colours).  
* Show **REST sample** in §5 for integration.  
* Outline production deployment path (Docker → K8s in Canadian VPC).

Total runtime ≈ **12 minutes**.

---

## 4&nbsp;&nbsp;Key Talking Points

1. **Canadian Data Residency** – Geo-fenced storage, encryption keys held in-region.  
2. **Model Flexibility** – Any provider reachable via LiteLLM proxy; cost/latency trade-offs.  
3. **Hybrid Retrieval (RAG)** – Vespa vector + BM25; recency decay; avoids hallucinations.  
4. **Live Document Addition** – <5 s from upload to searchable; zero service restarts.  
5. **Compliance Dashboard** – Maps controls to PIPEDA, CPPA, SOC 2 (see screenshot).  
6. **Ease of Maintenance** – YAML/ENV config, drag-and-drop connectors, role-based UI.

---

## 5&nbsp;&nbsp;Sample REST Query

```bash
curl -X POST http://localhost:8080/api/v1/query \
  -H "Authorization: Bearer <API_KEY>" \
  -H "Content-Type: application/json" \
  -d '{
        "question": "List high-risk customers by revenue impact",
        "model": "gpt-4o",
        "top_k": 5
      }'
```

Response includes answer JSON, citations, and SQL snippet executed.

---

## 6&nbsp;&nbsp;Troubleshooting

| Symptom | Fix |
|---------|-----|
| Charts not loading | Ensure you opened via `http://` static server; some browsers block file:// XHR |
| Fonts/icons missing | Internet required for CDN links (FontAwesome, Chart.js) |
| PDF preview blank | Disable browser pop-up blockers or test in Chrome/Edge |
| Memory doesn’t clear | Hard refresh page (session storage cache) |

---

## 7&nbsp;&nbsp;Moving from Demo → Production

1. Copy `.env.canadian` into `deployment/docker_compose` and run:  
   `docker compose -f docker-compose.prod.yml --env-file .env.canadian up -d`
2. Point DNS to NGINX load-balancer in AWS/GC ca-central-1 or on-prem.  
3. Configure SSO (AzureAD, Okta) in Onyx settings.  
4. Add real connectors (SharePoint, Jira, Salesforce) and re-index.

---

### Contact  
Rishi Kalakuntla · **AI Solutions Architect**  
rishi.kalakuntla@northerntech.ca · +1 416-555-1000
