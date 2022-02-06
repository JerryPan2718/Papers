# MLSys

## Week 1: Intro
- What defines great machine learning research?
	- As the goal of machine learning algorithm is to generalize over a large dataset, good machine learning research should address how the model can generalize over different datasets and tasks, while keeping many other factors in mind, including model training and inference runtime and cost, privacy, robustness, security, ethics, and etc. Good ML research should keep the minimal as necessary for simplicity while maximizing the benefits. Learning = Representation + Evaluation + Optimization
- What defines great systems research?
	- Great systems research address key limitations, including emergent properties, propagation of effects, incommensurate scaling, and trade-offs, in a complex system while managing complexity properly for simplicity. Any additional optimization should balance the additional workload or overhead within reasonable complexity constraints. 
- What defines great machine learning systems research?
	- As the intersection area of machine learning and computer systems, a good research should apply the research methodology in machine learning to solve limitations and difficulties in system research or vice versa. The new methodology should frame the optimization problem with clear objective, manage the complexity with additional system part, balance out constrained resources with or without tradeoffs.

### Principles of Computer System Design
- Problems in Systems: 
	- 1. Emergent properties: the group could develop an unpredictable misbehavior though individual components are intact.
	- 2. Propagation of effects: a small disruption or a local change can have effects on the global system faw away.
	- 3. Incommensurate scaling: as a system increases in size or speed, not all parts of it follow the same scaling rules.
	- 4. Trade-offs: first to maximize the limited amount of goodness, second to avoid wasting it, and third to allocate it to the places where it will help the most.
- System: 
	- A set of interconnected components that has an expected behavior observed at the interface with its environment.
- Principles: 
	- Principle of escalating complexity: Adding a requirement increases complexity out of proportion.
	- Avoid excessive generality: If it's good for everything, it's good for nothing.
	- The law of diminishing returns: The more one improves some measure of goodness, the more effort the next improvement will require.
	- The unyielding foundations rule: It's easier to change a module than to change the modularity.
	- The robustness princple: Be tolerant of inputs and strict on outputs.
	- The safety margin principle: Keep track of the distance to the cliff, or you may fall over the edge.	
	- Decouple modules with indirection: Indirection supports replaceability.
	- The incommensurate scaling rule: Changing any system parameter by a factor of 10 usually requires a new design.
	- Design for iteration: You won't get it right the first time, so make it easy to change.
	- Adopt sweeping simplifications

### Key lessons for ML researchers and practitioners
- Learning = Representation + Evaluation + Optimization
- Legit Generalization
- More Data
- Different kinds of Overfitting
- Unintuitive High Dimensions
- Induction is contrasted with Deduction
- Data > Algo
- Multiple Models: model ensemble, bagging, boosting, stacking
- Simplicity !=> Accuracy
- Representable !=> Learnable 
- Correlation !=> Causation


## Week 2: Big Data Systems

### Towards a Unified Architecture for in-RDBMS Analytics
- Problem: Each new statistical technique must be implemented from scratch in the RDBMS, which leads to a lengthy and complex development process.
- Idea: A unified architecture for in-database analytics
	- Need for unified data platform architecture
		- Data warehousing functionality
		- Data lake open direct-access data formats
	- Convergence towards Lakehouses
		- First-class support for ML and data science
		- SOTA performance
	- Performance optimizations for analytics techniques can be studied generically instead of an ad hoc, per-technique fashion.
	- Two factors that impact performance: 1. The order of data is stored, 2. Parallelization of computations on a single-node multicore RDBMS.
- Optimization:
	- Prototype implementations are faster than existing approaches for simple tasks
	- We can study the factors that impact performance and optimize them in a way that applies across several analytics tasks.
	- Two factors that impact performance: 1. Data clustering, 2. Parallelism on a single-node multicore system.
- Solutions & Contributions
	- BISMARCK Architecture
	- Metadata layer
	- Declarative DataFrame APIs
- Strength
	- 1. Data is redundantly stored in data lakes and data warehouses.
	- 2. Data lakes solved the proliferation of unstructured data, but introduced complex pipelines from the late to the warehouse.
	- 3. Cost/Execution time are both better. 
- Weakness
	- 1. Lakehouses make it harder to take advantage of specialized query optimizers build specifically for BI.
	- 2. Have to maintain fine-grain permissions for security and privacy. 
	- 3. Overhead to migrate existing data and infrastructure. 

### Lakehouse: A New Generation of Open Platforms that Unify Data Warehousing and Advanced Analytics
- Challenges: 
	- 1. Data quality and reliability, 
	- 2. Increased data staleness with a separate staging area for incoming data before the warehouse, 
	- 3. Unstructured data
- Lakehouse Architecture:
	- The system store data in a low-cost object store using a standard file format
	- Metadata layers over data lake storage

### Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing
- Problem: how to define abstractions to efficiently execute iterative applications in a distributed setting
	- Metrics for succeess: runtime
- Background:
	- MapReduce and Dryad for big data analytics: provided operators that allowed users to writy parallel computations, but lack abstractions for leveraging distributed memory
- Solutions
	- Resilient Distributed Datasets: a distributed memory abstraction that lets programmers perform in-memory computations on large clusters in a fault-tolerant manner.
	- Spark: the system that leverages RDD

## Week 3: Hardware for ML

### Mixed Precision Training
- Solutions & Contributions
	- Training DNN using half-precision floating point numbers without losing model accuracy or having to modify hyperparameters.
	- Halves memory requirements and speeds up arithmetic.
	- 3 Techniques to prevent model accuracy loss
		- Maintaining a master copy of weights in FP32
		- Loss-scaling that minimizes gradient values becoming zeros
		- FP16 arithmetic with accumulation in FP32

### Eyeriss: A Spatial Architecture for Energy-Efficient Dataflow for Convolutional Neural Networks
- Solutions & Contributions
	- A novel dataflow called row-stationary (RS) to minimize data movement energy consumption on a spatial architecture by exploiting local data reuse of filter weights and feature map pixels.
	- An analysis framework that can quantify the energy efficiency for different CNN dataflows under the same hardware constraints.

### Interstellar: Using Halide’s Scheduling Language to Analyze DNN Accelerators
- Solutions & Contributions
	- Halide's scheduling language can quickly explore different dataflow and loop blocking choices, and then consider hardware resource optimizations.

### Gemmini: Enabling Systematic Deep-Learning Architecture Evaluation via Full-Stack Integration
- Challenges
	- NN accelerators are developed in isolation of cross-stack and system-level effects, which makes it difficult to appreciate the impact of System-on-Chip (SoC) resource contention, OS overheads, and programming-stack inefficiencies on overall performance/energy-efficiency.
- Solutions & Contributions
	- Gemmini, a full-stack DNN accelerator generator, generates a wide design-space of efficient ASIC accelerators from a flexible architectural template.


![Screen Shot 2022-02-06 at 12 33 46](https://user-images.githubusercontent.com/37657480/152700325-fe79ae44-2846-40d3-9f14-9c0f38d141ad.png)


