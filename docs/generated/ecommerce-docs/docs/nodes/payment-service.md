---
id: payment-service
title: Payment Service
---

## Details
<div className="table-container">
| Field               | Value                    |
|---------------------|--------------------------|
| **Unique ID**       | payment-service                   |
| **Node Type**       | service             |
| **Name**            | Payment Service                 |
| **Description**     | Handles payment processing, PCI compliance, payment gateway integration, and transaction security for all customer payments          |

</div>

## Interfaces
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
                        <b>UniqueId</b>
                    </td>
                    <td>
                        payment-service-api
                            </td>
                </tr>
                <tr>
                    <td>
                        <b>AdditionalProperties</b>
                    </td>
                    <td>
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
                                        <b>Protocol</b>
                                    </td>
                                    <td>
                                        HTTPS
                                            </td>
                                </tr>
                                <tr>
                                    <td>
                                        <b>Host</b>
                                    </td>
                                    <td>
                                        payments.internal.example.com
                                            </td>
                                </tr>
                                <tr>
                                    <td>
                                        <b>Port</b>
                                    </td>
                                    <td>
                                        8443
                                            </td>
                                </tr>
                                <tr>
                                    <td>
                                        <b>Path</b>
                                    </td>
                                    <td>
                                        /api/payments
                                            </td>
                                </tr>
                                </tbody>
                            </table>
                        </div>
                    </td>
                </tr>
                </tbody>
            </table>
        </div>


## Related Nodes
```mermaid
graph TD;
payment-service[payment-service]:::highlight;
order-service -- Connects --> payment-service;
ecommerce-system -- Composed Of --> payment-service;
classDef highlight fill:#f2bbae;

```
## Controls

        ### Compliance

        PCI-DSS compliance for payment processing

        <div className="table-container">
            <table>
                <thead>
                <tr>
                    <th>Requirement URL</th>
                    <th>Config</th>
                </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>
                                <a href="https://www.pcisecuritystandards.org/documents/PCI-DSS-v4.0" target="_blank">
                                    https://www.pcisecuritystandards.org/documents/PCI-DSS-v4.0
                                </a>
                        </td>

                        <td>
                                <a href="https://configs.example.com/compliance/pci-dss-config.json" target="_blank">
                                    https://configs.example.com/compliance/pci-dss-config.json
                                </a>

                        </td>
                    </tr>
                </tbody>
            </table>
        </div>


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
                  <b>Version</b>
              </td>
              <td>
                  3.1.0
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Runtime</b>
              </td>
              <td>
                  Go 1.20
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Protocol</b>
              </td>
              <td>
                  HTTPS
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Data Classification</b>
              </td>
              <td>
                  highly-sensitive
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Tech Owner</b>
              </td>
              <td>
                  Payment &amp; Finance Team
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Repository</b>
              </td>
              <td>
                  https://github.com/example-org/payment-service
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Deployment Type</b>
              </td>
              <td>
                  container
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Sla Tier</b>
              </td>
              <td>
                  tier-1
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Compliance</b>
              </td>
              <td>
                  PCI-DSS Level 1
                      </td>
          </tr>
          </tbody>
      </table>
  </div>
