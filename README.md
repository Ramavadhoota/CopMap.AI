# 🚓 CopMap AI – Patrolling & Bandobast Intelligence System

An AI-assisted system designed to support Indian police operations such as **patrolling**, **bandobast**, and **nakabandi** by providing real-time risk indicators, alerts, and intelligence summaries — while keeping officers firmly in the decision loop.

---

## 1. Problem Understanding

### Where AI Fits in Police Operations

Modern police operations face challenges such as:
- High crowd density during public events
- Limited manpower
- Delayed situational awareness
- Information overload from CCTV feeds and patrol logs

AI can **realistically assist** by:
- Monitoring scenes continuously
- Highlighting potential risks
- Summarizing large volumes of operational data

AI **should not** replace officers or automate enforcement decisions.

---

### What Is Automated vs Assisted

**Automated (Low-Risk, High-Value)**
- Crowd density estimation
- Object detection (people, vehicles, suspicious items)
- Event logging and aggregation
- Alert triggering based on predefined thresholds

**Assisted (Human-in-the-Loop)**
- Violence confirmation
- Risk interpretation
- Patrol deployment decisions
- Escalation and enforcement actions

All AI outputs are **advisory**, not commands.

---

### Risks of False Positives

Potential risks:
- Misclassification due to lighting or camera angle
- Single-frame noise triggering alerts
- Alert fatigue

Mitigations implemented:
- Temporal aggregation for violence detection
- Conservative confidence thresholds
- Multi-signal validation (vision + time + context)
- Human review before action

---

## 2. System Architecture

### High-Level Flow

CCTV / Video Input
->
Computer Vision Models (YOLO, Violence Detection)
->
Event & Risk Analysis Layer
->
SQL Database + Vector Store (FAISS)
->
LLM (RAG-based Intelligence Summaries)
->
CopMap Backend / Officer Dashboard


---

### Core Components

1. **Vision Layer**
   - YOLOv8 for people, vehicle, and object detection
   - Violence detection using ResNet / CLIP
   - Crowd density estimation

2. **Intelligence Layer**
   - Rule-based risk scoring
   - Temporal violence detection to reduce false positives

3. **Data Layer**
   - SQLite for audit-grade event storage
   - FAISS vector database for semantic retrieval (RAG)

4. **LLM & RAG Layer**
   - FLAN-T5 (open-source)
   - Patrol summaries, risk insights, recommendations

5. **Output Layer**
   - Alerts
   - Patrol intelligence summaries
   - Metrics and reports

---

## 3. Implementation Overview

### What Was Implemented

- Object detection (YOLOv8)
- Crowd density risk analysis
- Violence detection with temporal smoothing
- Suspicious object detection
- SQL-based event storage
- Vector search using FAISS
- LLM-based patrol summaries (RAG)
- Metrics and visualizations
- Exportable reports and evidence logs

### What Was Intentionally Skipped

| Feature | Reason |
|------|-------|
| Facial recognition | Privacy and legal concerns |
| Autonomous enforcement | Human-in-the-loop required |
| Real-time streaming | High infra cost; snapshot-based sufficient for PoC |
| Model retraining pipelines | Out of scope for screening task |

Skipping these was a **deliberate design decision**, not a limitation.

---

## 4. LLM & RAG Usage (Mandatory Requirement)

### Why LLM Is Used

The LLM does **not** make decisions.  
It is used for:
- Summarizing patrol activity
- Highlighting patterns
- Providing operational recommendations

### RAG Flow

Detection Events → Embeddings → FAISS
->
Relevant Context
->
FLAN-T5 Summary


### Cost-Aware Strategy

- Fully open-source models
- No paid APIs
- Short, structured prompts
- Retrieval-first (RAG) approach to limit token usage

This makes the system **government-friendly and deployable**.

---

## 5. Operational Interpretation of AI Outputs

| AI Output | Police Interpretation |
|---------|----------------------|
| High crowd density | Bandobast congestion risk |
| Weapon / suspicious object | Nakabandi escalation risk |
| Sustained violence detection | Immediate patrol attention required |
| Repeated alerts in same zone | Potential hotspot formation |

---

## 6. Output Integration

- AI outputs are exposed as structured data
- Alerts can be pushed to CopMap backend APIs
- Officers consume:
  - Maps
  - Risk indicators
  - Natural-language summaries
- All events are logged for audit and review

---

## 7. Why Google Colab Was Used

Google Colab was chosen to:
- Ensure easy reproducibility for reviewers
- Provide free GPU access
- Avoid local environment setup issues
- Focus evaluation on **approach and thinking**, not infrastructure

This aligns with the screening task’s intent.

---

## 8. Deliverables Included

- ✅ Source code (public GitHub repository)
- ✅ This README
- ✅ Architecture and flow diagrams
- ✅ Sample outputs (JSON, charts)
- ✅ Patrol intelligence summaries
- ✅ Metrics and visualizations
- ✅ Exportable ZIP of reports and database
- ✅ Explanation video (5–10 minutes)

---

## 9. Key Takeaways

- AI is used responsibly and conservatively
- Officers remain the final decision-makers
- System is cost-aware, explainable, and deployable
- Focus is on **practical usefulness**, not feature count

---

## 10. Disclaimer

This project is a **screening-task proof of concept**  
and not a production-deployed law enforcement system.

It is intended to demonstrate:
- Applied AI/ML thinking
- System design clarity
- Awareness of ethical and operational constraints
