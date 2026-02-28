# sockshop_mircoservices_k8s
Deployed Helidon-based Sockshop microservices application on Kubernetes cluster. Implemented service communication, MySQL database integration, environment configuration, and debugging of production-level issues like CrashLoopBackOff and 500 Internal Server errors.

# Project overview
This project deploys the Helidon-based Sockshop microservices application on Kubernetes.
The application is an online store that sells socks and is based on the canonical SockShop Microservices Demo originally written and published under the Apache 2.0 license by Weaveworks.

## 🏗️ Microservices Deployed

The following microservices were deployed and configured:

- Users Service
- Orders Service
- Payment Service
- Shipping Service
- Cart Service
- Catalog Service
- Frontend Service
  
Each service was deployed using custom Kubernetes manifests.

---

## ⚙️ Kubernetes Implementation

For each microservice, I implemented:

- Dedicated Namespace for isolation
- Deployment manifests
- ClusterIP Services for internal communication
- ConfigMaps for configuration management
- Secrets for sensitive data (DB credentials)
- Environment variable injection
- Liveness and Readiness Probes (for selected services)
- Proper label and selector configuration
- Resource configuration to prevent memory issues

All services communicate internally using Kubernetes DNS-based service discovery.

---

## 🛠️ Database Integration

- Integrated MySQL databases for relevant services
- Configured DB host, port, and credentials using environment variables
- Used Kubernetes Service names for internal DB communication
- Verified service endpoints and connectivity

---

## 🧪 Troubleshooting & Production Debugging

During deployment, several real-world issues were encountered and resolved:

### 1️⃣ CrashLoopBackOff
- Identified container restart loops
- Used `kubectl logs --previous` for root cause analysis
- Fixed missing environment variables and DB connection issues

### 2️⃣ OOMKilled
- Detected memory limit failures
- Adjusted container resource limits
- Verified pod stability after changes

### 3️⃣ 500 Internal Server Errors
- Traced backend service logs
- Verified service-to-service communication
- Validated database connectivity
- Fixed misconfigured environment variables

### 4️⃣ Service Communication Issues
- Verified endpoints using `kubectl get endpoints`
- Ensured correct label-selector matching
- Confirmed internal DNS resolution using service names

---

## 🚀 Deployment Steps

```bash
kubectl create namespace sockshop
kubectl apply -f k8s/
kubectl get pods -n sockshop
