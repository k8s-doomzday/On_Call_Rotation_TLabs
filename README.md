# AI On-Call Operations Console (Tessera Labs)

An enterprise-grade, zero-dependency AI On-Call Operations & Automated Incident Remediation platform featuring real-time incident management, simulated webhook ingestion, automated engineer notification dispatching, and Gemini AI root-cause diagnostic playbooks.

---

## Project Structure

oncall-ops-poc/
├── .vscode/                 # IDE workspace configuration & settings
├── chart/                   # Helm chart deployment package
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       ├── deployment.yaml
│       ├── namespace.yaml
│       └── service.yaml
├── Dockerfile               # Nginx container definition
├── azure-pipelines.yml      # CI/CD pipeline definition for Azure AKS
├── index.html               # Single-file React & Tailwind application
└── README.md                # Project documentation

## Local Deployment

Utilizing Rancher-Desktop and Helm for local validation testing. End-User can use their choice of local kubernetes environment. From root directory, user simply can run:

docker build -t oncall-ops:latest .
helm apply --install oncall-ops ./chart


## Evidence of Successful Run

### Visual Demo
![Dashboard Overview](docs/screenshots/2-dashboard-oncall.png)

### Incident Ingestion & AI Triage Playbook
![AI Root Cause Analysis](docs/screenshots/3-incident-ai-triage.png)

### Terminal & Kubernetes Deployment
![Kubernetes Deployment](docs/screenshots/1-cluster-deployment.png)

### Video Walkthrough
A short video demonstration of the incident dispatch and AI triage workflow is available at [`docs/demo.mp4`](docs/demo.mp4).

---

## Assumptions, Trade-offs & Security

### Architectural & Operational Assumptions
* **Single-Page Application Scope:** Built as a standalone Nginx container serving a zero-friction React/Tailwind frontend to eliminate external backend database setup requirements for local evaluation.
* **Cluster Access:** Assumes local access to a k3s/Rancher Desktop cluster with default storage and networking drivers.

### Security Awareness
* **Secret Management:** Sensitive credentials (such as Azure Service Principals and API keys) are injected dynamically via Azure DevOps Pipeline secrets / Kubernetes Secrets rather than stored in repository files.
* **RBAC & Isolation:** The application deploys to a dedicated `operations` namespace to ensure workload isolation and apply strict Role-Based Access Control (RBAC).
* **Ingress Security:** Local deployment uses NodePort for simplicity; production AKS deployment expects SSL/TLS termination at the ingress controller.

### Observability & Future Enhancements
* **Metrics & Logging:** Production deployments should integrate Prometheus metrics (`/metrics`) and structured JSON logs forwarded to Azure Log Analytics or Datadog.
* **Persistent Storage:** Incident history currently operates in-memory for the POC; production architecture should back this with an enterprise datastore (e.g., PostgreSQL / Azure Cosmos DB).