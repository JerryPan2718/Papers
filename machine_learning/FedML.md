# FedML: A Research Library and Benchmark for Federated Machine Learning

## Diverse areas of focus within Federated Learning
- Statistical challenges: Distributed optimization, non-IID and model personalization, Semi-supervised Learning, Neural Architecture Search, Meta-Learning
- Security/Privacy: Preserving privacy, Adversarial attack, Fairness, Incentive Mechanism
- System Constraints: Communication efficiency, computation efficiency, wireless communication, cloud computing, FL system
- Models and Applications: NLP, CV, Data Mining, and etc.
- https://github.com/chaoyanghe/Awesome-Federated-Learning
1. Communication Efficiency
- Trade computation for communication
- e.g. Federated Averaging Algorithm (converges with SGD and GD for IID and non-IID data)
2. Privacy 
- Training data can be reversely inferred from the model
3. Adversarial Robustness
- Attack 1: Data poisoning attack
- Attack 2: Model poisoning attack
- Defense 1: Server check validation accuracy
- Defense 2: Server check gradient statistics 
- Defense 3: Byzantine-tolerant aggregation

## Background 

### FL Library
- TensorFlow Federated (TFF) by Google Research 
- LEAF
- PySyft
- FATE 

### Challenge: Platform Diversity
1. Diversity of platforms and Cross-platform migration
- Three computing platforms (IoT/Mobile, Distributed Computing, Standalone Simulation)
2. Diverse topologies
- Diverse demands on information exchange protocols, and training procedures
3. Newly published algorithms are not working on the same benchmarking (models, datasets, non-IID partition, hyper-parameters, and etc.)

## FedML Library - Design Goal
1. Keep pace with advances in Academia
2. Write Once, Run Everywhere with seamless cross-platform migration
3. Innovate on algorithsm and let the library do the implementation

## FedML-core
- Worker-oriented Programming Interface
- Trainer Customization

## Federated Learning v.s. Distributed Learning
- Federated Learning is a kind of Distributed Learning
1. Ucers have control over their device and data
2. Worker nodes are unstable
3. Communication cost is higher than computation cost
4. Data stored on worker nodes are not IID
5. The amount of data is severly imbalanced
- Objective: jointly learn a model without sharing data
- Unique challenges, e.g.
	- Non-IID data
	- Slow communication

