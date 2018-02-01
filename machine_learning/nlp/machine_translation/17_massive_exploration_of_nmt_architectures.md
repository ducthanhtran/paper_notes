# Massive Exploration of Neural Machine Translation Architectures
* [arXiv, 2017](https://arxiv.org/pdf/1703.03906)
* [EMNLP, 2017](http://aclweb.org/anthology/D17-1151)

**Authors**:
* Britz, Denny
* Goldie, Anna
* Luong, Ming-Thanh
* Le, Quoc V.

## Key points
* experimental investigations of hyperparameters of a typical attention-based encoder-decoder architecture including few architectural designs
  * embedding dimensionality
  * RNN Cell Type (GRU vs. LSTM)
  * encoder and decoder depth
  * uni- vs. bi-directional encoder
  * attention mechanism (additive vs. dot-product)
  * beam width


### Experiments ###
* WMT'15 English->German: 4.5M sentence pairs
  * validation: newstest2013
  * test: newstest2014, newstest2015
* small scale experiment on WMT'15 English->French highly correlated to results of English->German
* preprocessing: Tokenization with Moses-Script + [BPE](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/16_nmt_of_rare_words_with_subword_units.md) (32K merges)
  * vocabulary size: 37K
* performance measured in BLEU

#### Baseline model ####
* 2-layer BLSTM encoder and 2-layer decoder
  * both have 512 GRUs
  * dropout 0.2 at input of each cell
* attention mechanism: multiplicative
* ADAM with fixed learning rate of 0.0001
* embedding dimensionality: 512

#### Results ####
Results reported on newstest2013.
* embedding dimensionality
  * no significant improvement by increasing embedding dimensionality
  * convergence required more time
  * large increase in parameters
* RNN Cell Type (GRU vs. LSTM)
  * LSTM cells outperformed
  * no difference in training speed
  * using vanilla decoder degrades BLEU performance heavily
* encoder and decoder depth
  * encoder: no real benefit of using more than 2 layers. Using 4 layers was best but with a low improvement over 2 layers, that is, 21.78 BLEU to 21.85 BLEU.
  * decoder: increase of 0.5 BLEU by going from 1/2 to 4 layers. For more layers residual connections have to be employed but no significant improvement can be observed.
* uni- vs. bi-directional encoder
  * bi-directional encoder has best performance, but margin to uni-directional ones are small. In addition, reversing the source sentence improves performance.
* attention mechanism (additive vs. dot-product)
  * attention-dimensionality has little effect (128-1024 tested)
  * additive from Bahdanau et al. outperforms multiplicative one, best at 512 attention-dimensionality
* beam width
  * length normalization/penalty (1.0) improves BLEU by about 0.3
  * has sweet spot - too large widths result in degradation

#### Comparison on testsets with other systems ####
* final configuration:
  * embedding dim.: 512
  * LSTM cells
  * bi-directional 2-layer encoder and decoder has depth 4
  * attention: additive by Bahdanau et al. and employing 512 dimensions
  * beam size 10 with length penalty 1.0

* newstest2014: 22.19
* newstest2015: 25.23
* outperform other systems like bpe2bpe ([Sennrich et al., 2016](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/16_nmt_of_rare_words_with_subword_units.md)) and bpe2char ([Chung et al., 2016](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/16_a_character_level_decoder_without_explicit_segmentation_for_nmt.md))

## Comments
* training and architecture settings of other systems not reported in testset comparisons
* 'best performing' model in table 8 should be 'baseline' model from section 3.3
