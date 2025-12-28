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

---

## 🏗️ Multi-Pattern Validation Strategy

Our architecture governance relies on a layered validation strategy where multiple patterns work together to enforce different requirements.

### 1. How Patterns Work Together
Instead of creating a single, massive pattern that tries to enforce everything, we use a modular approach:
- **Structural Patterns** (e.g., `web-app-pattern.json`): Enforce that an architecture has the correct components and connections for a specific use case.
- **Standards Patterns** (e.g., `company-base-pattern.json`): Enforce that *whatever* components exist, they all contain mandatory corporate metadata (ownership, cost tracking, security classification).

An architecture is considered fully compliant only when it passes **both** validation checks.

### 2. Why Heterogeneous Patterns are Better
This separation of concerns provides several benefits:
- **Scalability**: New structural patterns (e.g., "Microservice Pattern", "Data Pipeline Pattern") can be added without duplicating corporate standard rules.
- **Maintainability**: Changes to corporate standards (e.g., adding a new metadata field) only need to be updated in one place (the Base Pattern).
- **Flexibility**: Teams have architectural freedom within their structural patterns while staying within the "guardrails" of corporate governance.

### 3. Enabling CI/CD Governance
This layered approach is designed for automated CI/CD pipelines:
1. **Developer Pre-check**: Developers validate against the structural pattern locally during design.
2. **Automated Audit**: The CI pipeline runs the `company-base-pattern` validation on every pull request to ensure no unowned or unclassified components are introduced.
3. **Continuous Compliance**: Periodic scans run all architectures against the base pattern to catch drifted configurations or newly released corporate standards.

### 4. Current Pattern Library
| Pattern File | Type | Purpose |
| :--- | :--- | :--- |
| `web-app-pattern.json` | **Structural** | Mandates a 3-tier web client, service, and database stack. |
| `company-base-pattern.json` | **Standards** | Mandates corporate ownership, finance, and security properties. |
