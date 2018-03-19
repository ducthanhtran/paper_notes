# Universal Neural Machine Translation for Extremely Low Resource Languages
* [arXiv 2018](https://arxiv.org/abs/1802.05368)
* [Microsoft](https://www.microsoft.com/en-us/research/publication/universal-neural-machine-translation-extremely-low-resource-languages/)
* 16th Annual Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies (NAACL-HLT), 2018

**Authors**:
* Gu, Jiatao
* Hassan, Hany
* Devlin, Jacob
* Li, Victor O.K.

## Key points
* tackle problem of translation with low-resource languages that do not have much parallel data
* main approach: transfer learning from rich-resource languages using multi-lingual, namely many-to-one, neural machine translation (NMT) setting
  * share lexical and sentence level representations from multiple source languages
  * source languages have small/limited data, some even have zero data
  * multi-lingual setting: avoid overfitting and utilize knowledge of other languages in translation
* challenges in training a multi-lingual NMT model
  * lexical-level sharing
  * sentence-level sharing
* proposal of *universal NMT* model with focus on low-resource data
* two vital components:
  * universal lexical representation (ULR)
    * each word represented by probabilistic mixture of universal space word embeddings: semantically similar words from different languages are projected in same space
  * mixture of language experts (MoLE)
    *

### Experiments ###
#### Results ####

## Comments ##
