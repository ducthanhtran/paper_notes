# A Convolutional Encoder Model for Neural Machine Translation
* ArXiv November 2016

**Authors**:
* Gehring, Jonas
* Auli, Michael
* Grangier, David
* Dauphin, Yann N.

## Key points
* problem of RNN-based encoders: non-parallelizability
* non-recurrent encoders
  1. pooling encoder
    * average embeddings of **k** consecutive words
    * add positional embedding information to encode absolute position of word within source sentence
    * attention computation uses sum of both positional and word embedding
  2. CNN encoder
    * stacking of several convolutional layers allows us to increase context size information
    * also use pos. embedding information like in pooling encoder
    * residual connections of each convolution to output - before non-linear activation (tanh)
    * no pooling layers, i.e. no downsampling
    * overall architecture:
      * a CNN-a to compute encoder output z_j. Use these to compute attention scores
      * a CNN-c to compute context vector c_i for decoder using attention scores
    * advantages:
      * possibility of parallelization
      * applying fixed number of non-linearities in bottom-up manner


## Experiments
* IWSLT'14 German-English
  * 176K sentence pairs
  * test: tst2010, tst2011, tst2012, tst2013 and dev2010
* WMT'14 English-French
  * subset of 12M sentence pairs, removing sentences longer than 150 words -> 10.7M sentence pairs
  * test: ntst14
* WMT'15 English-German
  * europarl v7, common crawl and news-commentary v10, in total: 3.9M sentence pairs
  * test: newstest2015
* WMT'16 English-Romanian
  * 2.8M sentence pairs
  * test: newstest2016
Comparison done to recurrent-based models using attention and Adam as optimizing algorithm. The pooling and CNN encoder use SGD and annealing, coupled with learning rate of 0.1 and early stopping based on perplexity.

### Models
1. LSTM encoder
2. bi-LSTM encoder
3. Pooling encoder
4. CNN encoder
5. Deep CNN 6/3 encoder (6 CNN-a and 3 CNN-c)

### Kernel width
* Pooling encoder: set **k** to 5 for all experiments
* CNN encoder: kernel width **k** to 3 for all experiments



### Results
* IWSLT'14
  * Deep CNN 6/3 outperforms bi-LSTM when using positional and word embedding: 30.4 vs. 29.7 BLEU
  * positional embeddings important, even more so in shallow models
    * 29.9 vs. 20.1 BLEU for CNN encoder
    * 30.4 vs. 25.2 BLEU for deep CNN 6/3 encoder
* WMT'14
  * comparison to
    * Luong et al., 2015; 6-layer LSTM encoder: 32.7 BLEU
    * Zhou et al., 2016; 9-layer LSTM encoder, 7-layer decoder, shortcut connections, dropout and L2 regularization: 35.9 BLEU
    * bi-LSTM encoder + single-layer decoder: 34.3
    * two-layer bi-LSTM encoder + two-layer decoder: 35.3 BLEU
  * deep CNN 8/4: 34.6 BLEU
  * deep CNN 20/5: 35.7 BLEU
* WMT'15
  * comparison to
    * Jean et al., 2015; large output vocabulary: 22.4 BLEU
    * Chung et al., 2016; character-level decoder: 23.9 BLEU
    * Yang et al., 2016; LSTMs instead of GRU + UNK replacement + recurrent attention: 25 BLEU
    * bi-LSTM encoder + single-layer decoder: 23.5 BLEU
    * two-layer bi-LSTM encoder + two-layer decoder: 24.1 BLEU
  * deep CNN 15/5 achieves 23.6 BLEU score, with a single-layer decoder
  * deep CNN 15/5 achieves 24.2 BLEU score, with a two-layer decoder - outperforming baselines of LSTM encoders
* WMT'16
  * comparison to
    * SOTA of Sennrich, 2016: 28.1 BLEU
    * bi-LSTM encoder: 27.5 BLEU
  * a deep CNN 8/4 achieves competitive BLEU: 27.8 BLEU
  * even a single CNN achieves 27.1 BLEU

## Comments
* competitive architecure that can utilize parallel computation
