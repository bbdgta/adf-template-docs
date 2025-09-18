# Deployment Flow

```mermaid
flowchart LR
  A[[Commit / New Model in Dev]] --> B[Build & Package]
  B --> C[Register model in Registry<br/>azureml:NAME:VERSION@REGISTRY]
  C --> D[Evaluate offline (quality gate)]
  D -->|Pass| E[Deploy Infra (ARM/Bicep)<br/>per env: Project+KV+ST+Search]
  E --> F[Deploy to DEV Project<br/>Create/Update Endpoint + Deployment]
  F --> G{Manual Approval}
  G -->|Approved| H[Deploy to QA Project<br/>Use same model:version]
  H --> I[Smoke/Functional Tests]
  I --> J{Manual Approval}
  J -->|Approved| K[Deploy to PROD Project<br/>Use same model:version]
  D -->|Fail| X[[Stop: do not promote]]
