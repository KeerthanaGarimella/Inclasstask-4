# INFO8985-Inclass-task-4

**Complete observability setup with SigNoz, k8s-infra monitoring, and instrumented Flask app**

## ✅ Quick Start

```bash
pip install ansible kubernetes
git submodule update --init --recursive
ansible-playbook up.yml
This deployment includes:

SigNoz observability platform (running on Docker in TrueNAS)

k8s-infra monitoring stack (deployed using Helm on vSphere Kubernetes)

Rolldice Flask app with OpenTelemetry instrumentation

🧱 Architecture

nginx

Rolldice App → k8s-infra OTEL Collector → SigNoz → Visualization

🔹 Components
Rolldice App: Flask app that emits traces, logs, and metrics

k8s-infra: Kubernetes observability agents using OpenTelemetry

SigNoz: Central platform for storing and visualizing telemetry

📍 Access Points

SigNoz UI: http://localhost:8080
Rolldice App: http://localhost:5000/rolldice
Kubernetes: kubectl get pods -n default

Testing Telemetry
# Generate test data
curl "http://localhost:5000/rolldice?player=alice"

# Generate load test
for i in {1..50}; do curl http://localhost:5000/rolldice; done
Verify telemetry in SigNoz UI → Services → rolldice-app

Configuration
Edit override-values.yaml to customize:

otelCollectorEndpoint: SigNoz collector endpoint
global.clusterName: Your cluster identifier
global.deploymentEnvironment: Environment name

Teardown

ansible-playbook down.yml