# Incident Post-Mortem: Load Balancer Health Check Misconfiguration

## 1. Affected Services and Tiers
The incident impacted our most critical backend infrastructure, all classified as **Tier-1**:
*   **Global Load Balancer (Tier-1)**: Logical entry point and source of the misconfiguration.
*   **API Gateway - Instance 2 (Tier-1)**: Erroneously marked unhealthy; 0% traffic.
*   **API Gateway - Instance 1 (Tier-1)**: Overloaded (100% traffic load), leading to cascading latency.
*   **Order Service (Tier-1)**: Degraded performance and eventual timeout errors.
*   **Inventory Service (Tier-2)**: Intermittent unavailability.

## 2. Business Flows Impacted
*   **Customer Order Processing (`order-processing-flow`)**: Primary impact. The synchronous portion of the checkout flow (Gateway → Order Service) failed due to Gateway saturation.
*   **Inventory Stock Check (`inventory-check-flow`)**: Administrative access to stock data was blocked, preventing inventory updates during the surge.

## 3. Customer Impact (Per Flow Metadata)
*   **Direct Impact**: Customers were unable to complete purchases, resulting in **direct revenue loss**.
*   **Customer Experience**: Users observed high latency followed by checkout errors. Per our incident metadata, the frontend displayed the **"Order processing delayed"** message.
*   **Downstream Resilience**: Since we implemented **ADR-0001 (Async Processing)**, any orders that *did* successfully reach the `order-service` were safely queued in RabbitMQ and processed as the system recovered.

## 4. Timeline of Dependency Failure
1.  **T-0**: Misconfiguration in the **Load Balancer** health check initiated.
2.  **T+2m**: **API Gateway 2** was marked unhealthy; entry-point relationship `load-balancer-to-gateway-2` was severed.
3.  **T+5m**: **API Gateway 1** received 100% of global traffic. Latency spiked to 5s+, triggering the `GW_RateLimit_Exceeded` alert.
4.  **T+8m**: **Order Service** circuit breaker opened due to high failure rates from the overloaded Gateway, preventing further backend saturation but stopping checkouts.

## 5. Remediation Steps Taken
*   **Isolate**: Used the **[API Gateway Grafana Dashboard](https://grafana.example.com/d/gw-metrics)** to identify the traffic imbalance.
*   **Recover**: Manually overrode the health check state for **API Gateway 2** to restore traffic distribution.
*   **Stabilize**: Increased the connection pool size on **Order Service** temporarily (per its Failure Mode remediation) to handle the surge of retried requests.

## 6. Follow-up Actions (Recurrence Prevention)
*   **Improve Controls**: Add an architecture-level **Resilience Control** requiring health check validation tests before deployment to the Load Balancer.
*   **Enhanced Monitoring**: Implement a new alert for **"Unbalanced Gateway Traffic"** (Alert if Instance-1 vs Instance-2 traffic delta > 20%).
*   **Capacity Tuning**: Re-evaluate the **Tier-1** capacity of a single Gateway instance; it should be able to handle 100% of peak traffic during a failover without saturating (current configuration failed this "N+1" test).
*   **Documentation Update**: Update the **Runbook** for the Load Balancer with specific instructions for "False Unhealthy" gateway recovery.
