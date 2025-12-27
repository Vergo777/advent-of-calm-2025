---
id: api-gateway
title: API Gateway
---

## Details
<div className="table-container">
| Field               | Value                    |
|---------------------|--------------------------|
| **Unique ID**       | api-gateway                   |
| **Node Type**       | service             |
| **Name**            | API Gateway                 |
| **Description**     | Centralized entry point for all client requests, handling routing, authentication, rate limiting, and load balancing across microservices          |

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
                        api-gateway-endpoint
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
                                        api.ecommerce.example.com
                                            </td>
                                </tr>
                                <tr>
                                    <td>
                                        <b>Port</b>
                                    </td>
                                    <td>
                                        443
                                            </td>
                                </tr>
                                <tr>
                                    <td>
                                        <b>Path</b>
                                    </td>
                                    <td>
                                        /api/v1
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
api-gateway[api-gateway]:::highlight;
customer -- Interacts --> api-gateway;
admin -- Interacts --> api-gateway;
api-gateway -- Connects --> order-service;
api-gateway -- Connects --> inventory-service;
ecommerce-system -- Composed Of --> api-gateway;
classDef highlight fill:#f2bbae;

```
## Controls

        ### Performance

        API Gateway rate limiting and caching requirements

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
                                <a href="https://internal-policy.example.com/performance/rate-limiting" target="_blank">
                                    https://internal-policy.example.com/performance/rate-limiting
                                </a>
                        </td>

                        <td>
                                <a href="https://configs.example.com/gateway/rate-limits.yaml" target="_blank">
                                    https://configs.example.com/gateway/rate-limits.yaml
                                </a>

                        </td>
                    </tr>
                    <tr>
                        <td>
                                <a href="https://internal-policy.example.com/performance/caching-policy" target="_blank">
                                    https://internal-policy.example.com/performance/caching-policy
                                </a>
                        </td>

                        <td>
                                <table>
                                    <thead>
                                    <tr>
                                        <th>Key</th>
                                        <th>Value</th>
                                    </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>default-ttl-seconds</td>
                                            <td>300</td>
                                        </tr>
                                        <tr>
                                            <td>cache-control</td>
                                            <td>private</td>
                                        </tr>
                                    </tbody>
                                </table>

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
                  1.5.0
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Framework</b>
              </td>
              <td>
                  Kong
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
                  public
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Tech Owner</b>
              </td>
              <td>
                  Platform Engineering Team
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Repository</b>
              </td>
              <td>
                  https://github.com/example-org/api-gateway
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
          </tbody>
      </table>
  </div>
