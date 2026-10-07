# Architecture

NEXSEC is organized around a controlled security lifecycle. Each stage produces evidence and state that the next stage can use; discovering something does not automatically grant permission to control it.

```mermaid
flowchart LR
  A[Discovery] --> B[Authority Discovery]
  B --> C[Classification]
  C --> D[IT Authorization]
  D --> E[Access Provisioning]
  E --> F[Integration]
  F --> G[Capability Validation]
  G --> H[Controlled Enforcement]
  H --> I[Baseline]
  I --> J[Continuous Watch]
```

## Lifecycle

| Stage | What it answers |
|---|---|
| Discovery | What exists on the networks NEXSEC can see? |
| Authority Discovery | Which devices might control or enforce policy here? |
| Classification | What is each asset, and how confident is that assessment? |
| IT Authorization | Has the responsible operator approved NEXSEC to use the authority? |
| Access Provisioning | How can NEXSEC safely reach the approved authority? |
| Integration | Is there a supported adapter for the device or service? |
| Capability Validation | What can the integration actually do? |
| Controlled Enforcement | Which actions are permitted by policy and authorization? |
| Baseline | What does normal activity and structure look like? |
| Continuous Watch | What has changed since the last trusted observation? |

## Architectural boundary

NEXSEC is designed to operate as an ordinary security peer/sensor unless an authorized integration explicitly gives it another role. It does not assume that being present on a network makes it the gateway or gives it administrative control.

This distinction is central to the architecture:

**Visibility ≠ authorization ≠ access ≠ capability ≠ enforcement.**

## Evidence flow

Each important lifecycle transition should be explainable in terms of observed evidence, authorization state, integration state, capability validation, and the policy governing the next action.

The public repository intentionally omits implementation details such as internal modules, database schema, exact detection rules, adapter internals, credentials, and operational configuration.
