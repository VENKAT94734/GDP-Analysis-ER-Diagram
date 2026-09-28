# ER Diagram Documentation

## Purpose
The ER diagram provides the database-level structure for a GDP Analysis and Prediction System. It organizes information required for dataset management, model training, GDP prediction, validation, analysis auditing, and data-imputation tracking.

## Entity Details

### COUNTRY_MASTER
**Attributes shown:** `CountryID` (PK), `CountryName`, `Region`, `ClimateType`, `Population`, `Area (sq. mi.)`, `PopDensity`.

### DATA_SET_VERSION
**Attributes shown:** `VersionID` (PK), `FileName`, `FileSourceURL`, `DateUploaded`, `ImputedFeaturesList`.

### TRAINED_MODEL_INSTANCE
**Attributes shown:** `ModelInstanceID` (PK), dataset-version foreign key, `ModelType`, `TrainingParamsJSON`, `RSquareScore`, `RMSE`.

### GDP_PREDICTION_REQUEST
**Attributes shown:** `PredictionID` (PK), `ModelInstanceID` (FK), optional `CountryID` (FK), `InputFeaturesJSON`, `PredictedGDPValue`, `RequestTimestamp`.

### DATA_ANALYSIS_LOG
**Attributes shown:** `LogID` (PK), optional `VersionID` (FK), `ActionType`, `ParametersJSON`, `Timestamp`.

### PREDICTION_VALIDATION_STATUS
**Attributes shown:** `ValidationID` (PK), optional `PredictionID` (FK), optional `ModelInstanceID` (FK), `Status`, `Notes`, `ValidatedSourceURL`.

### DATA_IMPUTATION_AUDIT
**Attributes shown:** `ImputationID` (PK), `LogID` (FK), `DataSetID` (FK), `StatColumn`, `Method`, `ValidatedSourceURL`.

## Relationship Explanation
- **Country Master → GDP Prediction Request:** A single country can be associated with multiple GDP prediction requests.
- **Data Set Version → Trained Model Instance:** One dataset version can be used to train multiple machine-learning model instances.
- **Data Set Version → Data Analysis Log:** A single dataset version can generate multiple analysis logs.
- **Trained Model Instance → GDP Prediction Request:** One trained model can process multiple GDP prediction requests.
- **GDP Prediction Request → Prediction Validation Status:** Each prediction request can have multiple validation records.
- **Data Analysis Log → Data Imputation Audit:** A single analysis log can contain multiple data-imputation audit records.
- **Data Set Version → Data Imputation Audit:** One dataset version can have multiple imputation audit records.

## Conceptual Data Flow
`Source Dataset → Dataset Version → Analysis/Preprocessing → Model Training → Prediction Request → Validation`

The audit entities provide traceability for preprocessing and prediction-validation activities.

## Diagram Versions
- `ER_Diagram_Original.png` preserves the first supplied ER diagram.
- `ER_Diagram_Presentation.png` preserves the second supplied presentation-style ER diagram.

## Source Consistency Note
The two supplied diagrams use different names for the dataset foreign key in `TRAINED_MODEL_INSTANCE`: `VersionID` in the first image and `TrainedOnVersionID` in the presentation image. This repository does not alter either image. Use one name consistently in the eventual implementation.
