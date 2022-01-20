# MLSys

## Week 1
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
