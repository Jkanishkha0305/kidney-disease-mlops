# Architecture — kidney-disease-mlops

## MLOps Pipeline

```
  ┌─────────────────────────────────────────────────────────┐
  │                    MLOps Pipeline                        │
  │                                                         │
  │  1. DATA VERSIONING                                     │
  │     DVC + DagsHub remote storage                        │
  │     dvc pull → reproducible data snapshots             │
  │                                                         │
  │  2. EXPERIMENT TRACKING                                 │
  │     MLflow → logs params, metrics, artifacts           │
  │     DagsHub → hosts MLflow server                      │
  │                                                         │
  │  3. MODEL TRAINING                                      │
  │     TensorFlow CNN classifier                          │
  │     Configurable via params.yaml + config.yaml         │
  │                                                         │
  │  4. EVALUATION                                          │
  │     Validation accuracy, F1, confusion matrix          │
  │     MLflow model registry for versioning               │
  │                                                         │
  │  5. CI/CD (GitHub Actions)                             │
  │     Push → lint → train → evaluate → register         │
  │                                                         │
  │  6. DEPLOYMENT                                          │
  │     Docker container → AWS EC2 via GitHub Actions      │
  │     REST API with FastAPI                              │
  └─────────────────────────────────────────────────────────┘
```

## Reproduce

```bash
# 1. Pull versioned data
dvc pull

# 2. Run full pipeline
dvc repro

# 3. View experiments
mlflow ui
```
