---
id: order-service-to-payment-service
title: Order Service To Payment Service
---

## Details
<div className="table-container">
| Field               | Value                    |
|---------------------|--------------------------|
| **Unique ID**       | order-service-to-payment-service                   |
| **Description**      |  Requests payment processing for confirmed orders   |
</div>

## Related Nodes
```mermaid
graph TD;
order-service -- Connects --> payment-service;

```

## Controls
    _No controls defined._

## Metadata
  <div className="table-container">
      <table>
          <thead>
          <tr>
              <th>Key</th>
              <th>Value</th>
          </tr>
          </thead>
          <tbody>
          <tr>
              <td>
                  <b>Latency Sla</b>
              </td>
              <td>
                  &lt; 500ms
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Monitoring</b>
              </td>
              <td>
                  true
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Encryption</b>
              </td>
              <td>
                  TLS 1.3
                      </td>
          </tr>
          </tbody>
      </table>
  </div>
