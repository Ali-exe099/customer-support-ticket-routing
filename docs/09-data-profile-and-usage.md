# Data Profile and Usage Notes

**Document version:** 1.0  
**Source file reviewed:** `dataset-tickets-multi-lang-4-20k.csv`  
**Profile date:** 18 November 2026

## 1. Source

The project uses the public Kaggle dataset *Multilingual Customer Support Tickets* by Tobias Bueck:

https://www.kaggle.com/datasets/tobiasbueck/multilingual-customer-support-tickets

The selected CSV contains 20,000 rows and 15 columns. The first analysis uses the 11,923 rows where `language` is `en`.

## 2. Fields available

| Field | Description based on the file | Planned use |
|---|---|---|
| `subject` | Ticket subject text | Model input |
| `body` | Ticket description text | Model input |
| `answer` | Response text associated with the ticket | Excluded from the baseline input |
| `type` | Existing ticket-type label | Prediction target for type experiment |
| `queue` | Existing queue label | Prediction target for queue experiment |
| `priority` | Existing priority label | Prediction target for priority experiment |
| `language` | Language label | Filter English records for the first experiment |
| `tag_1`–`tag_8` | Additional tag fields | Excluded from the baseline input |

The precise business definition and creation process for each label should be confirmed from the dataset documentation and, for any real product, with the organisation that owns the taxonomy.

## 3. English subset profile

| Check | Result |
|---|---:|
| Total records in selected CSV | 20,000 |
| English records | 11,923 |
| German records | 8,077 |
| Missing subject in English subset | 1,032 (8.66%) |
| Missing body in English subset | 1 (0.01%) |
| Missing answer in English subset | 3 |
| Missing queue / priority / type | 0 for each field |
| Exact duplicate rows in English subset | 0 |
| Duplicate subject + body pairs in English subset | 0 |

There are no English records where both subject and body are missing. A missing subject does not automatically make a ticket unusable because the body may contain the description. The single missing body record may still have a usable subject, subject to the agreed input rule.

## 4. Existing label distribution

### Queue

| Queue label | Records | Share of English subset |
|---|---:|---:|
| Technical Support | 3,412 | 28.6% |
| Product Support | 2,232 | 18.7% |
| Customer Service | 1,859 | 15.6% |
| IT Support | 1,391 | 11.7% |
| Billing and Payments | 1,302 | 10.9% |
| Returns and Exchanges | 582 | 4.9% |
| Service Outages and Maintenance | 442 | 3.7% |
| Sales and Pre-Sales | 330 | 2.8% |
| Human Resources | 205 | 1.7% |
| General Inquiry | 168 | 1.4% |

### Priority

| Priority label | Records | Share of English subset |
|---|---:|---:|
| medium | 4,952 | 41.5% |
| high | 4,571 | 38.3% |
| low | 2,400 | 20.1% |

### Ticket type

| Type label | Records | Share of English subset |
|---|---:|---:|
| Incident | 4,642 | 38.9% |
| Request | 3,498 | 29.3% |
| Problem | 2,498 | 21.0% |
| Change | 1,285 | 10.8% |

The queue labels are imbalanced. General Inquiry and Human Resources have comparatively few examples, so an overall accuracy score could hide weak performance on these queues. Per-class precision and recall should be reviewed.

## 5. Baseline input decision

Use `subject` and `body` as the initial text input. Exclude the following from the first baseline:

- `answer`: a response may be written after the ticket has already been classified or handled. Using it could introduce information that would not be present at intake.
- `tag_1` to `tag_8`: the data does not establish that these tags are available at the point when a new ticket first arrives. Including them would make the evaluation less representative of the proposed use case.
- `queue`, `priority` and `type`: these are target labels for the corresponding prediction tasks, not input features.

The `language` field is used to select English records for this first experiment. It is not needed as a predictive feature when the analysis has already been filtered to English.

## 6. Data quality and preparation considerations

- Keep records where at least one of subject or body contains usable text; document the resulting row count after applying the rule.
- Combine subject and body in a consistent way, while retaining the ability to trace predictions back to the source row.
- Normalise text carefully. Do not remove terms, punctuation or identifiers without checking whether they carry routing information.
- Split data into training, validation and test sets before fitting text transformations or selecting model parameters.
- Use stratification where feasible so that rare labels are represented in each split. Inspect the resulting class counts.
- Keep all versions of preprocessing and model configuration with the evaluation results.

## 7. What this dataset cannot answer

The file has no assignment-change history, event timestamps for routing decisions, agent identity, override records, resolution timestamps, SLA targets or SLA outcomes. It cannot support a measured reassignment rate, handling-time reduction, first-response improvement, resolution-time improvement or SLA impact.

The model can be evaluated for its agreement with the existing `queue`, `priority` and `type` labels. This is not proof that those labels are always correct or optimal.

## 8. Redistribution note

Public availability does not automatically grant permission to redistribute the raw CSV. Review the dataset's current licence and terms before committing any data or derived extracts. Keep this documentation in the repository and add a source link rather than uploading the full dataset unless redistribution is explicitly permitted.
