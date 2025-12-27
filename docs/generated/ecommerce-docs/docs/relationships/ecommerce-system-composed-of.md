---
id: ecommerce-system-composed-of
title: Ecommerce System Composed Of
---

## Details
<div className="table-container">
| Field               | Value                    |
|---------------------|--------------------------|
| **Unique ID**       | ecommerce-system-composed-of                   |
| **Description**      |  Contains all core platform services and supporting infrastructure   |
</div>

## Related Nodes
```mermaid
graph TD;
ecommerce-system -- Composed Of --> api-gateway;
ecommerce-system -- Composed Of --> order-service;
ecommerce-system -- Composed Of --> inventory-service;
ecommerce-system -- Composed Of --> payment-service;
ecommerce-system -- Composed Of --> order-database;
ecommerce-system -- Composed Of --> inventory-database;

```

## Controls
    _No controls defined._

## Metadata
  _No Metadata defined._
