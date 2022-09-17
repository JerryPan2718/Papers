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
  
