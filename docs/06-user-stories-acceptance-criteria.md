# User Stories and Acceptance Criteria

**Document version:** 1.0  
**Status:** Proposed backlog for refinement

The stories below describe the user-facing behaviour expected from the first version. Acceptance criteria are written as observable outcomes so that product, engineering and QA can review them together.

## US-01 — Receive a ticket for assessment

**As the routing feature,** I want to receive a ticket from the existing ticketing platform, **so that** an eligible ticket can be assessed without asking the customer to submit it again.

**Acceptance criteria**

- **Given** the platform sends a ticket with a valid identifier, **when** the feature receives it, **then** the feature stores the identifier and acknowledges the request according to the agreed integration contract.
- **Given** the same request is delivered more than once, **when** the feature processes the repeat delivery, **then** it does not create duplicate decision records.
- **Given** a request does not contain the required identifier, **when** it is received, **then** the feature returns or records a controlled validation error.

## US-02 — Validate ticket text and language

**As a support agent,** I want unusable or unsupported tickets to be identified, **so that** I do not rely on a recommendation generated from unsuitable input.

**Acceptance criteria**

- **Given** a ticket has usable subject or body text in a supported language, **when** validation completes, **then** the ticket can proceed to classification.
- **Given** both text fields are blank or unusable, **when** validation completes, **then** the ticket is marked for manual handling.
- **Given** the language is outside the supported scope, **when** validation completes, **then** the ticket is marked unsupported and is not passed through the normal recommendation path.

## US-03 — View a ticket-type recommendation

**As a support agent,** I want to see a suggested ticket type, **so that** I have a consistent starting point when reviewing a new ticket.

**Acceptance criteria**

- **Given** a ticket passes validation, **when** classification completes, **then** the feature displays one value from the approved ticket-type list.
- **Given** the feature cannot produce a valid type, **when** the result is prepared, **then** it indicates that no recommendation is available and flags the ticket for review.

## US-04 — View a queue recommendation

**As a support agent,** I want to see a suggested support queue, **so that** I can assess where the ticket should be handled.

**Acceptance criteria**

- **Given** a ticket passes validation, **when** queue classification completes, **then** the feature displays one value from the approved queue list.
- **Given** no valid queue can be returned, **when** the result is prepared, **then** the feature does not create a new queue label and flags the ticket for review.

## US-05 — View a priority recommendation

**As a support agent,** I want to see a suggested priority, **so that** I can review the ticket using the organisation's priority policy.

**Acceptance criteria**

- **Given** a ticket passes validation, **when** priority assessment completes, **then** the feature displays one approved priority value.
- **Given** the priority policy has not been configured, **when** the feature is used, **then** it does not present an unapproved priority as a final business decision.

## US-06 — Understand confidence and recommendation reason

**As a support agent,** I want to see how confident the feature is and why it made the recommendation, **so that** I can judge whether further review is needed.

**Acceptance criteria**

- **Given** a recommendation is available, **when** it is displayed, **then** the confidence indication appears alongside the recommendation.
- **Given** a recommendation is displayed, **when** the agent reviews it, **then** a concise reason is available.
- **Given** confidence is not calibrated, **when** the score is displayed, **then** the interface does not describe it as a verified probability of correctness.

## US-07 — Review an uncertain ticket

**As a support agent,** I want low-confidence and out-of-scope tickets to be clearly flagged, **so that** I can make the decision manually.

**Acceptance criteria**

- **Given** the score is below the approved threshold, **when** the recommendation is displayed, **then** the ticket is marked for manual review.
- **Given** input validation fails or the language is unsupported, **when** the ticket is processed, **then** the ticket follows the manual path.
- **Given** a ticket is marked for manual review, **when** the agent opens it, **then** the review status is visible and the recommendation is not presented as ready for automatic use.

## US-08 — Confirm or override a recommendation

**As a support agent,** I want to accept or change the suggested values, **so that** the final decision reflects the ticket and the business context.

**Acceptance criteria**

- **Given** a recommendation is displayed, **when** the agent accepts it, **then** the accepted values are recorded as the final decision.
- **Given** the agent changes the queue, type or priority, **when** the agent saves the decision, **then** the changed values are recorded as the final decision and the original recommendation remains unchanged.
- **Given** an override reason is required by policy, **when** the agent submits an override, **then** the feature requires a reason before the decision is saved.

## US-09 — Retain an audit record

**As a team lead,** I want to review what the feature recommended and what the agent selected, **so that** routing decisions can be checked later.

**Acceptance criteria**

- **Given** a recommendation is generated, **when** the event is stored, **then** the record includes the recommendation, confidence, model/version reference and timestamp where available.
- **Given** an agent confirms or overrides the result, **when** the decision is saved, **then** the final values, actor and decision timestamp are recorded.
- **Given** an authorised reviewer opens the audit record, **when** it is displayed, **then** the recommendation and final decision can be distinguished.

## US-10 — Review performance information

**As an operations manager,** I want to review model and workflow measures, **so that** I can decide whether the feature is suitable for a controlled pilot or further improvement.

**Acceptance criteria**

- **Given** a reporting period and eligible evaluation data are available, **when** the report is generated, **then** classification measures are shown with their population and date range.
- **Given** workflow event data is available, **when** the report is generated, **then** manual-review and override measures are shown separately from model classification measures.
- **Given** a measure cannot be calculated from the available data, **when** the report is viewed, **then** it is labelled unavailable rather than estimated without evidence.
