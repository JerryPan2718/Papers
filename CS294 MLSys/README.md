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

## Week 4: Distributed Deep Learning, Part I: Systems

### Chimera: Efficiently Training Large-Scale Neural Networks with Bidirectional Pipelines
- Chimera
	- A novel pipeline parallelism scheme which combines bidirectional pipelines for efficiently training large-scale models.
	- A synchronous approach and therefore no loss of accuracy.
	- Reduces the number of bubbles by up to 50% compared with the latest synchronous pipeline approach.
	- A more balanced activation memory consumption.
	- Takeaways: for large models that are easily partitioned into balanced stages, clever scheduling of comput and gradient synchronization can reduce pipeline bubbles.
	- With model replicas, it takes advantage of both model and data parallelism.

<img width="1400" alt="Screen Shot 2022-02-14 at 14 19 28" src="https://user-images.githubusercontent.com/37657480/153962761-9bd503b1-6887-47ee-bba7-ac10f2170ba2.png">

### ZeRO-Infinity: Breaking the GPU Memory Wall for Extreme Scale Deep Learning
- Challenges
	- Large model >> GPU memory limit
- Solutions
	- Infinity offload engine: use CPU, GPU, NVMe as seamless pool of memory, leverage CPU for compute
	- Memory-centric tiling: handle large operators without splitting model across GPUs
	- Bandwidth-centric partitioning: goal is to put throughout of all available devices to best use
	- Overlap-centrix design: minimize pipeline bubbles by interleaving compute and communications
	- Withouy model code refactoring

