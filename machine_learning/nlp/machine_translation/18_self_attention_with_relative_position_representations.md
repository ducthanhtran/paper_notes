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
* maximum rel. position is clipped at value **k** - a hyperparamter#
  * authors argue that exact information is not useful beyond certain distance
  * in total, capture window of 2k+1 edge information around a certain word

#### Implementation Issues ####
* sharing rel. position representation across attention heads improves space overhead
* authors report 7% decrease in steps/second

### Experiments ###
* WMT'14 English-German: 4.5M sentence pairs
* WMT'14 English-French: 36M sentence pairs
* split tokens into 32,768 word-piece vocabulary (similar to [BPE](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/16_nmt_of_rare_words_with_subword_units.md))
* each batch
  * consider sentence pair lengths
  * 4096 tokens limited in input and output per GPU
  * resulting in approx. 25K source and 25K target tokens for whole batch
* ADAM optimizer with beta_1=0.9, beta_2=0.98 and eps=10^-9
#### Results ####

## Comments
