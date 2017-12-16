# Is Statistical Machine Translation Approach Dead?
* ICNLSSP 2017

**Authors**:
* Menacer, M.A.
* Langlois, D.
* Mella, O.
* Fohr, D.
* Jouvet, D.
* Smaili, K.

## Key points
* a short survey/overview-paper about neural machine translation (NMT)
* rise of neural machine translation; show promising results comparable or even surpassing those of statistical machine translation approaches (SMT)
* previous popular approach: language and translation model, plus other components like reordering model in phrase-based translation systems
* neural machine translation
    * end-to-end system that directly transforms source sentence into a target one by using a single neural network
    * encoder-decoder architecture and attention mechanism

## Experiments
* Arabic-English translation task
    * data: Multiun (United Nations parallel corpus)
    * training set: 100K parallel sentences
    * development set: 1K parallel sentences
    * testing set: 1K sentences
    * 24K Arabic words and 20K English words
* beam size of 1

#### Models
1. SMT (Baseline): 3-gram language model
2. NMT (Baseline): pure Encoder-Decoder approach: RNN, one hidden layer and each RNN bloc has 100 hidden units
3. Baseline NMT + Attention (RNN)
4. Baseline NMT + Attention (RNN) + Rare Words
    * first approach: external dictionary by Luong et al.
        * translate unknown tokens in post-processing step
    * second approach: discounting by Arthur et al.
        * discount probabilties during training, considering out-of-vocabulary words (reserving probability mass)
    * for experiments: built dictionary of 10M entries from corpus of 9M parallel sentences
5. Baseline NMT + Attention (LSTM) (+ Rare Words?)
6. Baseline NMT + Attention (RNN) + Rare Words + Word Penalty (Beam Size equivalent) Modification

### Results
#### 1. Baseline SMT
* dev: 33.72 BLEU and test: 24.54 BLEU

#### 2. Baseline NMT

|Optimization method|dev. BLEU|test BLEU|
|-------|---------|---------|
|SGD|7.83|5.35|
|Momentum|4.19|2.89|
|AdaGrad|6.27|4.61|
|Adam|6.33|4.49|

#### 3. Baseline NMT + Attention (RNN)
* improved BLEU to 28.1 on dev. and 20.63 on test set

#### 4. Baseline NMT + Attention (RNN)+ Rare Words method
* external dictionary more favourable on this small data set

|Approach|dev. BLEU|test BLEU|
|--------|---------|---------|
|Baseline NMT + Attention|28.1|20.63|
|ext. dictionary|28.09|21.03|
|discounting|25.88|19.79|

#### 5. Baseline NMT + Attention (LSTM) (+ Rare Words?)
* no improvement when using LSTM to alleviate vanishing gradient issue
* tested 2 to 6 hidden layers

#### 6. Baseline NMT + Attention (RNN) + Rare Words + Word Penalty (Beam Size equivalent) Modification
* word penalty = 1 means no modification is done onto generated sentence
    * decreasing and system tends to produce longer sentences
    * experiments yield optimal beam size of 20 and best word penalty is 0.5
* improvement to 32.05 BLEU on dev. and 24.37 BLEU on test
    * small gap to SMT that performs better than this model due to limited training corpus

## Notes
* experiments done on small dataset
* this paper gives a small overview on basic techniques on neural machine translation, not comprehensive!
    * operation on subword units like byte-pair encoding missing
* just application of previous methods in NMT research

### Minus
* weird title; slightly *missleading*?
* experiments
    * SMT system details unclear
    * NMT training details not specified
        * did not specify any details on 3rd model (NMT + attention mechanism)
        * training set of external dictionary not mentioned (4th model)+
