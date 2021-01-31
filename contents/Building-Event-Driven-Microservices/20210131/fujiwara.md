## 読書メモ

# Chapter7
- Advantages of Using Internal State
  - SCALABILITY REQUIREMENTS ARE OFFLOADED FROM THE DEVELOPER
  - HIGH-PERFORMANCE DISK-BASED OPTIONS
  - FLEXIBILITY TO USE NETWORK-ATTACHED DISK
- Disadvantages of Using Internal State
  - LIMITED TO USING RUNTIME-DEFINED DISK
  - WASTED DISK SPACE
- Scaling and Recovery of Internal State
  - USING HOT REPLICAS
  - RESTORING AND SCALING FROM CHANGELOGS
  - RESTORING AND SCALING FROM INPUT EVENT STREAMS
- Advantages of External State
  - FULL DATA LOCALITY
  - TECHNOLOGY
- Drawbacks of External State
  - MANAGEMENT OF MULTIPLE TECHNOLOGIES
  - PERFORMANCE LOSS DUE TO NETWORK LATENCY
  - FINANCIAL COST OF EXTERNAL STATE STORE SERVICES
  - FULL DATA LOCALITY
- Scaling and Recovery with External State Stores
  - USING THE SOURCE STREAMS
  - USING CHANGELOGS
      - Rebuilding external state stores from source event streams or changelogs can be prohibitively time-consuming due to network latency overhead. Make sure you can still meet the microservice SLAs in such a scenario.
  - USING SNAPSHOTS
- Rebuilding Versus Migrating State Stores
- Transactions and Effectively Once Processing
  - Transactions and Effectively Once Processing
  - Effectively Once Processing Without Client-Broker Transactions

# Chapter8
- Choreographed Transactions: The Saga Pattern
  - Remember the single-writer principle. No more than one service should publish to an event stream.
- Compensation Workflows
