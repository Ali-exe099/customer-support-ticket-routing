# Workflow Diagrams

**Document version:** 1.0  
**Status:** Proposed workflow; not a production process map

The diagrams use Mermaid flowchart syntax so they render in GitHub. They are workflow illustrations, not formal BPMN 2.0 models.

## 1. Dataset-level current view

The source dataset contains text fields and existing labels. It does not describe who assigned those labels or the sequence of operational steps.

```mermaid
flowchart LR
    A[Ticket subject and body] --> B[Existing ticket type label]
    A --> C[Existing support queue label]
    A --> D[Existing priority label]
    A --> E[Answer and tag fields]
```

## 2. Proposed future-state workflow

```mermaid
flowchart TD
    A([Ticket available from existing platform]) --> B[Receive ticket record]
    B --> C{Ticket ID and usable text present?}
    C -- No --> M[Manual handling path]
    C -- Yes --> D{Language supported?}
    D -- No --> M
    D -- Yes --> E[Prepare subject and body text]
    E --> F[Recommend ticket type, queue and priority]
    F --> G[Calculate confidence and prepare rationale]
    G --> H{Confidence meets approved threshold?}
    H -- No --> M
    H -- Yes --> I[Show recommendation to support agent]
    M --> J[Agent reviews ticket manually]
    I --> K{Agent accepts recommendation?}
    K -- Yes --> L[Confirm recommended values]
    K -- No --> N[Agent selects final values]
    J --> N
    L --> O[Record recommendation and final decision]
    N --> O
    O --> P[Update ticket in source platform]
    P --> Q[Include event in authorised reporting]
    Q --> R([End])
```

## 3. Exception path: model or integration unavailable

```mermaid
flowchart TD
    A([Ticket received]) --> B{Routing feature available?}
    B -- Yes --> C[Continue to validation and recommendation]
    B -- No --> D[Leave ticket in existing workflow]
    D --> E[Notify or expose fallback status]
    E --> F[Agent handles ticket using current procedure]
    C --> G([Continue normal flow])
    F --> H([End])
```

## 4. Design notes

- The existing ticketing platform remains the source of truth for the ticket and final assignment.
- Manual handling is available when input is invalid, language is unsupported, confidence is low or the model service is unavailable.
- The agent's final values must not overwrite the original recommendation in the audit record.
- The decision threshold and fallback procedure require operational approval.
- The exact integration, retry and duplicate-event behaviour require technical design.
