# GDP Analysis and Prediction System — ER Diagram

## Project Overview
This repository contains the Entity Relationship (ER) Diagram and supporting documentation for the **GDP Analysis and Prediction System**.

The ER model represents country information, dataset versioning, machine-learning model training, GDP prediction requests, prediction validation, analysis logging, and data-imputation auditing.

## Entities
- `COUNTRY_MASTER` — Master data for world countries.
- `DATA_SET_VERSION` — Source data versions (`world.csv` files).
- `TRAINED_MODEL_INSTANCE` — Model training parameters and evaluation metrics.
- `GDP_PREDICTION_REQUEST` — Core prediction request/action record.
- `DATA_ANALYSIS_LOG` — Audit of visualization and preprocessing actions.
- `PREDICTION_VALIDATION_STATUS` — Supporting records for prediction checks.
- `DATA_IMPUTATION_AUDIT` — Supporting records for tracing data-cleaning steps.

## Relationships
| Source | Related Entity | Cardinality | Purpose |
|---|---|---:|---|
| `COUNTRY_MASTER` | `GDP_PREDICTION_REQUEST` | 1:M | One country can be associated with multiple GDP prediction requests. |
| `DATA_SET_VERSION` | `TRAINED_MODEL_INSTANCE` | 1:M | One dataset version can be used to train multiple model instances. |
| `DATA_SET_VERSION` | `DATA_ANALYSIS_LOG` | 1:M | One dataset version can generate multiple analysis logs. |
| `TRAINED_MODEL_INSTANCE` | `GDP_PREDICTION_REQUEST` | 1:M | One trained model can process multiple prediction requests. |
| `GDP_PREDICTION_REQUEST` | `PREDICTION_VALIDATION_STATUS` | 1:M | A prediction request can have multiple validation records. |
| `DATA_ANALYSIS_LOG` | `DATA_IMPUTATION_AUDIT` | 1:M | One analysis log can contain multiple imputation audit records. |
| `DATA_SET_VERSION` | `DATA_IMPUTATION_AUDIT` | 1:M | One dataset version can have multiple preprocessing/imputation audit records. |

## Technology Context
The supplied project description identifies Streamlit, Scikit-learn, Pandas, Matplotlib/Seaborn, S3, and a relational database as the project technology/persistence context.

## Repository Contents
```text
GDP-Analysis-ER-Diagram-GitHub/
├── diagrams/
│   ├── ER_Diagram_Original.png
│   └── ER_Diagram_Presentation.png
├── docs/
│   ├── ER_Diagram_Documentation.md
│   └── Submission_Checklist.md
└── README.md
```

## Source Consistency Note
The two supplied diagrams contain a naming variation for the dataset foreign key in `TRAINED_MODEL_INSTANCE`: the first image uses `VersionID`, while the presentation version uses `TrainedOnVersionID`. Both supplied images are preserved unchanged. Select one naming convention before implementing the database schema/code.

## Author
**Venegalla Venkata Laxminath**

## Project Status
**In Progress**
