flowchart TB

subgraph Client_Layer[Client Layer]
  C1[Customer App
ReactJS]
  C2[Driver App
ReactJS]
  C3[Admin Dashboard
ReactJS]
end

subgraph Gateway[API Gateway]
  G[API Gateway
NodeJS]
end

subgraph Microservices[Microservices Layer]
  A[Auth Service]
  U[User Service]
  D[Driver Service]
  B[Booking Service]
  P[Pricing Service]
  R[Ride Service]
  Pay[Payment Service]
  N[Notification Service]
  Rev[Review Service]
end

subgraph Broker[Message Broker]
  K[Kafka / RabbitMQ]
end

subgraph Data[Data Layer]
  PG[(PostgreSQL)]
  MG[(MongoDB)]
  RD[(Redis)]
end

C1 -->|HTTPS / WS| G
C2 -->|HTTPS / WS| G
C3 -->|HTTPS| G

G --> A
G --> U
G --> D
G --> B
G --> P
G --> R
G --> Pay
G --> N
G --> Rev

B -->|RideCreated| K
R -->|RideStatusChanged| K
Pay -->|PaymentSuccess| K

A --> PG
U --> PG
D --> PG
Pay --> PG
Rev --> PG

B --> MG
R --> MG
N --> MG

D --> RD
R --> RD