![Screen Shot 2022-02-14 at 15 11 45](https://user-images.githubusercontent.com/37657480/153962705-4d132ab5-4c32-4904-979d-6feaa8fd356b.png)

### Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM
- Challenges
	- GPU memory capacity is limited
	- The number of compute operations required can result in unrealistically long training times
- Solutions
	- Can compose pipeline, tensor, and data parallelism to get near-linear weak scaling on large models by analyzing their communication tradeoffs.

<img width="1207" alt="Screen Shot 2022-02-14 at 15 18 26" src="https://user-images.githubusercontent.com/37657480/153963222-b3fb2aea-16e6-459c-8a36-14eb4432316d.png">

## Week 5: Holiday
## Week 6: Distributed deep learning, Part II: Scaling Constraints

### Measuring the Effects of Data Parallelism on Neural Network Training
- Contributions
	- Experimentally characterized the effects of increasing the batch size on training time, as measured by the number of steps necessary to reach a goal out-of-sample error. 
	- Studied the above relationship varied with the training algorithm, mode, and dataset, adn found extremely large variation between workloads.
	- Showed that disagreements in the literature on how batch size affects model quality can largely be explained by differences in metaparameter tuning and compute budgets at different batch sizes.
- Results
	- Lots of experimental results

### Scaling Laws for Neural Language Models
- Contributions & Key Findings
	- Performance depends strongly on scale, weakly on model shape
	- Smooth power laws
	- Universality of overfitting
	- Universality of training
	- Transfer improves with test performance
	- Sample efficiency
	- Convergence is inefficient
	- Optimal batch size
![Screen Shot 2022-02-28 at 14 18 17](https://user-images.githubusercontent.com/37657480/156068395-2a5737bc-a922-4efd-b30d-ceb8d8be024f.png)
- Summary of scaling laws
	![Screen Shot 2022-02-28 at 14 21 51](https://user-images.githubusercontent.com/37657480/156068373-804da422-6c69-4e82-8741-c6bff3c9070e.png)

### Deep Learning Training in Facebook Data Centers: Design of Scale-up and Scale-out system
- Deep learning recommendation models (DLRMs)
	- Exercise not only compute but also memory capacity as well as memory and network bandwidth. Efficiently scaling training becomes a challenge as the model size and complexity increase. 
	- Designed Zion Facebooks next-generation large-memory training platform that consists of both CPUs and accelerators: Zion scale-up system can be used for training of DLRMs.
		- Zion introduced the common form factor OCP Accelerator Module (OAM)
	- Discussed different aspects of training of DLRMs: asynchronous and synchronous training, data-parallelism and model-parallelism patterns map to allreduce and all2all communication primitives.
![Screen Shot 2022-02-28 at 14 40 28](https://user-images.githubusercontent.com/37657480/156072945-a51431f1-0c1c-4fc3-909f-176de7c56f9c.png)

## Week 7: Project Proposal
## Week 8: ML Applied to Systems

### Device Placement Optimization with Reinforcement Learning
- Contributions
	- Propose a method which learns to optimize device placement for TensorFlow computational graphs.
	- Use a sequence-to-sequence model to predict which subsets of operations in a TensorFlow graph should run on which of the available devices.

### The Case for Learned Index Structures
- Background
	- Indexes are models: a B-Tree-Index can be seen as a model to map a key to the position of a record within a sorted array, a Hash-Index as a model to map a key to a position of a record within an unsorted array, and a BitMap-Index as a model to indicate if a data record exists or not.
- Contributions
	- A model can learn the sort order or structure of lookup keys and use this signal to effectively predict the position or existence of records.

### Neural Adaptive Video Streaming with Pensieve
- Pensieve: use RL to generate ABR algorithms


## Week 10: Machine Learning Frameworks and Automatic Differentiation

### Automatic differentiation in ML: Where we are and where we should be going?
- Proposed a functional, typed, and graph-based intermediate representation (IR) for AD to achieve both flexibility/generality and performance
- Metric: performance, expressive power, usability
- Related work
	- Operator overloading (e.g. PyTorch): the derivative problem is dynamically constructed upon execution.
	- Source transformation (ADIFOR, Tapenade): ST to explicitly construct a program with a reversed control flow.
	- Dataflow programming (e.g. TensorFlow/Theano): Rely on computation DAGs as intermediate representation without scoping for simplicity and optimization
### TensorFlow: A System for Large-Scale Machine Learning
- TensorFlow addresses the growing need for experimenting with new models, training on large datasets, and achieving large-scale production. 
	- Supports large-scale training and production: both performance and flexibility.
	- Represent mathematical operators as nodes in the dataflow graph to easily compose novel layers using scripting interface.
	- Mutable state and its operations are nodes for each of experimentation with different update rules. 
### TVM: An Automated End-to-End Optimizing Compiler for Deep Learning
- Declarative tensor expression language
	- Maps operator's algebraic expression -> possible schedules
	- Introduces two new schedule primitives
		- Memory scope -> efficient use of GPU shared memory
		- Tensorization -> plug-in interface for hardware intrinsics and micro-kernels
- Automated schedule optimizer
	- Search space: schedule templates & their tunable knobs
	- Cost-estimation: gradient-boosted tree
	- Search algorithm: simulated annealing

### Abstractions for ML Compilations by Tianqi Chen
- Trend: The software ecosystem tunnel becomes a lot wider from the narrow tunnel.
<img width="1364" alt="Screen Shot 2022-03-28 at 15 38 18" src="https://user-images.githubusercontent.com/37657480/160498699-451b56ac-7f90-4a55-9782-4605f6a80420.png">
<img width="1392" alt="Screen Shot 2022-03-28 at 15 47 00" src="https://user-images.githubusercontent.com/37657480/160499393-c3fd0d1c-52d3-46ac-8db5-55a1c87e2508.png">


## Week 11: Efficient ML

### Quantization and Training of Neural Networks for Efficient Integer-Arithmetic-Only Inference
- Contributions
	- Quantized Inference (Integer-arithmetic-only Inference)
		- Represents weights and activations as integers
		- Performs arithmetic operations (e.g., matmul) on the quantized values without dequantizing them
	- Quantized Training (Quantization-Aware Training)
		- Weights and activations in FP
		- Simulates quantization effect during training by applying "fake quantization" to weights and activations.

### Linear Mode Connectivity and the Lottery Ticket Hypothesis
- Contributions
	- Study whether a neural network optimizes to the same, linearly connected minimum under different samples of SGD noise. Study iterative magnitude  pruning (IMP), the procedure used by work on the lottery ticket hypothesis to identify subnetworks that could have trained in isolation to full accuracy. These subnetworks only reach full accuracy when they are stable to SGD noise, which either occurs at initialization for small-scale settings (MNIST) or early in training for large-scale settings.
	- Proposes instability analysis as a way to shed light on how SGD noise affects the outcome of optimizing neural networks.

### FBNet: Hardware-Aware Efficient ConvNet Design via Differentiable Neural Architecture Search
- Contributions
	- Problem: Design NN architectures that are both accurate and efficient is challenging due to extremely large design space.
	- Key metrics: accuracy and efficiency
	- Differential NAS at the layer-level: repeat for different inpuyt size/device
		- Set a microarchitecture of network, composed of "blocks"
		- Loss: cross-entropy loss + latnecy penalty
		- Search space, as "stochastic super net"

## Week 12: ML in the Cloud

### The Sky Above the Cloud
- Intercloud brokers will act as an intermediary between a user's application and various cloud service providers by designing and executing an optimal cloud setup for that application.
	- Characterizes the anti-competitive incentives in the status quo: low ingress cost, high egress cost, volume discounts, and proprietary interfaces
- Limitation: few services will dominate the market, limiting the use of intercloud brokers.
- Key insights: if implemented, Sky computing aims to bring about more market competition to encourage overall better cloud services.

### FrugalML: How to Use ML Prediction APIs More Accurately and Cheaply
- Learn a two-phase pipeline
	- Step 1: Predict with base API to obtain label and confidence 
	- Step 2: Compare confidence with a threshold
	- Step 3: If base API is not confident, predict with a 2nd API

### Understanding and Efficiently Consuming ML-as-a-Service by Matei Zaharia
- FrugalML
- MASA: ML API Shift Assessment

## Week 13: Benchmarking Machine Learning Workloads

### ML Benchmarking by Prof. Vijay Janapa Reddi
<img width="1270" alt="Screen Shot 2022-04-18 at 13 16 47" src="https://user-images.githubusercontent.com/37657480/163871262-80b66271-8afd-4b59-93c3-974c64c978a6.png">
<img width="1266" alt="Screen Shot 2022-04-18 at 13 34 26" src="https://user-images.githubusercontent.com/37657480/163873651-6d3aed73-ac76-43bb-a137-ba00fe04d951.png">

### Benchmark Analysis of Representative Deep Neural Network Architectures
- DNN multiple performance indices benchmark

### MLPerf Inference Benchmark
### MLPerf Training Benchmark