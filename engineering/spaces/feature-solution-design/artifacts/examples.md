# Rancang — Illustrative Typed Representations (Not Project Standards)

> **CAUTION:** These are *fictional, conditional examples* for choosing and checking an artifact representation. They are **not** approved project API endpoints, business rules, schemas, security mechanisms, Design requirements or output-format mandates. Use current project-owned conventions and formal standards first. Do not write shared/protected specs without separate authorization. See [artifact precedence](README.md#precedence-and-selection).

## Example A — OpenAPI when the project actually uses HTTP contracts

Use the project's accepted OpenAPI version, source path, field naming, authentication, error format and generation tooling. The sample below is intentionally small and illustrates a response contract, not a production specification. **Do not copy it unchanged into an authorized project.**

```yaml
openapi: 3.1.0
info:
  title: Illustrative Item Lookup
  version: 0.0.0-example
paths:
  /items/{itemId}:
    get:
      operationId: getExampleItem
      summary: Illustrative lookup only
      parameters:
        - name: itemId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Example record returned
          content:
            application/json:
              schema:
                type: object
                required: [id, state]
                properties:
                  id:
                    type: string
                  state:
                    type: string
                    enum: [available, unavailable]
        '404':
          description: Example record absent
        '503':
          description: Example lookup temporarily unavailable
```

**Contract review:** A real project must define actual data authority, access control, result/error vocabulary, and all needed positive/negative outcomes. Nothing here states that every API must use REST, bearer authentication, this path, these status codes or these example states. If downstream requires machine-readable OpenAPI, align exact published source/revision with the project's owning API process; an O2 draft is not binding by itself.

## Example B — Sequence diagram for a material time/order question

Use only if timing, system boundaries, races or intermediate unknown results matter. The project's current diagram style wins when different. The diagram is an **illustration**, not proof of implementation or a substitute for textual state/invariant definitions.

```mermaid
sequenceDiagram
    actor Actor
    participant Client
    participant Service
    participant Store
    Actor->>Client: Request permitted action
    Client->>Service: Submit request (correlation reference)
    Service->>Store: Evaluate and record authoritative outcome
    alt Confirmed outcome
        Store-->>Service: Committed result
        Service-->>Client: Confirmed response
        Client-->>Actor: Show supported result
    else Result unknown / response lost
        Service--xClient: Response unavailable
        Client-->>Actor: Show uncertainty, not success
        Note over Client,Service: Re-check by project-approved method if available
    end
```

In a real assignment, source acceptance decides whether a record can be queried, what effects are atomic, which actors may retry and what can be truthfully displayed. These must be aligned with O2/O3 and O4. **Never invent recovery or identity mechanisms to make an example look complete.**

## Choose a smaller or different representation when appropriate

- For one local invariant, a source-anchored table and verification condition may be sufficient.
- For long-lived workflow states, a state-transition table or state diagram may be clearer than a sequence diagram.
- For event/message consumers, use the project's approved event schema, AsyncAPI or other typed contract instead of forcing HTTP/OpenAPI.
- For human-facing experience obligations, O3 state tables and original Design authority may be more useful than UI wireframes.

[Actual output semantics](../contracts.md) · [Logical templates](templates.md)
