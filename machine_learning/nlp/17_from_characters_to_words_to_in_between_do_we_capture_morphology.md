# From Characters to Word to in Between: Do We Capture Morphology?
* [arXiv 2017](https://arxiv.org/abs/1704.08352)
* Proceedings of the 55th Annual Meeting of the ACL, August 2017
  * [ACL 2017](http://www.aclweb.org/anthology/P17-1184)

**Authors**:
* Vania, Clara
* Lopez, Adam


## Key points ##
* study about different word representations through subword units in NLP
  * alleviate problem of rare and out-of-vocabulary (OOV) words
  * model might learn about morphological variants, i.e. linguistic rules
* differ between four processes of morpheme compositions (typology): fusional, agglutinative, root+pattern and reduplication
* done on language modeling task
* representational models:
  * subword representations:
    * character
    * character trigram
    * morph types like BPE
  * compositional functions to obtain word representation
    * summation of subword units except character representations
    * bidirectional LSTM (bi-LSTM) (see Ling et al., 2015, Finding function in form: compositional character models for open vocabulary word representation)
    * CNN + Highway layers for character inputs


## Experiments ##
* language model: RNN with LSTM units
  * re-implemented all models in a single framework using Tensorflow: [Github](https://github.com/claravania/subword-lstm-lm)
  * two hidden layers with 200 hidden units
  * word/character/morph vectors use 200 dimensions
  * random and uniformly initialized
  * SGD with minibatch size of 32
    * learning rate of 1.0, decrease by half if validation perplexity (PPL) doesn't decrease by 0.1 for 3 epochs
    * fixed learning rate of 0.2 for models with bi-LSTMs. Stop training if validation PPL doesn't improve after 3 epochs
  * dropout of 0.5 on input-to-hidden layer + all LSTM cells
* test on ten langauges
  * fusional: Czech, English, Russian
  * aggulinative: Finnish, Japanese, Turkish
  * root+pattern: Arabic, Hebrew
  * reduplication: Indonesian, Malaysian


### Results ###

## Comments ##
