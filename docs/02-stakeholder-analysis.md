# Stakeholder Analysis

**Document:** Stakeholder analysis  
**Version:** 1.0  
**Status:** Initial view; validate with the organisation

The list below reflects the roles likely to be involved in a ticket-routing feature. It is a proposed stakeholder map, not a record of interviews or confirmed organisational ownership.

## 1. Stakeholder register

| Stakeholder | Interest in the feature | Main needs / concerns | Suggested involvement |
|---|---|---|---|
| Customer | Indirect user | Ticket reaches the right team without unnecessary delay; no loss of context | Validate customer-impact scenarios and communication boundaries |
| Support agent | Primary user | Clear recommendation, quick review, ability to override, no loss of control | Workflow walkthroughs, usability feedback and pilot testing |
| Team lead | Operational owner | Correct queue allocation, visibility of exceptions and override patterns | Confirm queue definitions and review process |
| Operations manager | Business owner / sponsor | Consistent handling, measurable outcomes and manageable operational risk | Agree objectives, pilot measures and go/no-go criteria |
| Product manager | Product decision-maker | Clear problem, prioritised scope and evidence for product decisions | Own product scope, priorities and release decisions |
| Business analyst | Requirements lead | Shared understanding, documented decisions and traceability | Facilitate discovery, maintain requirements and manage changes |
| Data scientist / ML engineer | Model implementation | Defined labels, usable training data, evaluation criteria and model monitoring | Assess feasibility, build and validate models |
| Backend / platform engineer | Integration owner | Stable input contract, access control, availability and audit events | Define API/event integration and system behaviour |
| Quality engineer | Test owner | Testable requirements, expected results and exception scenarios | Create and execute functional and integration tests |
| Security / privacy team | Control function | Appropriate use of ticket text, access restrictions, retention and auditability | Review data handling and control requirements |

## 2. Influence and interest

| Group | Stakeholders | Engagement approach |
|---|---|---|
| High influence / high interest | Operations manager, product manager, team lead | Involve in scope, policy decisions, prioritisation and pilot reviews |
| High influence / specialist interest | Security / privacy, engineering leads | Consult on architecture, data handling and operational controls |
| High interest / day-to-day impact | Support agents, quality engineers | Include in workflow design, usability sessions and acceptance testing |
| Delivery specialists | Data scientist / ML engineer, backend engineer | Work through requirements refinement, design reviews and technical testing |
| Indirectly affected | Customers | Validate that the proposed flow does not degrade customer experience |

## 3. Decisions that need stakeholder input

1. Which ticket queues are in scope, and who owns the official queue taxonomy?
2. What business definitions distinguish low, medium and high priority?
3. What confidence threshold should trigger manual review? The threshold should be selected using validation evidence and operational capacity, not guessed in advance.
4. Should an agent be required to enter a reason when overriding a recommendation?
5. What ticket information may be processed, stored and shown to each user role?
6. Which system is the source of truth for final queue assignment and audit history?
7. What pilot size and operational measures are needed before any rollout decision?

## 4. Engagement plan

| Activity | Participants | Output |
|---|---|---|
| Discovery workshop | Product, operations, team leads, agents, BA | Confirmed problem statement, current process and scope |
| Queue and priority review | Team leads, operations, product | Approved taxonomy and priority definitions |
| Requirements review | Product, operations, engineering, QA, BA | Reviewed BRD, FRD and acceptance criteria |
| Data feasibility review | Data science, product, operations, privacy | Data suitability, exclusions and evaluation plan |
| Prototype walkthrough | Agents, team leads, QA, product | Usability feedback and workflow changes |
| Pilot review | Product, operations, quality, data science | Pilot findings and recommendation on next steps |

No interviews or workshops are claimed to have taken place as part of this portfolio exercise.
