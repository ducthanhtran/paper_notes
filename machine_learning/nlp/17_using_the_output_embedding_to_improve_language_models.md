# Using the Output Embedding to Improve Language Models
* [arXiv 2016](https://arxiv.org/abs/1608.05859)
* Proceedings of the 15th Conference of the European Chapter of the Association for Computational Linguistics: Volume 2, Short Papers, April 2017
  * [ACL 2017](http://aclweb.org/anthology/E17-2025)

**Authors**:
* Press, Ofir
* Wolf, Lior

## Key points ##
* study top-most weight matrix of neural network language models (NN-LM): acts as 'output embedding'
  * effect of weight tying on three categories: NNLMs, word2vec skip-gram model and neural machine translation (NMT) model


## Experiments ##
* NNLMs
  * bi-LSTM with scoring and softmax layer
  * cross entropy loss
  * models
    * large: +dropout on added projection matrix on 2nd LSTM layer output, lambda=0.15
    * small: no regularization
  * SGD
  * untied NNLM
    * during training only input embedding row that corresponds to input is updated
    * therefore rare words only obtain small number of updates!
    * output embedding on the other hand obtain updates on every row in every timestep
  * tied NNLM
    * set input embedding := output embedding := matrix S
    * every row of S is updated for every iteration
    * update similar to untied NNLM except for one
* word2vec skip-gram model
  * nearly same as NNLMs with exception of upper LSTM layer, where identity is used instead
* NMT model
  * many subword units [(Sennrich et al, 2016)](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/16_nmt_of_rare_words_with_subword_units.md) are shared by source and target vocabulary
  * experiment 1: tie input and output embeddings of decoder
  * experiment 2: tie input embedding of encoder and  input/output embedding of decoder (three-way weight tying, TWWT for short)

### Data ###
* text8 datasets
* Penn Treebank

### Results ###
* embedding quality with metricssimlex999, Verb-143, MEN, Rare-Word, MTurk-771
  * NNLMs
    * small model
      * input embedding always inferior to output one
      * by tying weights we achieve better performance w.r.t. used metrics, on par with output embeddings in untied NNLM
  * word2vec skip-gram model
    * on text8 datasets
    * degradation for all metrics when weight tying is applied
* embedding similarity

* NMT
  * TWWT model has about 28% fewer parameters but BLEU score are similar to baseline
  * same observation for tied decoder embeddings

## Comments ##
* embedding quality for large NNLM missing
*
