
# Day 20 — Kubernetes Health, Resources & Autoscaling

## Objective
Configure a Kubernetes Deployment with startup, readiness, and liveness
probes, CPU/memory requests and limits, QoS classification, Metrics Server,
and Horizontal Pod Autoscaler (HPA).

## Technologies
- Kubernetes
- kubectl
- Metrics Server
- Horizontal Pod Autoscaler
- BusyBox load generator

## Workload
- Namespace: day20-health
- Deployment: php-apache
- Image: registry.k8s.io/hpa-example
- Initial replicas: 1
- HPA CPU target: 50%
- Minimum replicas: 1
- Maximum replicas: 5

## Resource Configuration
| Resource | Request | Limit |
|---|---:|---:|
| CPU | 200m | 500m |
| Memory | 64Mi | 128Mi |

## Health Probes
- Startup probe: allows time for application initialization.
- Readiness probe: controls whether the Pod receives Service traffic.
- Liveness probe: detects failed health checks and can trigger a restart.

## QoS
Expected class: Burstable. Requests and limits are configured, but they
are not equal for CPU and memory.

## HPA and Load Test
Document the observed CPU utilization and replica counts before, during,
and after load testing. Do not claim scaling success unless it was observed.

## Readiness Failure Test
Temporarily changed the readiness endpoint to /wrong-path, observed probe
failure, and restored the endpoint to /.

Readiness failure removes the Pod from eligible Service endpoints.
Liveness failure can restart the container. Startup probes protect
slow-starting applications during initialization.

## Troubleshooting
- Metrics API unavailable: check Metrics Server and its APIService.
- HPA CPU unknown: check metrics and CPU requests.
- No scaling: inspect HPA conditions, events, load, and CPU utilization.
- OOMKilled: inspect memory usage, limits, logs, and Pod events.

## Screenshots
Store lab evidence in the screenshots/ directory.
