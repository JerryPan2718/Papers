# Networking 
## [Experiences with Modeling Network Topologies at Multiple Levels of Abstraction](https://www.usenix.org/conference/nsdi20/presentation/mogul)
- Big networks need automated management
  - Demand forcasting and capacity planning
  - Ordering materials - racks, switches, cables, etc.
  - Configuring switches and SDN controllers.
- Multi-Abstraction-Layer Topology (MALT)
  - Google's internal standard for almost all representations of network topology.
  - Supports interoperability between many software systems.
  - Supports multiple layers of abstraction.
- Why a standard representation?
  - Decouples producers and consumers.
  - Exposes knowledge in the data, rather than hiding it in code.
  - Enables the development of shared infrastructure.
  - Overall: enables faster innovation.
  - Generate network designs automatically. 
    - Start with high-level abstractions.
    - Expand detail at each step, based on additional data.
- Basics of MALT
  - MALT is an entity-relationship model
    - Entities represent things: real or abstract
    - Entities have entity-kinds, names, and attributes
    - Relationships connect entities, and don't have attributes
  - MALT queries
    - Most applications navigate small regions of a model, not an entire graph
      - e.g. generate config for a single device; figure out what fails if a rack dies
    - MALT has a query language to make this reasonable efficient
  - MALTshop storage
    - A single replicated service for storing MALT models

## [Service Mesh: Challenges, State of the Art, and Future Research Opportunities](https://ieeexplore.ieee.org/document/8705911)
- Service Mesh: mitigate operational complexity by introducing a dedicated infrastructure layer over microservices without imposing modification on the service implementations.

## [An Open-Source Benchmark Suite for Microservices and Their Hardware-Software Implications for Cloud & Edge Systems](https://www.csl.cornell.edu/~delimitrou/papers/2019.asplos.microservices.pdf)
- DeathStarBench: study the architectural characteristics of microservices, their implications in networking and operating systems, their challenges with respect to cluster management, and their tradeoffs in terms of application design and programming frameworks.

## [NetHint: White-Box Networking for Multi-Tenant Data Centers](https://hongzhangblaze.github.io/assets/pdf/nethint.pdf)
- Incentive: adapt data-intensive applications' data transfer schedules based on the cloud network characteristics.
- NetHint: an interactive mechanism between a cloud tenant and a cloud provider to jointly enhance application performance. The NetHint design provides abundant network information for cloud tenants to compute their optimal transfer schedules, while introducing little overhead for the cloud provider to collect and expose this information.
 
