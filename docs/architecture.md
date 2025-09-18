# Deployment Flow -Dev → QA → Prod

```mermaid
flowchart LR
  A[[Commit / New Model in Dev]] --> B[Build & Package]
  B --> C[Register model in Registry: NAME:VERSION@REGISTRY]
  C --> D[Evaluate offline quality gate]
  D -->|Pass| E[Deploy Infra -ARM/Bicep per environment]
  E --> F[Deploy to DEV Project -Endpoint + Deployment]
  F --> G{Manual Approval}
  G -->|Approved| H[Deploy to QA Project -same model:version]
  H --> I[Smoke/Functional Tests]
  I --> J{Manual Approval}
  J -->|Approved| K[Deploy to PROD Project -same model:version]
  D -->|Fail| X[[Stop: do not promote]]
