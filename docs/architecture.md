sequenceDiagram
  participant Dev as Dev Project
  participant ADO as Azure DevOps
  participant REG as Registry
  participant QA as QA Project
  participant PROD as Prod Project

  Dev->>ADO: push/train outputs (model artifacts)
  ADO->>REG: az ml model create (NAME, VERSION, tags)
  ADO->>ADO: run evaluation, enforce thresholds
  ADO->>QA: az ml online-endpoint/deployment (model:version@REG)
  QA-->>ADO: smoke test OK
  ADO->>PROD: az ml online-deployment (same model:version)
  PROD-->>ADO: health check OK
