```mermaid 
flowchart LR
    subgraph Client
      UINew1[New UI #1]
      UINew2[New UI #2]
      UIOld1[Old UI #1]
      UIOld2[Old UI #2]
      UIOld3[Old UI #3]
      UIOld4[Old UI #4]
      UIOld5[Old UI #5]
      UINew3[New UI #3]
      UINew4[New UI #4]
      UINew5[New UI #5]
    end

    UINew1 -->|HTTPS| APINew[(New API)]
    UINew2 -->|HTTPS| APINew
    UINew3 -->|HTTPS| APINew
    UINew4 -->|HTTPS| APINew
    UINew5 -->|HTTPS| APINew

    UIOld1 -->|HTTPS| APIOld[(Old API)]
    UIOld2 -->|HTTPS| APIOld
    UIOld3 -->|HTTPS| APIOld
    UIOld4 -->|HTTPS| APIOld
    UIOld5 -->|HTTPS| APIOld

    subgraph AKS[AKS Cluster]
      MS1[Service 1]
      MS2[Service 2]
      MS3[Service 3]
      MS4[Service 4]
      MS5[Service 5]
    end

    APINew --> MS1
    APINew --> MS2
    APINew --> MS3
    APINew --> MS4
    APINew --> MS5

    APIOld --> MS1
    APIOld --> MS2
    APIOld --> MS3
    APIOld --> MS4
    APIOld --> MS5

    subgraph Shared Core
      KV[(Key Vault)]
      DB[(Database)]
    end

    MS1 --> KV
    MS2 --> KV
    MS3 --> KV
    MS4 --> KV
    MS5 --> KV

    MS1 <--> DB
    MS2 <--> DB
    MS3 <--> DB
    MS4 <--> DB
    MS5 <--> DB
