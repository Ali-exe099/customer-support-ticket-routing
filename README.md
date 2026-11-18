# Customer Support Ticket Routing — Product BA Case Study

**Project type:** Product Business Analysis / AI-assisted workflow design  
**Version:** 1.0  
**Status:** Requirements and process-design case study  
**Data source:** Public multilingual customer-support ticket dataset (English records used for the proposed baseline)

## Project summary

Support teams receive tickets that need to be understood, prioritised and sent to the right queue. This case study examines how an AI-assisted routing feature could help with that first decision without removing the support agent from the process.

The proposed feature reads the ticket subject and description, then recommends a ticket type, support queue and priority. It also provides a confidence indication and a short reason for the recommendation. Low-confidence cases are sent for manual review. The agent can accept or change the recommendation, and the system records both the recommendation and the final decision.

This is a product requirements and workflow-design exercise based on a public dataset. It is not a live customer-support deployment, and the dataset does not contain the operational history needed to prove that automated recommendations reduce handling time, reassignment or SLA breaches.

## Business question

**Can an AI-assisted decision-support feature make initial ticket classification and queue selection more consistent, while keeping agents in control of the final assignment?**

The project will test whether ticket text can reproduce the labels already present in the dataset. That is a useful first check, but it is not the same as proving that the labels represent the best possible routing decision.

## Proposed product behaviour

1. The existing support platform makes a new ticket available to the routing feature.
2. The feature validates the subject and description and checks whether the language is supported.
3. It recommends a ticket type, support queue and priority.
4. It displays a confidence score and a brief explanation for each recommendation.
5. Low-confidence or unsupported cases are placed in a manual-review path.
6. A support agent confirms the recommendation or selects a different outcome.
7. The system records the recommendation, the agent's final decision and any override reason.
8. Product and operations users review model and workflow performance using agreed measures.

## Repository contents

| File | What it covers |
|---|---|
| [Project overview](docs/01-project-overview.md) | Context, objectives, scope and boundaries |
| [Stakeholder analysis](docs/02-stakeholder-analysis.md) | Stakeholder needs, influence and involvement |
| [Process analysis](docs/03-process-analysis.md) | Dataset-level current-state view and proposed future flow |
| [Business requirements (BRD)](docs/04-business-requirements.md) | Business needs, objectives and requirements |
| [Functional requirements (FRD)](docs/05-functional-requirements.md) | Product behaviour and non-functional requirements |
| [User stories and acceptance criteria](docs/06-user-stories-acceptance-criteria.md) | Backlog-ready stories and testable outcomes |
| [Requirements traceability matrix](docs/07-requirements-traceability-matrix.md) | Requirement-to-story-to-test mapping |
| [Workflow diagrams](docs/08-workflow-diagrams.md) | Mermaid diagrams for the proposed process |
| [Data profile and usage](docs/09-data-profile-and-usage.md) | Dataset structure, profile and limitations |
| [Validation plan](docs/10-validation-plan.md) | Evaluation approach and measures |
| [Assumptions, risks and open questions](docs/11-assumptions-risks-open-questions.md) | Items that need confirmation before delivery |

## Data used

The selected source file is `dataset-tickets-multi-lang-4-20k.csv`, a 20,000-row public dataset. The project uses the 11,923 records labelled English for the first analysis. The English subset contains 10 queue labels, 3 priority labels and 4 ticket-type labels.

The initial model input is limited to `subject` and `body`. The `answer` field and `tag_1` through `tag_8` are excluded from the baseline because they may not be available when a new ticket first arrives and could leak information that would not exist at prediction time.

See [Data profile and usage](docs/09-data-profile-and-usage.md) for the observed counts and limitations.

## Important interpretation limits

- The queue, priority and type values are existing dataset labels. They are treated as reference labels for an initial classification exercise, not as independently verified correct decisions.
- The data does not include assignment history, reassignment events, agent overrides, resolution timestamps or SLA outcomes.
- No reduction in reassignment, handling time or SLA breaches is claimed.
- The current-state workflow is not documented by the dataset. The process analysis therefore separates the fields observed in the data from assumptions that would need stakeholder validation.
- The proposed feature is decision support. The support agent retains final control.

## Suggested review order

Start with this README, then review the BRD and FRD. The process diagrams and user stories show how the requirements translate into a working flow. The data and validation documents explain what can be tested from the available public data and where further operational evidence would be required.

## Source

Bueck, Tobias. *Multilingual Customer Support Tickets*. Kaggle.  
https://www.kaggle.com/datasets/tobiasbueck/multilingual-customer-support-tickets

Check the dataset's current licence and attribution terms before redistributing any raw records. This repository is intended to hold the project documentation; do not commit the dataset itself unless its licence permits it.
