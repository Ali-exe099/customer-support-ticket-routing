# Business Requirements Document (BRD)

**Project:** Customer Support Ticket Routing  
**Document version:** 1.0  
**Status:** Proposed requirements for stakeholder review  
**Prepared:** 18 November 2026

## 1. Purpose

This document describes the business need and the outcomes expected from an AI-assisted ticket-routing feature. It is intended to give product, operations and delivery teams a shared starting point for solution design.

## 2. Problem statement

Incoming support tickets need an initial ticket type, queue and priority. The quality and consistency of these decisions matter to the support workflow. This case study explores whether a model can provide useful recommendations from ticket text and make uncertainty visible to the agent.

The available public dataset does not establish the size of any existing routing problem. The business case and expected operational benefits must therefore be validated with operational data before implementation.

## 3. Business objective

Provide support agents with a consistent, explainable recommendation for ticket classification and routing, while retaining human control over the final decision.

## 4. Scope

**Included:** ticket intake from an existing platform; text validation; ticket type, queue and priority recommendations; confidence and rationale; manual review; agent confirmation or override; audit recording; performance reporting.

**Excluded:** replacement of the ticketing platform; automatic customer replies; autonomous final assignment; production integration; non-English model support in the first data experiment; claims of operational improvement without pilot evidence.

## 5. Business requirements

| ID | Requirement | Priority | Business rationale |
|---|---|---|---|
| BR-01 | The feature shall recommend a support queue for each eligible ticket. | Must | Helps the agent identify the team most likely to handle the issue. |
| BR-02 | The feature shall identify a likely ticket type. | Must | Gives the agent a consistent starting classification. |
| BR-03 | The feature shall recommend a priority using the agreed priority categories and policy. | Must | Supports consistent review of ticket urgency. |
| BR-04 | The feature shall identify uncertain recommendations and send them for manual review. | Must | Prevents weak recommendations from being treated as reliable decisions. |
| BR-05 | A support agent shall be able to review the recommendation before the final decision is recorded. | Must | Keeps the decision under human control. |
| BR-06 | A support agent shall be able to override any recommendation. | Must | Allows the agent to use context that may not be present in the ticket text. |
| BR-07 | The feature shall retain a record of the recommendation and the final decision. | Must | Supports audit, review and future improvement. |
| BR-08 | Authorised users shall be able to review classification and workflow performance. | Should | Makes performance and exceptions visible after launch. |
| BR-09 | The feature shall provide a readable reason for each recommendation. | Should | Helps an agent assess whether the recommendation is relevant. |
| BR-10 | The feature shall validate ticket input and identify unsupported or unusable records before classification. | Must | Avoids generating recommendations from invalid or out-of-scope inputs. |

Priorities are proposed for initial discussion. Product and operations stakeholders should confirm them during requirements review.

## 6. Business rules

| ID | Rule |
|---|---|
| RULE-01 | Only queue, ticket-type and priority values approved by the business may be returned. |
| RULE-02 | The feature must not treat a missing or unusable ticket description as a normal classification case. |
| RULE-03 | Tickets in an unsupported language must be clearly identified and sent to an agreed non-model path. |
| RULE-04 | Recommendations below the approved confidence threshold must be routed for manual review. |
| RULE-05 | The support agent's confirmed values are the final values for the workflow. |
| RULE-06 | A recommendation and the final decision must be stored separately. |
| RULE-07 | The system must not send customer-facing responses as part of this feature. |

## 7. Assumptions

- An existing platform can provide the ticket subject and description to the feature.
- The organisation has an approved queue taxonomy and priority policy.
- Support agents have access to the ticket and the recommendation when they review it.
- The feature can store recommendation and decision events in an approved system.
- English is the first language considered for the data experiment; production language coverage will be a separate decision.

## 8. Constraints

- The portfolio exercise uses a public static dataset rather than live operational records.
- Dataset labels are not independently verified ground truth.
- The dataset does not include reassignment, resolution or SLA events.
- No operational impact target can be justified from the selected data alone.

## 9. Risks

- Historical labels may not match current business rules.
- Less common queues may have too few records for reliable model evaluation.
- Missing or unclear ticket text may affect recommendation quality.
- Excessive manual review may reduce the value of the feature.
- Sensitive ticket information would require privacy and access controls in a real deployment.

## 10. Acceptance at business level

The proposed solution is ready for detailed design when stakeholders have confirmed the queue taxonomy, priority definitions, human-review policy, audit requirements, data handling rules and pilot measures. The data experiment should separately demonstrate its classification performance and limitations.
