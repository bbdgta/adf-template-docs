
---

## ✅ Corrected Topology Diagram

```markdown
# Topology (Projects per Env + Registry)

```mermaid
graph TD
  subgraph Dev_RG["Resource Group: DEV"]
    DevP[Foundry Project: DEV]
    DevEP[(Endpoint: dev-mymodel)]
    DevP --> DevEP
  end

  subgraph Shared["Cross-Env Artifact"]
    REG[[Azure ML / AI Registry]]
  end

  subgraph QA_RG["Resource Group: QA"]
    QaP[Foundry Project: QA]
    QaEP[(Endpoint: qa-mymodel)]
    QaP --> QaEP
  end

  subgraph Prod_RG["Resource Group: PROD"]
    PrP[Foundry Project: PROD]
    PrEP[(Endpoint: prod-mymodel)]
    PrP --> PrEP
  end

  DevP -- register model --> REG
  REG -- promote same version --> QaP
  REG -- promote same version --> PrP
