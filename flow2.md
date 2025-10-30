''''mermaid
flowchart LR
  subgraph Clients
    U1v1[UI-1 (old)]
    U2v1[UI-2 (old)]
    U3v1[UI-3 (old)]
    U4v1[UI-4 (old)]
    U5v1[UI-5 (old)]
    U1v2[UI-1 (new)]
    U2v2[UI-2 (new)]
    U3v2[UI-3 (new)]
    U4v2[UI-4 (new)]
    U5v2[UI-5 (new)]
  end

  U1v1 --> APIOld[(API v1)]
  U2v1 --> APIOld
  U3v1 --> APIOld
  U4v1 --> APIOld
  U5v1 --> APIOld

  U1v2 --> APINew[(API v2)]
  U2v2 --> APINew
  U3v2 --> APINew
  U4v2 --> APINew
  U5v2 --> APINew

  subgraph AKS Cluster
    subgraph edge-v1 ns
      APIOld --> MS1v1[ordersvc v1]
      APIOld --> MS2v1[paymentsvc v1]
      APIOld --> MS3v1[clientsvc v1]
      APIOld --> MS4v1[notificationsvc v1]
      APIOld --> MS5v1[dashboardsvc v1]
    end
    subgraph edge-v2 ns
      APINew --> MS1v2[ordersvc v2]
      APINew --> MS2v2[paymentsvc v2]
      APINew --> MS3v2[clientsvc v2]
      APINew --> MS4v2[notificationsvc v2]
      APINew --> MS5v2[dashboardsvc v2]
    end
  end

  subgraph Shared Core
    KV[(Key Vault)]
    DB[(Database)]
  end

  MS1v1 --> KV
  MS2v1 --> KV
  MS3v1 --> KV
  MS4v1 --> KV
  MS5v1 --> KV

  MS1v2 --> KV
  MS2v2 --> KV
  MS3v2 --> KV
  MS4v2 --> KV
  MS5v2 --> KV

  MS1v1 <--> DB
  MS2v1 <--> DB
  MS3v1 <--> DB
  MS4v1 <--> DB
  MS5v1 <--> DB

  MS1v2 <--> DB
  MS2v2 <--> DB
  MS3v2 <--> DB
  MS4v2 <--> DB
  MS5v2 <--> DB
