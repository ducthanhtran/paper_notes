# Joint Training for Neural Machine Translation Models with Monolingual Data
* [arXiv 2018](https://arxiv.org/abs/1803.00353)
* AAAI 2018

**Authors**:
* Zhang, Zhirui
* Liu, Shujie
* Mu, Li
* Zhou, Ming
* Chen, Enhong

## Key points
* build upon [Backtranslation](machine_learning\nlp\machine_translation\15_improving_nmt_with_monolingual_data.md) approach in order to incorporate monolingual data
  * use both source and target monolingual data to improve both src->target and target->src models
  * iterative process
* use source-to-target model A and target-to-source model B:

1. pretrain both A and B on parallel corpus
2. translate monolingual source data S with A and obtain T'
3. translate monolingual target data T with B and obtain S'
4. train new model A on parallel corpus + synthetic one from 3.
5. train new model B on parallel corpus + synthetic one from 2.
6. if not converged, GOTO 2.

* weight sentences
  * parallel corpus: 1
  * synthetic corpus: with translation model A or B
  * penalize weak synthetic translations

### Experiments ###
#### Results ####

## Comments
