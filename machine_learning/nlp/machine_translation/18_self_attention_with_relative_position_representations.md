# Self-Attention with Relative Position Representations
* [arXiv 2018](https://arxiv.org/abs/1803.02155)
* NAACL-HLT 2018

**Authors**:
* Shaw, Peter
* Uszkoreit, Jakob
* Vaswani, Ashish

## Key points
* extend self-attention: additionally consider pairwise relationships between input elements
  * *directed, complete graph* where labels on edge ij is denoted by weight alpha_ij from self-attention
  * these *edges* capture information about rel. position differences between input elements
  * incorporate edge information in self-attention by summation (small computational overhead)
* additional parameters are learned and shared across attention-heads
* maximum rel. position is clipped at value **k** - a hyperparamter


### Experiments ###
#### Results ####

## Comments
