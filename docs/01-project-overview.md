# Project Overview

**Document:** Project overview  
**Version:** 1.0  
**Status:** Proposed solution for portfolio case study

## 1. Background

A support ticket usually needs an initial classification before it reaches the team that can handle it. The person or system making that decision has to interpret the ticket text, understand the issue and select a queue and priority. A weak first assignment can create extra work, but the size of that problem has not been measured in the dataset used for this case study.

This project explores a decision-support feature that can make a recommendation from the ticket's subject and description. It is designed to assist the support agent, not replace the agent's judgement.

## 2. Business question

Can ticket text be used to recommend a ticket type, support queue and priority, while identifying uncertain cases for human review?

## 3. Objectives

- Define the business need and boundaries for an AI-assisted ticket-routing feature.
- Document the expected workflow from ticket receipt through agent confirmation.
- Translate the business need into traceable functional and non-functional requirements.
- Define a safe manual-review path for uncertain or unsupported cases.
- Establish a validation approach using only fields available at ticket intake.
- Identify which operational outcomes cannot be measured with the selected public dataset.

## 4. Proposed users

The primary users are support agents who review incoming tickets. Team leads and operations managers need visibility into recommendation quality and workflow exceptions. Product, engineering, data science, quality and security teams would be involved in defining, building and governing the feature.

## 5. Scope

### In scope

- Receiving a ticket record from an existing support channel or ticketing platform.
- Validating the subject, description and supported language.
- Recommending ticket type, support queue and priority.
- Displaying confidence and a short recommendation rationale.
- Sending uncertain cases to manual review.
- Allowing an agent to accept or override a recommendation.
- Recording the recommendation and final agent decision.
- Reporting classification and workflow measures.

### Out of scope for this case study

- Replacing the organisation's ticketing platform.
- Automatically sending customer responses.
- Making the final assignment without an agent decision.
- Defining production priority policy or queue ownership rules without stakeholder input.
- Measuring live SLA performance, resolution time or reassignment reduction.
- Supporting languages other than English in the first data experiment.
- Claiming a production-ready model or production integration.

## 6. Product boundary

The proposed feature starts when an existing platform makes a new ticket available to it. The customer-facing submission form and the underlying ticket-management platform are outside this feature's boundary. The exact integration method would be agreed during solution design.

## 7. Expected outputs

The feature should return a recommended ticket type, queue and priority, along with confidence and a readable explanation. It should also make it clear when a recommendation should not be relied on without manual review.

## 8. How success will be assessed

The first phase will assess agreement with the historical labels in the public dataset. Measures include per-class precision and recall, macro and weighted F1, confusion matrices and confidence-based review coverage. These measures assess classification performance against the available labels; they do not establish operational benefit.

Operational measures such as reassignment rate, time to first assignment, time to resolution and SLA attainment would require a pilot with ticket-event and outcome data. Baselines and targets should be agreed with the operations team before a live trial.

## 9. Key constraints

The public dataset is a static collection of labelled tickets. It does not include the sequence of events that led to a queue assignment or the final operational outcome. Its labels may be useful for model experimentation, but their meaning and quality should be confirmed before they are used in a live product.
