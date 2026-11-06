# Product Requirements Document (PRD)
## AI On-Call Operations — Tessera Labs AI

### 1. Objective
Provide a lightweight, zero-friction AI-assisted incident management and on-call dispatch platform. The system bridges real-time incident ingestion, engineer schedule routing, automated alerts, and safe AI root-cause triage.

### 2. Core User Workflows
1. **Schedule Visibility:** Engineers and leads view real-time primary and secondary on-call coverage shifts.
2. **Incident Ingestion:** Incidents are created via simulated UI triggers, webhooks, or API payloads.
3. **Automated Dispatch:** System resolves the active on-call engineer and triggers an immediate email notification payload.
4. **AI Root-Cause Triage:** Gemini AI ingests incident error logs and stack traces to synthesize root-cause summaries, confidence scores, and safe, step-by-step diagnostic playbooks.
5. **Timeline Recording:** Every action—alert trigger, AI triage generation, and engineer resolution—is recorded chronologically in the incident timeline.

### 3. Non-Functional Requirements
* **Zero-Friction Deployment:** Standalone container serving single-file frontend for instant local evaluation via Helm (`helm upgrade --install`).
* **Cloud Parity:** Helm values dynamically configure for NodePort (local testing) or LoadBalancer (Azure AKS cloud production).
* **Operational Safety:** AI acts strictly in an advisory role (Human-in-the-Loop) to prevent unauthorized production execution.