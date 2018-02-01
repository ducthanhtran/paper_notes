# Deep Architectures for Neural Machine Translation
* [arXiv 2017](https://arxiv.org/abs/1707.07631)
* Proceedings of the Conference on Machine Translation (WMT), vol. 1: Research Papers. ACL 2017
  * [ACL 2017](http://www.aclweb.org/anthology/W17-4710)

**Authors**:
* Barone, Antonio Valerio Miceli
* Helcl, Jindrich
* Sennrich, Rico
* Haddow, Barry
* Birch, Alexandra

## Related Work
* [Massive Exploration of Neural Machine Translation Architectures by Britz et al., 2017](https://github.com/ducthanhtran/paper_notes/blob/master/machine_learning/nlp/machine_translation/17_massive_exploration_of_nmt_architectures.md)

## Key points
* experimental investigations on stacked and deep transition recurrent architectures, that is, depth of architectures.
* evaluate baseline architecture (encoder-decoder with attention) with GRUs with some variants

### Deep Transition Architectures ###
*  GRU transition blocks within each timestep

### Stacked Architectures ###
* stack GRUs with help of residual connections between states in order to improve gradient flows

#### Alternating Stacked Encoder ####
* forward part of encoder:
  * alternate between forward and backwards direction
  * employ residual connections
* backwards part of encoder: begin with backwards direction on first level, then alternate with forward direction like forward part of encoder in similar fashion

#### Biunidirectional Stacked Encoder ####
* forward and backward parts are shallow like in baseline
* simply feed in concatenated states to subsequent stacked GRUs that operate in a forward manner


## Experiments

### Results

## Comments
