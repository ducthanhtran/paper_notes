# One Decade of Statistical Machine Translation: 1996-2005
* CLIN, 2005

**Authors**:
* Ney, Hermann

## Key points
* traditional non-statistical approach: rule-based
  * completeness and consistency are a problem
* statistical machine translation (SMT) instead uses probability distributions
  * language and translation model
  * alignment model captures correspondences between source and target words (kind of prior information)
    * not unique correspondence -> use probability distributions as well
    * incorporate into translation model
  * forms foundation of any non-traditional approach in machine translation (MT)
  * major improvements in SMT due to:
    * automatic evaluation metrics like BLEU, WER and PER allow fast train/test procedures of systems
    * more efficient algorithms for training: alignment-lexicon models
    * context-dependent/phrase-based lexicon models
    * generation algorithm: beam search
    * log-linear model combinations and rescoring
    * better hardware ressources and parallel copora for training

### Advantages of using probability distributions/statistics
* probabilities denote scores that are normalized
* combining scores: either multiplication or summation
* ambiguity can be modeled
* probability distributions can be learned by algorithms

### Tasks in SMT
1. error measure: Bayes decision rule based on minimizing posterior risk -> require error measure/rate
2. probability models: replaces true and unknown probability distribution
3. training criterion: learn free parameters of probabilirt models from training data
4. decision rule: search problem of selecting most suitable target sentence

## Comments
* good overview of SMT research from 1996 to 2005
