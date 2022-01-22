# Cached Models

## Cache Based Recurrent Neural Network Language Model Inference For First Pass Speech Recognition
- Idea
	- Restrict the RNNLM calls to those words with reasonable score according to a n-gram model and deploy a set of caches to reduce the cost of RNNLM in the first pass to the cost of using an additional n-gram model.
- Cache implementation
	- Caches are implemented as hash tables to store key value pairs
	- Dynamically constructed as the decoder makes LM calls
	- Cache 1: LM probability 
	- Cache 2: key-value pairs of histories and their corresponding hidden state vectors
	- Cache 3: the class normalization term 
	- Cache 4: the history and calss normalization term 

## EL-Attention: Memory Efficient Lossless Attention for Generation
- Problem
	- Cache brings up memory-related costs and prevents leveraging larger batch size for faster speed
- Idea
	- EL-attention: avoid heavy operations for building multi-head keys and values.
	- Constructs an ensemble of attention results by expanding query while keeping key and value shared.
	- Memory used for caching input related model states: reduced from O(L*d_m) to O(d_m), where L is # decoder layers and d_m is model dimension.


## Cache-Augmented Latent Topic Language Models for Speech Retrieval
- Idea
	- Cached model capture word repetition for its suitability as a LM for speech recognition and retrieval.