# INFO8985-Inclass-task-4

**Complete observability setup with SigNoz, Kubernetes monitoring, and instrumented Flask app using Ansible**

---

## ✅ Quick Start

```bash
pip install ansible kubernetes
git submodule update --init --recursive
ansible-playbook up.yml
This deployment includes:

SigNoz observability platform (running via Docker on TrueNAS)

Kubernetes infra monitoring stack (Helm chart)

Rolldice Flask app with OpenTelemetry instrumentation

📐 Architecture
nginx

Rolldice App → k8s-infra OTEL Collector → SigNoz (Docker on TrueNAS) → UI Dashboard
Components:
Rolldice App – Flask app generating traces, metrics, and logs

k8s-infra – Kubernetes observability via OTEL Collector

SigNoz – Centralized observability dashboard

🌐 Access Points

SigNoz UI	http://<TrueNAS-IP>:3301
Rolldice App	http://localhost:5000/rolldice
Kubernetes Pods	kubectl get pods 

🧪 Testing Telemetry
Send sample trace:
bash

curl "http://localhost:5000/rolldice?player=keerthana"
Load testing:
bash
for i in {1..50}; do curl http://localhost:5000/rolldice; done
Check SigNoz:
Open the SigNoz UI

Navigate to Services → rolldice-app

View traces, metrics, and logs

⚙️ Configuration
Override OTEL collector settings in values.yaml:

yaml
otelCollector:
  endpoint: "http://<TrueNAS-IP>:4317"

global:
  clusterName: "vsphere-cluster"
  deploymentEnvironment: "dev"
🧹 Teardown
bash
ansible-playbook down.yml
