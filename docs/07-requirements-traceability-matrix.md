# Requirements Traceability Matrix (RTM)

**Document version:** 1.0  
**Status:** Initial mapping; update as requirements change

The matrix links the business requirements to functional requirements, user stories and proposed validation cases. Test cases are identifiers for planned testing, not evidence that testing has already been completed.

| Business requirement | Functional requirement(s) | User story | Test case(s) |
|---|---|---|---|
| BR-01 — Recommend support queue | FR-04 | US-04 | TC-04, TC-08 |
| BR-02 — Identify ticket type | FR-03 | US-03 | TC-03 |
| BR-03 — Recommend priority | FR-05 | US-05 | TC-05, TC-08 |
| BR-04 — Identify uncertainty and require manual review | FR-06, FR-08 | US-06, US-07 | TC-06, TC-07 |
| BR-05 — Allow agent review | FR-08, FR-09 | US-07, US-08 | TC-07, TC-08 |
| BR-06 — Allow agent override | FR-09 | US-08 | TC-08 |
| BR-07 — Record recommendation and final decision | FR-10 | US-09 | TC-09 |
| BR-08 — Report performance | FR-11 | US-10 | TC-10 |
| BR-09 — Explain recommendations | FR-07 | US-06 | TC-06 |
| BR-10 — Validate ticket input and scope | FR-01, FR-02 | US-01, US-02 | TC-01, TC-02 |

## Planned test-case index

| Test case | Purpose | Main expected result |
|---|---|---|
| TC-01 | Receive a valid ticket | Ticket is accepted and traceable to its source identifier |
| TC-02 | Validate missing text and unsupported language | Ticket is flagged; normal classification is not attempted |
| TC-03 | Return ticket type | One approved ticket type or a controlled no-result state is returned |
| TC-04 | Return support queue | One approved queue or a controlled no-result state is returned |
| TC-05 | Return priority | One approved priority value is returned under the agreed policy |
| TC-06 | Display confidence and rationale | Confidence and explanation are displayed without overstating certainty |
| TC-07 | Route low-confidence case to review | Case is marked for manual review |
| TC-08 | Confirm and override | Final values are saved separately from model recommendations |
| TC-09 | Inspect audit history | Recommendation, final decision and relevant metadata are available to authorised users |
| TC-10 | Review dashboard measures | Available metrics show definitions and population; unavailable measures are clearly identified |

## Coverage notes

- FR-01 through FR-11 are represented in the matrix.
- Each business requirement has at least one linked functional requirement and user story.
- System performance, security, privacy and availability requirements are covered by NFRs in the FRD and need separate technical test cases during solution design.
- Test execution status is not recorded here because the proposed product has not been built.
