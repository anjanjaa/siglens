# siglens
LLM-based interpretation layer that converts alerts and events into structured, actionable output for incident response.

Minimal working implementation exposed via a FastAPI service.

---

## Context
Monitoring systems detect anomalies but leave interpretation to operators.

In high-volume environments, alerts often lack context, prioritization, and clear actionability. This creates a gap between detection and response.

SigLens introduces an interpretation layer between these stages, converting observability data into structured outputs that support consistent and faster response.

observability data → interpretation → response

---

## System Context
This repository is part of the SigLens system:

[siglens](https://github.com/anjanjaa/siglens) — interpretation layer (LLM-based analysis)  
[siglens-clustering](https://github.com/anjanjaa/siglens-clustering) — structural layer (semantic grouping of alerts)

---

## System Flow
```
[ Observability Systems ]  
(alerts, metrics, events)   
        ↓  
[ SigLens ]  
(LLM-based implementation)  
        ↓  
structured JSON output  
        ↓  
[ Downstream Systems ]  
(incident response, routing, dashboards)
```

---

## Functionality
Given an alert event, SigLens:
  - summarizes the incident
  - classifies severity
  - suggests likely root causes
  - recommends operational actions

All outputs are returned as structured JSON for integration into downstream systems.

---

## Example
### Input
```json
{
  "alert_name": "HighLatency",
  "service": "satellite-gateway-1",
  "value": 320,
  "threshold": 200
}
```
### Output Analysis
```json
{
  "summary": "Latency spike detected exceeding threshold.",
  "severity": "high",
  "likely_cause": "Network congestion or degraded signal quality",
  "recommended_actions": [
    "Check bandwidth usage",
    "Inspect signal quality",
    "Review recent deployments"
  ]
}
```

---

## Architecture
- FastAPI service for alert ingestion
- LLM-based interpretation engine
- Structured JSON output validation
- Designed for integration with observability systems such as Prometheus and Alertmanager  

## Model Layer
SigLens is designed as a provider-agnostic interface for LLM integration.
### Current implementation
- single-alert analysis pipeline
### Planned
- OpenAI / Gemini / Claude support
- model comparison
- fallback strategies
- provider-independent routing

---

## Tech Stack
- Python
- FastAPI
- Pydantic
- OpenAI API
- Google Gemini API
- Anthropic Claude API

---

## Status
Minimal working v0 focused on single-alert interpretation via a FastAPI interface.

## Direction
- alert clustering using embeddings
- multi-alert correlation
- drift detection across alert patterns
- integration with incident management systems
- context-aware analysis using historical alerts (RAG)
- model fallback strategies
