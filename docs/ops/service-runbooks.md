# Service Runbooks
Generated from architecture: 
Generated on: 

---

## Global Load Balancer
**Unique ID:** `load-balancer`
**Type:** service

### Ownership
| Field | Value |
|-------|-------|
| Owner | platform-team |
| On-Call Slack | #oncall-platform |
| Tier | tier-1 |
| Runbook | https://runbooks.example.com/load-balancer |

### Health & Monitoring
- **Health Endpoint:** `/health`
- **Dashboard:** https://grafana.example.com/d/lb-metrics
- **Log Query:** `service:load-balancer`

### Dependencies
This service depends on:
- api-gateway-1
- api-gateway-2

### Known Failure Modes
No failure modes documented yet.

---
## API Gateway - Instance 1
**Unique ID:** `api-gateway-1`
**Type:** service

### Ownership
| Field | Value |
|-------|-------|
| Owner | platform-team |
| On-Call Slack | #oncall-platform |
| Tier | tier-1 |
| Runbook | https://runbooks.example.com/api-gateway |

### Health & Monitoring
- **Health Endpoint:** `/health`
- **Dashboard:** https://grafana.example.com/d/gw-metrics
- **Log Query:** `service:api-gateway-1`

### Dependencies
This service depends on:
- order-service
- inventory-service

### Known Failure Modes
No failure modes documented yet.

---
## API Gateway - Instance 2
**Unique ID:** `api-gateway-2`
**Type:** service

### Ownership
| Field | Value |
|-------|-------|
| Owner | platform-team |
| On-Call Slack | #oncall-platform |
| Tier | tier-1 |
| Runbook | https://runbooks.example.com/api-gateway |

### Health & Monitoring
- **Health Endpoint:** `/health`
- **Dashboard:** https://grafana.example.com/d/gw-metrics
- **Log Query:** `service:api-gateway-2`

### Dependencies
This service depends on:
- order-service
- inventory-service

### Known Failure Modes
No failure modes documented yet.

---
## Order Service
**Unique ID:** `order-service`
**Type:** service

### Ownership
| Field | Value |
|-------|-------|
| Owner | order-team |
| On-Call Slack | #oncall-orders |
| Tier | tier-1 |
| Runbook | https://runbooks.example.com/order-service |

### Health & Monitoring
- **Health Endpoint:** `/actuator/health`
- **Dashboard:** https://grafana.example.com/d/order-metrics
- **Log Query:** `service:order-service`

### Dependencies
This service depends on:
- order-database-primary
- order-queue

### Known Failure Modes
#### HTTP 503 errors
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Database connection pool exhausted |
| **How to Check** | Check connection pool metrics in Grafana dashboard |
| **Remediation** | Scale up service replicas or increase pool size |
| **Escalation** | If persists &gt; 5min, page DBA team |
#### High latency (&gt;2s p99)
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Payment service degradation |
| **How to Check** | Check payment-service health and circuit breaker status |
| **Remediation** | Circuit breaker should open automatically; check fallback queue |
| **Escalation** | Contact payments-team if circuit breaker not triggering |
#### Order validation failures
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Inventory service returning stale data |
| **How to Check** | Verify inventory-service cache TTL and database replication lag |
| **Remediation** | Clear inventory cache; check replica sync status |
| **Escalation** | Contact platform-team for cache issues |

---
## Inventory Service
**Unique ID:** `inventory-service`
**Type:** service

### Ownership
| Field | Value |
|-------|-------|
| Owner | inventory-team |
| On-Call Slack | #oncall-inventory |
| Tier | tier-2 |
| Runbook | https://runbooks.example.com/inventory-service |

### Health & Monitoring
- **Health Endpoint:** `/health`
- **Dashboard:** https://grafana.example.com/d/inventory-metrics
- **Log Query:** `service:inventory-service`

### Dependencies
This service depends on:
- inventory-database

### Known Failure Modes
#### HTTP 500 errors
| Aspect | Details |
|--------|---------|
| **Likely Cause** | MongoDB replica set failover or primary unavailability |
| **How to Check** | Check MongoAtlas logs and db-connection-lag |
| **Remediation** | Primary selection should be automatic; check service retry logic |
| **Escalation** | Page DBA team if write-lock detected |
#### Stale stock data
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Cache synchronization failure |
| **How to Check** | Compare DB vs Cache stock count for sample product |
| **Remediation** | Flush Redis cache for affected SKUs |
| **Escalation** | Contact platform-team if cache invalidation service is hung |
#### Latency spikes
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Indexing overhead or full table scan |
| **How to Check** | Check slow query logs in MongoDB |
| **Remediation** | Kill long-running queries; review index coverage |
| **Escalation** | Contact DBA team for query optimization |

---
## Payment Service
**Unique ID:** `payment-service`
**Type:** service

### Ownership
| Field | Value |
|-------|-------|
| Owner | payments-team |
| On-Call Slack | #oncall-payments |
| Tier | tier-1 |
| Runbook | https://runbooks.example.com/payment-service |

### Health & Monitoring
- **Health Endpoint:** `/health`
- **Dashboard:** https://grafana.example.com/d/payment-metrics
- **Log Query:** `service:payment-service`

### Dependencies
This service depends on:
- order-queue

### Known Failure Modes
#### HTTP 502/504 errors
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Downstream payment gateway (Stripe/Adyen) timeout |
| **How to Check** | Check external provider status page and egress latency |
| **Remediation** | Retry with exponential backoff; check circuit breaker |
| **Escalation** | Page payment-oncall if gateway is down &gt; 10min |
#### High queue depth
| Aspect | Details |
|--------|---------|
| **Likely Cause** | Consumer processing lag |
| **How to Check** | Check RabbitMQ unsent message count |
| **Remediation** | Horizontal auto-scaling for payment-service instances |
| **Escalation** | Manual intervention if queue doesn&#x27;t clear in 15min |
#### Auth failures
| Aspect | Details |
|--------|---------|
| **Likely Cause** | PCI-compliant token vault access issues |
| **How to Check** | Check secret management service logs |
| **Remediation** | Rotate vault client token; check IAM permissions |
| **Escalation** | Immediate page for Security/Platform-team |

---

## Quick Links
| Service | Health Check | Dashboard | Runbook |
|---------|--------------|-----------|---------|
| Global Load Balancer | `/health` | [Dashboard](https://grafana.example.com/d/lb-metrics) | [Runbook](https://runbooks.example.com/load-balancer) |
| API Gateway - Instance 1 | `/health` | [Dashboard](https://grafana.example.com/d/gw-metrics) | [Runbook](https://runbooks.example.com/api-gateway) |
| API Gateway - Instance 2 | `/health` | [Dashboard](https://grafana.example.com/d/gw-metrics) | [Runbook](https://runbooks.example.com/api-gateway) |
| Order Service | `/actuator/health` | [Dashboard](https://grafana.example.com/d/order-metrics) | [Runbook](https://runbooks.example.com/order-service) |
| Inventory Service | `/health` | [Dashboard](https://grafana.example.com/d/inventory-metrics) | [Runbook](https://runbooks.example.com/inventory-service) |
| Payment Service | `/health` | [Dashboard](https://grafana.example.com/d/payment-metrics) | [Runbook](https://runbooks.example.com/payment-service) |
