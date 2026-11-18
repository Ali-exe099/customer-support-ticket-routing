# Assumptions, Risks and Open Questions

**Document version:** 1.0  
**Status:** Working register

## 1. Assumptions

| ID | Assumption | Why it matters | Validation needed |
|---|---|---|---|
| A-01 | An existing ticketing platform can provide the ticket record to the feature. | Defines the integration boundary. | Confirm source system, event/API contract and ownership. |
| A-02 | Subject and body are available early enough to support initial classification. | These are the baseline model inputs. | Confirm actual field availability and data quality. |
| A-03 | The business maintains approved queue, type and priority taxonomies. | Predictions must use valid business values. | Obtain the current taxonomy and owners. |
| A-04 | Agents can review and change recommendations in the ticket workflow. | Human control is a core product requirement. | Validate agent workflow and permissions. |
| A-05 | The organisation can retain recommendation and final-decision events. | Enables audit and workflow measurement. | Confirm event store, access and retention policy. |

## 2. Risks

| ID | Risk | Potential impact | Proposed response |
|---|---|---|---|
| R-01 | Historical labels are inconsistent or do not match current policy. | Model learns patterns that should not be repeated. | Review label definitions and sample records with queue owners. |
| R-02 | Rare queues have too few examples. | Low recall or unstable performance for smaller teams. | Report per-class results; consider more data or a safe manual path. |
| R-03 | Missing or poor-quality ticket text reduces reliability. | Incorrect or unavailable recommendations. | Validate inputs and measure performance by input-quality segment. |
| R-04 | Confidence scores are not calibrated. | Agents may over-trust recommendations. | Assess calibration and avoid probability language until validated. |
| R-05 | Manual-review volume is too high. | The feature creates additional workload. | Measure review coverage on validation data and test pilot capacity. |
| R-06 | Agents override recommendations but reasons are not captured. | Limited evidence for improving the product. | Agree override reason policy and make recording straightforward. |
| R-07 | Ticket text contains personal or sensitive information. | Privacy or access-control breach. | Complete privacy review, minimise data and apply role-based access. |
| R-08 | Model or integration outage blocks ticket handling. | Tickets are delayed or missed. | Keep the existing workflow available as a fallback. |

## 3. Open questions

| ID | Question | Decision owner(s) |
|---|---|---|
| Q-01 | What is the authoritative source for queue names and ownership? | Product / Operations |
| Q-02 | What rules define low, medium and high priority? | Operations |
| Q-03 | Is the ticket-type taxonomy fixed, or can teams change it? | Product / Operations |
| Q-04 | What confidence threshold should trigger manual review? | Product / Operations / Data Science |
| Q-05 | Should the threshold differ by prediction type or queue? | Product / Data Science |
| Q-06 | Which fields may be sent to the model, retained and displayed? | Security / Privacy / Engineering |
| Q-07 | What is the source of truth for final assignment and audit history? | Platform owner / Engineering |
| Q-08 | What override reason codes are needed, and are they mandatory? | Operations / Product |
| Q-09 | Which service-level and performance targets apply to the feature? | Product / Engineering / Operations |
| Q-10 | What pilot size, duration and stop conditions are acceptable? | Product / Operations |

## 4. Decisions recorded for this portfolio version

- The feature is designed as decision support; an agent confirms the final outcome.
- The first data experiment uses English records only.
- The baseline input is limited to subject and body text.
- The answer and tag fields are excluded from the baseline model input.
- The current-state process is not claimed as verified; only the dataset fields are directly observed.
- No operational benefit is claimed from the public dataset.
