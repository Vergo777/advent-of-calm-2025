---
architecture: ../architectures/ecommerce-platform.json
---

# Relationship Details: E-commerce order processing platform

### customer-uses-api-gateway


**Type:** Interaction
- **Actor:** `customer`
- **Interacts with:** `api-gateway`


---
### admin-uses-api-gateway


**Type:** Interaction
- **Actor:** `admin`
- **Interacts with:** `api-gateway`


---
### api-gateway-to-order-service

**Type:** Connection

| Property | Value |
|----------|-------|
| Source | `api-gateway` |
| Destination | `order-service` |
| Source Interfaces | `api-gateway-endpoint` |
| Dest Interfaces | `order-service-api` |



---
### api-gateway-to-inventory-service

**Type:** Connection

| Property | Value |
|----------|-------|
| Source | `api-gateway` |
| Destination | `inventory-service` |
| Source Interfaces | `api-gateway-endpoint` |
| Dest Interfaces | `inventory-service-api` |



---
### order-service-to-order-database

**Type:** Connection

| Property | Value |
|----------|-------|
| Source | `order-service` |
| Destination | `order-database` |
| Source Interfaces | `order-service-api` |
| Dest Interfaces | `order-db-connection` |



---
### inventory-service-to-inventory-database

**Type:** Connection

| Property | Value |
|----------|-------|
| Source | `inventory-service` |
| Destination | `inventory-database` |
| Source Interfaces | `inventory-service-api` |
| Dest Interfaces | `inventory-db-connection` |



---
### order-service-to-payment-service

**Type:** Connection

| Property | Value |
|----------|-------|
| Source | `order-service` |
| Destination | `payment-service` |
| Source Interfaces | `order-service-api` |
| Dest Interfaces | `payment-service-api` |



---
### ecommerce-system-composed-of



**Type:** Composition
- **Container:** `ecommerce-system`
- **Contains:** `api-gateway`, `order-service`, `inventory-service`, `payment-service`, `order-database`, `inventory-database`

---
