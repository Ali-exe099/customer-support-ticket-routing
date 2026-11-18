# Validation and Measurement Plan

**Document version:** 1.0  
**Status:** Proposed evaluation plan; no model results claimed

## 1. Purpose

This plan defines how the first classification experiment should be assessed and what evidence would be needed before a controlled operational pilot. It does not report completed model performance.

## 2. Evaluation questions

1. How well can ticket text reproduce the existing ticket-type labels?
2. How well can ticket text reproduce the existing queue labels?
3. How well can ticket text reproduce the existing priority labels?
4. Which classes are frequently confused?
5. Can a confidence-based review policy isolate a subset of cases where the model is less reliable?
6. What additional operational data would be needed to assess the effect on the support workflow?

## 3. Experimental design

- Use the English subset for the first experiment.
- Use `subject` and `body` as the only baseline text inputs.
- Exclude `answer`, tag fields and target labels from the input features.
- Apply a reproducible train/validation/test split. Use stratification where label counts allow it.
- Fit vocabulary, vectorisation, feature selection and other learned preprocessing only on the training portion.
- Select model parameters using training/validation data. Keep the test set untouched until final evaluation.
- Record the split method, random seed, preprocessing version, model configuration and dataset version.
- Compare the model with a simple baseline, such as the most-frequent-class predictor, before interpreting a more complex result.

The exact algorithm should be selected after a baseline is established. Model complexity is not the objective; the goal is a reliable and understandable recommendation for the intended workflow.

## 4. Model evaluation measures

| Measure | Why it matters |
|---|---|
| Accuracy | Overall share of predictions that match the existing label; can be misleading with imbalanced classes |
| Per-class precision | Shows how often predictions for a particular class match the reference label |
| Per-class recall | Shows how many records from a reference class are identified |
| Macro F1 | Gives each class equal weight and highlights weak performance on smaller classes |
| Weighted F1 | Reflects class frequency while combining precision and recall |
| Confusion matrix | Shows which labels are confused with one another |
| Top-2 queue accuracy (optional) | Indicates whether the reference queue appears among two suggested queues, if the product design supports ranked alternatives |

Report queue, type and priority results separately. Do not combine them into one score because they represent different decisions.

## 5. Confidence and manual-review evaluation

A confidence threshold should not be selected by intuition alone. Use validation data to examine the relationship between confidence and actual agreement with the reference labels.

For a range of candidate thresholds, report:

- the share of tickets sent to manual review;
- the share retained for agent review as a model recommendation;
- error rate among retained recommendations;
- error rate by queue, type and priority;
- the effect on less common labels.

Where model probabilities are used, assess calibration before describing them as probabilities of correctness. A confidence score should be treated as a review signal until that assessment is complete.

## 6. Data limitations affecting interpretation

The evaluation measures agreement with labels in the public dataset. It does not establish whether the historical queue, type or priority was the best decision. Label quality and consistency would need to be reviewed with the taxonomy owner before using model performance as a product-readiness measure.

## 7. Operational pilot measures

A live pilot would require additional event-level data. Candidate measures include:

| Measure | Definition to agree before pilot | Additional data required |
|---|---|---|
| Initial assignment accuracy | Share of initial assignments accepted without correction, with agreed definition of correctness | Initial assignment, final assignment and review events |
| Reassignment rate | Share of tickets reassigned at least once within a defined period | Assignment history and timestamps |
| Time to first assignment | Time from ticket creation to first confirmed queue assignment | Ticket creation and assignment timestamps |
| Time to resolution | Time from ticket creation to resolved status | Creation and resolution timestamps |
| SLA attainment | Share of eligible tickets meeting the applicable SLA | SLA policy, eligibility and event timestamps |
| Manual-review rate | Share of tickets routed to manual review | Review status events |
| Override rate | Share of recommendations changed by an agent | Recommendation and final decision records |
| Agent feedback | Agent assessment of recommendation usefulness | Structured feedback or survey data |

No target value should be set until a baseline is measured and stakeholders agree the operating context.

## 8. Release / pilot decision

A pilot should not proceed solely because a model achieves a high overall accuracy. Review per-class performance, confidence behaviour, manual-review capacity, data protection controls, fallback behaviour and agent feedback. Operations and product owners should agree acceptable thresholds and stop conditions before the pilot starts.
