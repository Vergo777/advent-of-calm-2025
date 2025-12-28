# CALM Architecture Patterns

Patterns in CALM are reusable, instantiable architecture templates defined as JSON schemas. They represent the "blueprints" for your system designs.

## 🚀 The Dual Superpowers of Patterns

Patterns provide a two-fold advantage for architecture management:

1.  **Generation (Speed)**: Use patterns to instantly bootstrap new architectures with the correct nodes and relationships already in place. It eliminates the blank-page problem and ensures teams start with a standard baseline.
2.  **Validation (Governance)**: Once an architecture is created, the pattern remains a contract. You can validate any architecture against its original pattern to ensure that critical components haven't been removed and that the core structure remains compliant with your organizational standards.

---

## 🛠️ Using the Web Application Pattern

The `web-app-pattern.json` defines a standard 3-tier application stack.

### 1. Generation
To bootstrap a new architecture instance from this pattern:
```bash
calm generate -p patterns/web-app-pattern.json -o my-app.json
```

### 2. Validation
To verify that an existing architecture still conforms to the 3-tier standard:
```bash
calm validate -p patterns/web-app-pattern.json -a my-app.json
```

---

## 🛡️ Enforcement Rules

This pattern enforces a strict structural contract:

*   **Node Integrity**: The architecture MUST contain exactly 3 nodes with these specific IDs:
    *   `web-frontend` (node-type: `webclient`)
    *   `api-service` (node-type: `service`)
    *   `app-database` (node-type: `database`)
*   **Relationship Strictness**: The architecture MUST contain exactly 2 relationships connecting the layers:
    *   `frontend-to-api`: Links the `web-frontend` to the `api-service`.
    *   `api-to-database`: Links the `api-service` to the `app-database`.

---

## 🎨 Flexibility & Extensibility

While the core structure is rigid, the following areas remain flexible for project-specific needs:

*   **Descriptions**: You can (and should) provide custom descriptions for every node and relationship to explain its specific business purpose.
*   **Interfaces**: You are free to add network interfaces (host, port, protocol) to the nodes as your infrastructure details emerge.
*   **Metadata**: Supplemental information like `version`, `owner`, or `repository` links can be added to any node.
*   **Controls**: You can attach security, compliance, or residence controls to both nodes and relationships without breaking the core pattern contract.

---

## 🛡️ Corporate Governance: Company Base Pattern

The `company-base-pattern.json` is a specialized governance-only pattern. Instead of defining *what* should be in your architecture, it defines the *rules* every component must follow.

### 📋 Enforcement Rules
This pattern enforces our organization's **Standards** across all components:
- **Every Node** must have:
    - `costCenter`: Formatted as `CC-XXXX`.
    - `owner`: A designated team or individual.
- **Every Relationship** must have:
    - `dataClassification`: Sensitivity level (public, internal, confidential, or restricted).
    - `encrypted`: Explicit boolean for transit security.

### ⚖️ Structure vs. Property Enforcement

| Feature | Web Application Pattern | Company Base Pattern |
| :--- | :--- | :--- |
| **Primary Goal** | Standardize **Structure** | Standardize **Compliance** |
| **Node Count** | Fixed (exactly 3) | Infinite / Flexible |
| **Relationship Count** | Fixed (exactly 2) | Infinite / Flexible |
| **Enforcement** | Must have specific IDs and types | Must have specific properties |
| **Use Case** | Bootstrapping a new 3-tier app | Auditing any existing or new system |

### 🛠️ Use Cases: Which pattern to use?
- Use **Web Application Pattern** when starting a new project to ensure you follow the standard Tier-1 stack architecture.
- Use **Company Base Pattern** for all existing architectures to audit them for corporate governance compliance.

### 🏗️ Local Standard Validation
Since our Standards use canonical URLs that aren't yet published, you must use the **URL Mapping** file when validating locally:

```bash
calm validate -p patterns/company-base-pattern.json -a my-architecture.json -u url-mapping.json
```
The `-u` flag tells the validator to map the remote standard URLs (e.g., `https://example.com/standards/...`) to your local `./standards/` directory components.
