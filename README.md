# siglens
LLM-based interpretation layer that converts alerts and events into structured, actionable output for incident response.

Minimal working implementation exposed via a FastAPI service.

## Components
- FastAPI ingestion endpoint
- LLM-based interpretation layer
- Structured output interface (JSON)
- Minimal single-alert analysis pipeline

---

## Context
Monitoring systems detect anomalies but leave interpretation to operators.

In high-volume environments, alerts often lack context, prioritization, and clear actionability.
This creates a gap between detection and response.

The interpretation layer sits between detection and response, converting observability data into structured output for action.
It reduces cognitive load and enables consistent handling.

observability data → interpretation → response

## Flow
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

- Summarizes the incident
- Classifies severity
- Suggests likely root causes
- Recommends operational actions

All outputs are returned as structured JSON for integration into downstream systems.

## Example
Example transformation from raw alert to structured output:

### Input Alert
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
    "Review recent deployments",
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
SigLens is designed for provider-agnostic LLM integration.

The first version focuses on single-alert analysis. Planned extensions include:
- OpenAI / Claude provider support
- Model comparison
- Fallback strategies
- Provider-independent routing

---

## Tech Stack
- Python
- FastAPI
- Pydantic
- OpenAI API
- Anthropic Claude API

---

## Current Status
Minimal working v0 focused on single-alert analysis via a FastAPI interface.

## Future Extensions
- Alert clustering using embeddings
- Multi-alert correlation
- Drift detection across alert patterns
- Slack/incident tool integration
- Context-aware analysis using historical alerts (RAG)

- Model fallback strategies

