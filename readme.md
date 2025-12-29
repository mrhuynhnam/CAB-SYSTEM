flowchart TB

subgraph Client
  C1[Customer App\nReactJS]
  C2[Driver App\nReactJS]
  C3[Admin Dashboard\nReactJS]
end

subgraph Gateway
  G[API Gateway\nNodeJS]
end

subgraph Microservices
  A[Auth]
  U[User]
  D[Driver]
  B[Booking]
  P[Pricing]
  R[Ride]
  Pay[Payment]
  N[Notification]
  Rev[Review]
end

subgraph Broker
  K[Kafka / RabbitMQ]
end

subgraph Data
  PG[(PostgreSQL)]
  MG[(MongoDB)]
  RD[(Redis)]
end

C1 --> G
C2 --> G
C3 --> G

G --> A
G --> U
G --> D
G --> B
G --> P
G --> R
G --> Pay
G --> N
G --> Rev

B --> K
R --> K
Pay --> K

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
