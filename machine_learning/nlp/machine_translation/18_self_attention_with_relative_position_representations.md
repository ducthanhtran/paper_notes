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
  * warmup and decay strategy for learning rate with 4K warmup steps
* label smoothing with value 0.1
* beam search with size 4 and length penalty of value 0.6

#### Models ####

|                                   | Base | Big  |
|-----------------------------------|------|------|
| Encoder/Decoder Layers            | 6/6  | 6/6  |
| Dimensions for word emb.          | 512  | 1024 |
| Dimensions for self-attention     | 64   | 64   |
| #Attention heads                  | 8    | 16   |
| Dimensions for feed-forward layer | 1024 | 4096 |
| Dropout value (EN-DE)             | 0.1  | 0.3  |
| Dropout value (EN-FR)             | 0.1  | 0.1  |
| Max. rel. position k              | 16   | 8    |
| #Training steps                   | 100K | 300K |

* unique edge presentation per layer and head
* Big model used averaging of last 20 checkpoints, saved at 10 minute intervals
* both compared to baseline [Transformer](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/17_attention_is_all_you_need.md) with sinusoidal position encoding
* used *newstest2013* development set
* using *newstest2014* as test set

#### Results ####
On test set:
| Model | Position Encoding | EN-DE: BLEU [%] | EN-FR: BLEU [%] |
|-------------------------------|-----------------|-----------------|
| Transformer (base) | sinusoidal    | 26.5       | 38.2            |
| Transformer (base) | rel. position | **26.8**   | **38.7**        |
| Transformer (big)  | sinusoidal    | 27.9       | 41.2            |
| Transformer (big)  | rel. position | **29.2**   | **41.5**        |

* no benefit of incorporating both rel. and sinusoidal positional encodings

#### Clipping distance k ####

| k   | EN-DE BLEU[%] |
|-----|---------------|
| 0   | 12.5          |
| 1   | 25.5          |
| 2   | 25.8          |
| 4   | 25.9          |
| 16  | 25.8          |
| 64  | 25.9          |
| 256 | 25.8          |
* on English-German development set *newstest2013*
* no real significant improvement beyond k=2

## Comments ##
