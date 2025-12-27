---
architecture: ../architectures/ecommerce-platform.json
---

# Node Inventory: E-commerce order processing platform

| Name | Type | ID | Description |
|------|------|-------|-------------|
| Customer | Actor | `customer` | End user who browses products, places orders, and manages purchases through the e-commerce platform |
| Administrator | Actor | `admin` | System administrator who manages inventory, monitors orders, and performs system maintenance |
| API Gateway | Service | `api-gateway` | Centralized entry point for all client requests, handling routing, authentication, rate limiting, and load balancing across microservices |
| Order Service | Service | `order-service` | Manages order creation, processing, status tracking, and order history for customers |
| Inventory Service | Service | `inventory-service` | Manages product inventory, stock levels, warehouse locations, and inventory synchronization across channels |
| Payment Service | Service | `payment-service` | Handles payment processing, PCI compliance, payment gateway integration, and transaction security for all customer payments |
| Order Database | Database | `order-database` | Primary database storing order records, customer order history, order status, and transaction details |
| Inventory Database | Database | `inventory-database` | Database for storing product catalog, stock levels, warehouse assignments, and inventory transactions |
| E-Commerce Platform | System | `ecommerce-system` | Complete e-commerce platform encompassing API gateway, order processing, inventory management, and payment services with supporting databases |

## Services Only
- **API Gateway** (`api-gateway`): Centralized entry point for all client requests, handling routing, authentication, rate limiting, and load balancing across microservices
- **Order Service** (`order-service`): Manages order creation, processing, status tracking, and order history for customers
- **Inventory Service** (`inventory-service`): Manages product inventory, stock levels, warehouse locations, and inventory synchronization across channels
- **Payment Service** (`payment-service`): Handles payment processing, PCI compliance, payment gateway integration, and transaction security for all customer payments

## Databases Only
- **Order Database** (`order-database`): Primary database storing order records, customer order history, order status, and transaction details
- **Inventory Database** (`inventory-database`): Database for storing product catalog, stock levels, warehouse assignments, and inventory transactions

## Actors
- **Customer**: End user who browses products, places orders, and manages purchases through the e-commerce platform
- **Administrator**: System administrator who manages inventory, monitors orders, and performs system maintenance
