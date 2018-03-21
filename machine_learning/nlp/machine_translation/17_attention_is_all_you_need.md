# Attention Is All You Need
* [arXiv 2017](https://arxiv.org/abs/1706.03762)
* 31st Conference on Neural Information Processing Systems (NIPS) | Advances in Neural Information Processing Systems 30, 2017
  * [NIPS 2017](https://papers.nips.cc/paper/7181-attention-is-all-you-need.pdf)
* [Kaiser: Slides](https://nlp.stanford.edu/seminar/details/lkaiser.pdf)

**Authors**:
* Vaswani, Ashish
* Shazeer, Noam
* Parma, Niki
* Uszkoreit, Jakob
* Jones, Llion
* Gomez, Aidan N.
* Kaiser, Lukasz
* Polosuhkin, Illia


## Key points
* RNN: no parallelization, sequential computation
* CNN: number of operations to relate informations between arbitrary input/output positions grows with sequence length
* proposal of Transformer model
  * purely (self-)attention-based that allows parallelization
  * constant number of operations required for information flow between arbitrary sequence positions at cost of reduced resolution
* architecture:
  * encoder-decoder architecture
  * encoder: stack of N=6 layers with following sub-layers
    * 1. multi-head attention mechanism
    * 2. position-wise fully connected feed-forward (FF) network
    * residual connection followed by layer normalization
    * layers produce output of dimension 512
  * decoder: stack of N=6 layers with following sub-layers
    * 1. multi-head attention (*like in encoder*) with masking to avoid attending subsequent positions
    * 2. multi-head attention over output of encoder stack
    * 3. position-wise fully connected feed-forward (FF) network (*like in encoder*)
    * residual connection, followed by layer normalization


### Experiments ###


#### Results ####


#### Comparison on testsets with other systems ####


## Comments
