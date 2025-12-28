# Business Flow Support Guide
**Architecture:** 
**Generated:** 

This guide documents each business flow, the services involved, and troubleshooting steps for support teams.

---

## Customer Order Processing
**Description:** End-to-end flow from customer placing an order to payment confirmation

### Business Impact
| Aspect | Details |
|--------|---------|
| **Impact** | Customers cannot complete purchases - direct revenue loss |
| **SLA** | 99.9% availability, 30s p99 latency |
| **Degraded Mode** | Orders queue in message broker; processed when service recovers |
| **Customer Message** | Display &#x27;Order processing delayed&#x27; message |

### Flow Path
This flow traverses the following relationships:

| Step | Relationship | Description |
|------|--------------|-------------|
| 1 | `customer-to-load-balancer` | Customer submits order via web interface |
| 2 | `load-balancer-to-gateway-1` | Load balancer forwards to Gateway 1 |
| 3 | `api-gateway-1-to-order-service` | API Gateway routes order to Order Service |
| 4 | `order-service-to-order-queue` | Order Service publishes payment request to queue |
| 5 | `order-queue-to-payment-service` | Payment Service consumes payment request from queue |

### Troubleshooting Checklist
When this flow is degraded:
1. Check the health endpoints for each service in the flow
2. Review circuit breaker status between services
3. Check message broker queue depths (if async)
4. Review recent deployments to services in this flow
5. Check database replication lag

### Escalation
If this flow is critical (tier-1), escalate immediately to the service owners.

---
## Inventory Stock Check
**Description:** Admin checks and updates inventory stock levels

### Business Impact
| Aspect | Details |
|--------|---------|
| **Impact** | Stock levels may be inaccurate - risk of overselling |
| **SLA** | 99.5% availability, 500ms p99 latency |
| **Degraded Mode** | Fall back to cached inventory; flag orders for manual review |
| **Customer Message** | Display &#x27;Stock availability being confirmed&#x27; |

### Flow Path
This flow traverses the following relationships:

| Step | Relationship | Description |
|------|--------------|-------------|
| 1 | `admin-to-load-balancer` | Admin requests inventory status |
| 2 | `load-balancer-to-gateway-2` | Load balancer forwards to Gateway 2 |
| 3 | `api-gateway-2-to-inventory-service` | Route to inventory service |
| 4 | `inventory-service-to-inventory-database` | Query current stock levels |
| 5 | `inventory-service-to-inventory-database` | Return stock data |
| 6 | `api-gateway-2-to-inventory-service` | Return inventory report |

### Troubleshooting Checklist
When this flow is degraded:
1. Check the health endpoints for each service in the flow
2. Review circuit breaker status between services
3. Check message broker queue depths (if async)
4. Review recent deployments to services in this flow
5. Check database replication lag

### Escalation
If this flow is critical (tier-1), escalate immediately to the service owners.

---

## Quick Reference: All Flows
| Flow | Business Impact | SLA |
|------|-----------------|-----|
| Customer Order Processing | Customers cannot complete purchases - direct revenue loss | 99.9% availability, 30s p99 latency |
| Inventory Stock Check | Stock levels may be inaccurate - risk of overselling | 99.5% availability, 500ms p99 latency |
