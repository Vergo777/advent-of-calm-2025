---
id: index
title: Welcome to CALM Documentation
sidebar_position: 1
slug: /
---

# Welcome to CALM Documentation

This documentation is generated from the **CALM Architecture-as-Code** model.

## High Level Architecture
```mermaid
C4Deployment

    Deployment_Node(deployment, "Architecture", ""){
        Person(customer, "Customer", "End user who browses products, places orders, and manages purchases through the e-commerce platform")
        Person(admin, "Administrator", "System administrator who manages inventory, monitors orders, and performs system maintenance")
        Deployment_Node(ecommerce-system, "E-Commerce Platform", "Complete e-commerce platform encompassing API gateway, order processing, inventory management, and payment services with supporting databases"){
            Container(api-gateway, "API Gateway", "", "Centralized entry point for all client requests, handling routing, authentication, rate limiting, and load balancing across microservices")
            Container(order-service, "Order Service", "", "Manages order creation, processing, status tracking, and order history for customers")
            Container(inventory-service, "Inventory Service", "", "Manages product inventory, stock levels, warehouse locations, and inventory synchronization across channels")
            Container(payment-service, "Payment Service", "", "Handles payment processing, PCI compliance, payment gateway integration, and transaction security for all customer payments")
            Container(order-database, "Order Database", "", "Primary database storing order records, customer order history, order status, and transaction details")
            Container(inventory-database, "Inventory Database", "", "Database for storing product catalog, stock levels, warehouse assignments, and inventory transactions")
        }
    }

    Rel(customer,api-gateway,"Interacts With")
    Rel(admin,api-gateway,"Interacts With")
    Rel(api-gateway,order-service,"Connects To")
    Rel(api-gateway,inventory-service,"Connects To")
    Rel(order-service,order-database,"Connects To")
    Rel(inventory-service,inventory-database,"Connects To")
    Rel(order-service,payment-service,"Connects To")

    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="2")
```
## Nodes
    - [Customer](nodes/customer)
    - [Administrator](nodes/admin)
    - [API Gateway](nodes/api-gateway)
    - [Order Service](nodes/order-service)
    - [Inventory Service](nodes/inventory-service)
    - [Payment Service](nodes/payment-service)
    - [Order Database](nodes/order-database)
    - [Inventory Database](nodes/inventory-database)
    - [E-Commerce Platform](nodes/ecommerce-system)

## Relationships
    - [Customer Uses Api Gateway](relationships/customer-uses-api-gateway)
    - [Admin Uses Api Gateway](relationships/admin-uses-api-gateway)
    - [Api Gateway To Order Service](relationships/api-gateway-to-order-service)
    - [Api Gateway To Inventory Service](relationships/api-gateway-to-inventory-service)
    - [Order Service To Order Database](relationships/order-service-to-order-database)
    - [Inventory Service To Inventory Database](relationships/inventory-service-to-inventory-database)
    - [Order Service To Payment Service](relationships/order-service-to-payment-service)
    - [Ecommerce System Composed Of](relationships/ecommerce-system-composed-of)


## Flows
    - [Customer Order Processing](flows/order-processing-flow)
    - [Inventory Stock Check](flows/inventory-check-flow)

## Controls
| Requirement URL               | Category    | Scope        | Applied To                |
|-------------------------------|-----------|--------------|---------------------------|
|https://internal-policy.example.com/performance/rate-limiting|performance|Node|api-gateway|
|https://www.pcisecuritystandards.org/documents/PCI-DSS-v4.0|compliance|Node|payment-service|
|https://internal-policy.example.com/audit/transaction-logging|audit|Flow|order-processing-flow|

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
                  <b>Owner</b>
              </td>
              <td>
                  ecommerce-team@example.com
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Version</b>
              </td>
              <td>
                  1.0.0
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Created</b>
              </td>
              <td>
                  2025-12-07
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Description</b>
              </td>
              <td>
                  E-commerce order processing platform
                      </td>
          </tr>
          <tr>
              <td>
                  <b>Tags</b>
              </td>
              <td>
                  <ul>
                      <li>ecommerce</li>
                      <li>microservices</li>
                      <li>orders</li>
                  </ul>
              </td>
          </tr>
          </tbody>
      </table>
  </div>

## Adrs
- [docs/adr/0001-use-message-queue-for-async-processing.md](docs/adr/0001-use-message-queue-for-async-processing.md)
- [docs/adr/0002-use-oauth2-for-api-authentication.md](docs/adr/0002-use-oauth2-for-api-authentication.md)
