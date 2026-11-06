# Architecture & Data Flow

```mermaid
graph TD
    subgraph Client Layer
        UI[Tessera Labs AI Operations Dashboard]
        WS[Webhook Simulator / Ingestion API]
    end

    subgraph Kubernetes Cluster / Azure AKS
        NS[Namespace: operations]
        ING[Service / Ingress: NodePort 30080 or AKS LoadBalancer (Preferred)]
        POD[Nginx Pod / On-Call App]
    end

    subgraph External Integrations
        AI[Gemini AI Diagnostics API]
        SMTP[Notification Dispatcher / Email API]
    end

    WS -->|Ingest Incident| UI
    UI -->|Look up Active Shift| UI
    UI -->|Trigger Alert Payload| SMTP
    UI -->|Send Error Logs & Context| AI
    AI -->|Return Triage & Playbook| UI
    UI -->|Append Audit Trail| UI

    POD --- ING
    ING --- UI