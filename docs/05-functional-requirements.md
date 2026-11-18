# Functional Requirements Document (FRD)

**Project:** Customer Support Ticket Routing  
**Document version:** 1.0  
**Status:** Proposed; subject to product and technical review

## 1. Purpose

This document describes the expected behaviour of the proposed routing feature. It translates the business requirements into functions that can be designed and tested.

## 2. Actors and systems

- **Ticketing platform:** source of the ticket record and final assignment.
- **Routing feature:** validates input and generates recommendations.
- **Support agent:** reviews and confirms or changes the recommendation.
- **Team lead / operations user:** reviews workflow and performance information.
- **Authorised administrator:** maintains approved categories, queues and thresholds through an agreed configuration process.

## 3. Input and output

### Input fields for the first version

| Field | Required? | Use |
|---|---|---|
| Ticket ID | Yes | Identifies the ticket and links the decision record |
| Subject | No, when body has usable text | One part of the text supplied to the classifier |
| Body / description | At least one usable text field is required | Main ticket description supplied to the classifier |
| Language | Derived or supplied | Confirms whether the ticket is in a supported language |
| Created timestamp | Required for event tracking | Records when the ticket entered the workflow |

The exact input contract must be agreed with the ticketing-platform owner. The dataset used for the portfolio contains subject, body and language, but not a ticket ID or created timestamp suitable for this proposed integration.

### Recommendation output

| Field | Description |
|---|---|
| Recommended ticket type | One value from the approved type list |
| Recommended queue | One value from the approved queue list |
| Recommended priority | One value from the approved priority list |
| Confidence | Model confidence or calibrated confidence measure, with documented interpretation |
| Recommendation reason | Short, readable explanation of the main evidence or factors behind the recommendation |
| Review status | Indicates whether the recommendation can be reviewed normally or requires manual review |

## 4. Functional requirements

### FR-01 — Receive a ticket

The feature shall receive an eligible ticket record from the existing ticketing platform. It shall retain the source ticket identifier so that recommendations and decisions can be associated with the original ticket.

**Expected result:** a valid ticket record is accepted and can be traced to its source. Invalid or repeated requests are handled according to the agreed integration contract.

### FR-02 — Validate text and language

The feature shall check that at least one usable text field is present and identify whether the ticket is in a supported language. For the first data experiment, only English records are in scope.

**Expected result:** tickets with no usable text or an unsupported language are not classified as normal cases; they are flagged for the agreed manual path.

### FR-03 — Recommend ticket type

The feature shall use the available ticket subject and body to recommend one approved ticket type.

**Expected result:** the result contains a ticket type from the approved list, or a clear status that no recommendation is available.

### FR-04 — Recommend support queue

The feature shall use the available ticket subject and body to recommend one approved support queue.

**Expected result:** the result contains a queue from the approved list, or a clear status that no recommendation is available.

### FR-05 — Recommend priority

The feature shall recommend a priority using the approved priority categories and the business-defined priority policy.

**Expected result:** the result contains a valid priority and does not create new priority values. The model's learned pattern must not replace the organisation's priority policy without approval.

### FR-06 — Calculate confidence

The feature shall provide a confidence indication for each recommendation, or a documented overall confidence measure if separate scores are not supported by the selected model.

**Expected result:** the score is available to the review workflow and its meaning is documented. A raw model probability must not be presented as a calibrated likelihood unless calibration has been evaluated.

### FR-07 — Explain the recommendation

The feature shall display a concise reason that helps the agent understand the recommendation. The reason must not imply certainty or expose restricted model details.

**Expected result:** the agent can see a short explanation alongside the predicted type, queue and priority. The explanation approach must be reviewed for usefulness and accuracy.

### FR-08 — Send uncertain cases to manual review

The feature shall flag cases that fall below the approved confidence threshold, fail input validation or fall outside supported scope.

**Expected result:** the ticket is clearly marked for manual review and is not silently treated as a high-confidence recommendation.

### FR-09 — Allow agent confirmation or override

The support agent shall be able to accept the recommendation or select different values for ticket type, queue or priority.

**Expected result:** the final values are recorded as the agent-confirmed values. If an override reason is required by business policy, the system prompts for it.

### FR-10 — Record recommendation and final decision

The feature shall record the recommendation, confidence, review status, final agent decision, actor and relevant timestamps. The record shall distinguish the model's suggestion from the agent's final decision.

**Expected result:** an authorised reviewer can reconstruct what was recommended and what was finally selected, subject to access and retention policies.

### FR-11 — Report performance and workflow measures

The feature shall provide authorised users with reporting on classification performance and workflow activity. Measures may include queue/type/priority precision and recall, manual-review volume, override rate and distribution of recommendations.

**Expected result:** the report identifies the data period, population and metric definitions. Model metrics and operational workflow metrics are shown separately.

## 5. Non-functional requirements

| ID | Requirement | Verification approach |
|---|---|---|
| NFR-01 Performance | Response-time target shall be agreed with product and engineering based on the ticketing workflow and expected load. | Load and response-time testing against an approved target |
| NFR-02 Availability | The feature shall fail safely when unavailable; tickets must remain accessible through the existing support workflow. | Failure and recovery testing |
| NFR-03 Access control | Only authorised roles may view recommendations, change configuration or access audit records. | Role-based access tests |
| NFR-04 Privacy | Ticket text and decision records shall be handled according to the organisation's data protection and retention policies. | Privacy/security review |
| NFR-05 Auditability | Recommendation and final decision events shall be recorded with enough detail for authorised review. | Audit-record inspection |
| NFR-06 Explainability | Recommendation reasons shall be understandable to the intended users and shall not overstate certainty. | Agent usability review |
| NFR-07 Usability | The review experience shall make the recommendation, confidence and manual-review status easy to distinguish. | Usability testing with representative agents |
| NFR-08 Maintainability | Queue, type and priority taxonomies shall be managed through a controlled update process. | Configuration and change-control review |
| NFR-09 Robustness | Missing, malformed or unsupported inputs shall produce a controlled outcome rather than an unhandled failure. | Negative and boundary testing |

No numeric response-time, availability or model-performance target is set in this document. Those values require stakeholder agreement and evidence from the intended environment.

## 6. Error and exception handling

| Scenario | Expected behaviour |
|---|---|
| Both subject and body are blank or unusable | Do not generate a normal recommendation; flag for manual handling |
| Subject is missing but body is usable | Continue using the available body text |
| Body is missing but subject is usable | Continue only if the agreed minimum text rule is met |
| Unsupported language | Mark as unsupported and use the manual path |
| Model service unavailable | Do not block the existing ticket workflow; use the fallback process |
| No valid category or queue returned | Do not invent a new label; send to manual review |
| Low confidence | Require agent review before final decision |
| Agent overrides recommendation | Store recommendation and final values separately |

## 7. Open design decisions

- Whether confidence is displayed per output or as one overall score.
- How recommendation rationale will be generated and validated.
- What thresholds trigger manual review for each output.
- Whether overrides require a reason code, free text or both.
- Which platform owns the audit record and final assignment.
- The retention period and access policy for ticket text and model records.
