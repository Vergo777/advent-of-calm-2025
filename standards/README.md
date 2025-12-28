# CALM Governance Standards

Standards in CALM are organization-specific extensions that enforce consistency and compliance across all architectural designs. They are defined using the JSON Schema 2020-12 specification.

## 🏗️ Architectural Extension via `allOf`

CALM uses the `allOf` composition pattern to merge core architectural definitions with our internal standards. This means that a component must satisfy **both** the official CALM schema **and** our company-specific rules to be considered valid.

Example of a standard-compliant node definition:
```json
{
  "$ref": "https://calm.finos.org/release/1.1/meta/core.json#/defs/node"
},
{
  "$ref": "standards/company-node-standard.json"
}
```

---

## 🏢 Company Node Standard
All services, databases, and systems within the organization must follow the requirements defined in `company-node-standard.json`.

### Required Properties:
*   **`costCenter`**: Must follow the pattern `CC-XXXX` (e.g., `CC-1234`). This is critical for automated budget allocation and financial reporting.
*   **`owner`**: The primary team or individual responsible for the component.

### Optional (Enum-Restricted) Properties:
*   **`environment`**: If provided, must be one of: `development`, `staging`, or `production`.

---

## 🔗 Company Relationship Standard
All network connections and data flows between components must follow the requirements defined in `company-relationship-standard.json`.

### Required Properties:
*   **`dataClassification`**: Every relationship must be labeled with its data sensitivity level: `public`, `internal`, `confidential`, or `restricted`.
*   **`encrypted`**: A boolean flag indicating if the data is encrypted in transit. This is strictly audited for all non-public data flows.

---

## ✅ Enforcement
These standards are automatically enforced by the CALM CLI during validation:
```bash
calm validate -a architectures/your-architecture.json
```
If a node is missing an owner or a relationship isn't labeled for encryption, the validation will fail with specific errors pointing to the standard violation.
